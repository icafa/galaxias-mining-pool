## How to Use EthOS to Mine Galaxias Through a Stratum Pool 

Click for instructions on [[how_to_install_and_configure_the_open-ethereum-pool_for_the_galaxy_blockchain|establishing a Galaxias mining pool]].

Note that this guide assumes that you have EthOS installed and working for your system and GPU processors.  You may need to check the [[http://ethosdistro.com/kb/|EthOS Knowledge Base]] if your EthOS installation is not ready.

### Connecting with EthOS 

Once you have installed EthOS, you will want to follow these simple instructions:

  * Unordered List ItemLog in as user "ethos"
  * Remove (or rename) the "remote.conf" file
  * Copy local.conf to local.conf.Backup
  * Edit /home/ethos/local.conf to read as follows:

```
globalminer sgminer
maxgputemp 85
stratumproxy enabled
proxywallet <your-glx-wallet-address
proxypool1 <your-mining-pool-domain-or-ip-address>:8008
flags --cl-local-work 128 --cl-global-work 16384 --farm-recheck 200
globalfan 85
globalpowertune 50
```

Depending on your mining rig, you may wish to adjust the settings such as fan, maxgputemp, etc to meet manufacturer's recommendations or best practices for your hardware  You may also substitute "ethminer" for "sgminer" if you wish to use that mining package, although better results have so far been had with sgminer.

  * Next type "r" to reboot your EthOS server

When your server reboots it should automatically connect to the mining pool specified in local.conf.  You can verify this on your EthOS rig with the "show miner" command-line command.  If your mining pool has a web-based UI you should now see your rig's status in the pool

See [[how_to_run_the_mining_pool_web_ui|How to Run the Mining Pool Web UI]] if appropriate.
