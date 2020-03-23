## How to Use a Solo Miner to Mine Galaxias

These instructions assume you are using Ubuntu 16.04.  Other operating systems should be similar but you may have to consult documentation for your particular setup.

Note that your system must have the correct drivers for your video card and mining software of choice installed.  If this is not the case, you are not ready to begin mining on the Galaxy Blockchain.

If you will be using a mining pool, please skip to the section "[[https://wiki.securesystemdesign.io/doku.php?id=how_to_use_a_solo_miner_to_mine_galaxias#using_ethminer_in_a_stratum_pool|Using ethminer in a Stratum Pool]]" as you will not need to run a node.

### Setting up Parity 

First, you must be ready to [[how_to_connect_to_the_galaxy_blockchain|connect to the Galaxy Blockchain]].

Next, create a GLX wallet with Parity. You can use the Parity UI or on the command line from the same user account that you invoke Parity from when connectingn to the Galaxy Blockchain:

```
$ parity --chain /path/to/galaxyBlockchain.json account new
```

Then enter a password.  Do not lose this password!  It is non-recoverable.

If you prefer to [[how_to_interface_with_the_galaxy_blockchain_through_parity|connect to Parity through web3 or the UI, please visit this page]].

### Using Parity as Stratum Miner 

If you are going to mine solo (without a pool), please follow [[https://github.com/paritytech/parity/wiki/Mining|these instructions]] to [[https://github.com/paritytech/parity/wiki/Mining|use Parity as a Stratum miner]].  

Your "author" address can be any GLX address such as the one you created above.

Your command line may look something like this:

```
parity /path/to/galaxyBlockchain.json --author=<my-GLX-address> --stratum
```

This would assume that the Stratum interface will be localhost and the default port of 8008. For other options, please consult the [[https://github.com/paritytech/parity/wiki/Mining|Parity documentation]].

### Using ethminer in a Stratum Pool 

Download and install ethminer for your operating system.  (https://github.com/ethereum-mining/ethminer/releases)

Invoke ethminer.  For "<your-address>" you may use any GLX address, such as the account you created in the previous section:

```
$ /home/ethminer/bin/ethminer -G -SP yourpooldomain.com:8008 -O <your-address>
```

Note that if your pool does not have a domain name, you can substitute the IP address.  If you are mining locally, your Stratum address is not a pool address but localhost or 127.0.0.1.

### Using sgminer 

As of 15 February 2018 solo mining with sgminer has not been attempted.  However mining with sgminer on EthOS has been very successful and there is every reason to expect success if you use a solo miner to mine Galaxias with sgminer assuming your card has at least 1024MB RAM.  However nVidia cards and sgminer sometimes don't get along and this is not related to the Galaxy Blockchain: 

Reference: [[ https://github.com/genesismining/sgminer-gm/issues/103 | https://github.com/genesismining/sgminer-gm/issues/103 ]]
