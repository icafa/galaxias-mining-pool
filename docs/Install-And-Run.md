## How to Install and Configure open-galaxias-pool for the Galaxy Blockchain

10 Jan 2018

updated 22 May 2018 re: first fork from open-ethereum-pool and entry to GitLab

This documents how to install and configure the open-galaxias-pool for use with the Galaxy Blockchain on Ubuntu 16.04.  Since the Galaxy Blockchain is not compatible with Parity, please follow the separate instructions to connect to the Galaxy Blockchain with Parity for your node connection.

### Install the project's prerequisutes 

Dependencies:

    go >= 1.9
    geth or parity
    redis-server >= 2.8.0
    nodejs >= 4 LTS
    nginx


### Install the open-ethereum-pool Project 

```
$ git config --global http.https://gopkg.in.followRedirects true
$ git clone git@gitlab.securesystemdesign.io:GALAXIAS/OpenGalaxiasPool.git
$ cd open-galaxias-pool
$ make
```

### Configuring and Running the open-galaxias-pool 

#### Configure the Mining Pool 

Copy the file open-ethereum-pool/config.example.json to open-ethereum-pool/config.json and edit the values to match your setup.  Among them:

```
"coin": "glx",

"proxy": {
  ...
  "listen": "<your-ip-address>:8888"
  ...
  "stratum": {
     ...
     "listen": "<your-ip-address>:8008",
  ...
  
"api": {
    "listen": "your-ip-address>:8080",

```

Do not configure unlocker or payouts at this time.  (See below).

Another document covers the [[how_to_run_the_mining_pool_web_ui|Mining Pool Web UI]].

### Run the Mining Pool 

Once Parity is running (connected to the Galaxy Blockchain) you can start the mining pool.  From the open-ethereum-pool directory:

```
$ ./build/bin/open-ethereum-pool config.json
```

### Configuring Payouts for the open-ethereum-pool 

The config.json file used in the previous step contains the payouts module.  However it is disabled by default.  The payouts module must be run as a separate instance.  So create a new file "payouts.json" and populate it with the following lines that are taken from the config.json file.  Be sure to use the same name for the coin, etc. and be sure to modify the "unlocker" and "payouts" section accordingly.  For example:

```
{
        "threads": 2,
        "coin": "glx",
        "name": "mygreatpool",

        "redis": {
                "endpoint": "127.0.0.1:6379",
                "poolSize": 10,
                "database": 0,
                "password": ""
        },

        "unlocker": {
                "enabled": true,
                "poolFee": 0,
                "poolFeeAddress": "",
                "donate": false,
                "depth": 120,
                "immatureDepth": 20,
                "keepTxFees": false,
                "interval": "10m",
                "daemon": "http://127.0.0.1:8545",
                "timeout": "10s"
        },

        "payouts": {
                "enabled": true,
                "requirePeers": 10,
                "interval": "360m",
                "daemon": "http://127.0.0.1:8545",
                "timeout": "10s",
                "address": "<your-author-address-goes-here>",
                "gas": "21000",
                "gasPrice": "50000000000",
                "autoGas": true,
                "threshold": 50,
                "bgsave": false
        }

}
```

### Connecting to the Mining Pool

Assuming the instructions have worked so far you should be able to connect any stratum-capable miner to the mining pool at your mining pool's IP address and the stratum port specified in config.json (default 8008).  For more information, please read these documents:

  * [[how_to_use_ethos_to_mine_galaxias_through_a_stratum_mining_pool|Connecting EthOS to a Galaxias Stratum Pool]]
  * [[how_to_use_a_solo_miner_to_mine_galaxias|How to Use a Solo Miner to Mine Galaxias]]

