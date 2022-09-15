# Install a Full Besu Node using Bonsai Storage on Ubuntu Server


## Who is this guide for
This guide is geared toward those who wish to set up an Ethereum Layer-1 node on a dedicated machine. This guide does not discuss using Docker or running this in a virtual machine.

The example node software here is using [Besu](https://besu.hyperledger.org/en/stable/){target=_blank}, however, installating other clients such as Erigon, Geth, OpenEthereum or others will utilise a lot of the same concepts. Future material may cover specific setups for the other clients.

Something important to consider when running a node is [client diversity](https://ethereum.org/en/developers/docs/nodes-and-clients/client-diversity/#client-diversity-importance){target=_blank}. Having diversity is important for stability of the network, specifically in the event a flaw is found in one of the clients. If those nodes had to go offline to prevent exploits, the others can continue unaffected. To see a breakdown of known clients (not all nodes appear here, but it illustrates diversity) go to [etherenodes.org](https://ethernodes.org/){target=_blank}.

### Why run a node?
- Contribute to the network and broader ecosystem
- Be your own bank
  - send your own transactions via your node
  - validate your account state is correct - trustless
  - not be concerned with DNS exploited RPC urls
- Gain insight into what it takes learning something along the way (hopefully)
---
### TL;DR
- Prerequisites
- Install the Operating system
- Configure drives (and possibly mount)
- Install software ( Java and Besu )
- Create a service file (stop start and enable)
- Monitor and be patient
---
## Hardware requirements and future thoughts

When considering hardware, there are a number of important factors:

1. Minimum requirements for syncing and maintaining sync.
2. How soon do you want the node to be up and running? ( Faster storage and CPU )
3. How long do you intend on running the node for?
4. What kind of node you are running [Besu Node Types](https://besu.hyperledger.org/en/stable/Concepts/Node-Types/){target=_blank}. Note: Other clients (e.g. Geth) may have similar and additional options.
5. How much traffic are you personally/or your business intending on sending to the node? (can the node support many concurrent users)
6. With everything cost is always a factor. Please consider these questions carefully weighing up future extension, whether it be storage space or CPU speed. Disk space upgrades will more than likely be the only real concern if the CPU is able to process transactions fast enough.
7. Do you have internet speed/data allowance concerns?

All of the considerations above will affect your choice in hardware and if you are able to successfully run a node.

1. You will need at least 8GB of RAM and a fast hard drive [SSD/mSATA/NVME](https://www.kingston.com/unitedkingdom/en/community/articledetail/articleid/48543){target=_blank} - Sata HDDs are too slow to maintain and get to sync. Depending on your storage configuration, swap space/virtual memory may be on the same disk making HDDs even less of an option. External USB3.x SSDs have also been used to sync. Weigh up disk speed, cost, longevity, and size. At end of June 2022, a currently sync'd node with fast sync Bonsai storage is using 611GB and a Full non-Bonsai fast sync node is 980GB and growing.

2. CPU is a bottlenecking factor - As an example, A Raspberry PI 4 overclocked to 2.147ghz sat at 100% for +-4 weeks syncing, whereas a Celeron G3930 took 10 days to sync. While it is possible to sync with a Raspberry PI, a vast amount of patience is required. As the chain grows in size, this time will increase, so depending on your timelines and usage, a Raspberry Pi may not be for you. **Note:** When rollups and sharding come into play, this may require a rethink, as CPU may need to be faster to keep up when processing rollups.

3. With [EIP-4844](https://blog.developerdao.com/eip-4844-and-its-impact-on-ethereum-scalability){target=_blank} coming down the track (eta unknown), an installation may run out of storage space where you will require easily an additional 2.2TB (+-) of storage (`10mb * 5 blocks per min * 60 mins per hour * 24hrs a day * 30 days`) - you can get away with a 2TB disk to start, but will/may need more when it eventually happens depending on implementation. **Note:** the estimates here and implementation is speculative.

4. **Note** If you run something like Geth, you can also run a "light node" [All node types](https://ethereum.org/en/developers/docs/nodes-and-clients/){target=_blank} vs. a Full or Archive Node

5. If you are expecting many users to access your node through MetaMask or other wallets vs. just a few home users, more resources are recommended for processing and data access.
---
## Installation

### Tools/Software
- Storage drive for installation of operating system ( MicroSD for a Raspberry PI )
- Optional drive for Node data
- USB stick for installing
- Software for creating a bootable USB [Balena Etcher](https://www.balena.io/etcher/){target=_blank} (Cross platform) or if you prefer [Rufus](https://rufus.ie/){target=_blank} (Windows only)

## Operating System

- Download an appropriate server install image [Ubuntu Downloads](https://ubuntu.com/download/server){target=_blank} with the matching architecture (ARM is available as another option).

- If you do decide to try it on a Raspberry Pi, the images can be found at [Ubuntu for Raspberry Pi](https://ubuntu.com/download/raspberry-pi){target=_blank} and the install process for ARM will need to be used.

### **Installing on a Raspberry Pi**
 - burn the image to the MicroSD
 - put it in the Pi
 - start the Pi and follow any configuration steps

### **Installing on a dedicated non-Pi machine**

- Create a bootable USB stick with the operating system
  - [Mac](https://ubuntu.com/tutorials/create-a-usb-stick-on-macos#1-overview){target=_blank}
  - [Ubuntu](https://ubuntu.com/tutorials/create-a-usb-stick-on-ubuntu#3-launch-startup-disk-creator){target=_blank}
  - [Windows](https://ubuntu.com/tutorials/create-a-usb-stick-on-windows#1-overview){target=_blank}
- Set your machine's BIOS to boot from the USB
- Boot from the USB
- Install the operating system enabling SSH [Install Step by Step](https://ubuntu.com/server/docs/install/step-by-step){target=_blank}. You won't need to install any snaps.
- The default file format is `ext4`, if you prefer `xfs` works as well
- When creating a user, this will be your admin user, once installation is complete and the server rebooted, a specific user will be created to run Besu with.
---
## **Initial OS Post-Installation Steps (both Pi and Non-Pi)**

## Upgrades
- Update and upgrade to make sure you have the latest packages (`sudo apt update && sudo apt upgrade -y && sudo reboot`)
---
## Utilities
- Install some basic utilities for networking and disk monitoring (`sudo apt install net-tools dstat jq -y`)
  - net-tools (for basic networking tools)
  - dstat (to monitor disk usage)
  - jq for nicely formatting RPC responses 
---
## Networking

**This assumes a wired network connection**

In order to make life easier when accessing your node/machine from other machines in the network or via SSH, it is advisable to set up a static IP Address. 
- Configure a static IP on your router for the MAC address if you are able to
  - To see your current IP address type in `ifconfig`
    - you should see something like `eth0` or `enp0s31f6` and a value next to `inet` for your IP
    - your MAC should be next to `ether`
     ```
     inet 192.168.85.6  netmask 255.255.255.0  broadcast 192.168.85.255
     inet6 fe23::7223:c2ff:fe69:81aa  prefixlen 64  scopeid 0x20<link>
     ether 50:a5:c2:6a:81:12  txqueuelen 1000  (Ethernet)
     ```
- Assign a static private IP address to your node with netplan ( see example below )
  - Edit your network configuration file (your name may differ) to create a static address for easy access (`sudo nano /etc/netplan/`) - **note** the spacing is critical. If done, and using nano press `control-o` and then after, press `enter` to save, followed by `control-x` to exit
  - see [netplan](https://netplan.io/examples/){target=_blank} for more instructions if you get stuck or want to know about wireless configuration

**An example:**

In `/etc/netplan/50-cloud-init.yaml` (your name may be different - check `ls /etc/netplan` to find yours)

**Note:** spacing in the yaml file is critical and needs to be maintained, else you might encounter errors such as

`Invalid YAML at /etc/netplan/50-cloud-init.yaml line 7 column 6: did not find expected key`

```
network:
  version: 2
  ethernets:
    enp0s31f6:
      addresses:
        - 192.168.50.18/24
      nameservers:
        addresses: [192.168.50.1]
      routes:
        - to: default
          via: 192.168.50.1
```
- Press `sudo netplan apply` to set the changes immediately (you may be disconnected if you are on another address)
- These changes should persist post reboot

---
## Disk management

**Disk allocation**
- If you are using an internal SSD, check all the space on the disk has been allocated ( `df -ha`)

You should see something like
```
/dev/mapper/ubuntu--vg-ubuntu--lv  109G  7.8G   96G   8% /
```

If this does not match your drive size, you might consider extending the space: **USE WITH CAUTION** [Extend your lvm space](https://packetpushers.net/ubuntu-extend-your-default-lvm-space/){target=_blank}

### If using an internal disk
- add a folder to contain node data (`sudo mkdir /besu`)

### If using an external disk

**Format and mount an external drive**

The main steps for this
- Plug the external drive in
- Type `sudo fdisk -l` - this should show you a list of devices - e.g.

```
Disk /dev/sdb: 1.82 TiB, 2000398934016 bytes, 3907029168 sectors
Disk model: Portable SSD T5
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 33553920 bytes
```

Once worked out which is your disk (e.g. `/dev/sdb` here)
- `sudo mkfs.xfs /dev/sdb` [see all formatting options](https://linux.die.net/man/8/mkfs.xfs){target=_blank}
- follow the prompts pressing yes where you need to (**be sure it is the correct drive**)

You should see output similar to:
```
mkfs.xfs /dev/sdb
meta-data=/dev/sdb               isize=512    agcount=4, agsize=5242880 blks
         =                       sectsz=512   attr=2, projid32bit=1
         =                       crc=1        finobt=0, sparse=0
data     =                       bsize=4096   blocks=20971520, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=1
log      =internal log           bsize=4096   blocks=10240, version=2
         =                       sectsz=512   sunit=0 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
```

- add a `ssd` mount directory to the system `sudo mkdir /mnt/ssd`
- mount the drive to the folder `sudo mount /dev/sdb /mnt/ssd`
- add a folder to contain node data (`sudo mkdir /mnt/ssd/besu`)

To make this mounting will persist on reboot:

- type `sudo blkid`- you should see entries similar to:

```
/dev/sdb: UUID="b8222ca7-29dd-44c0-be50-7ffcc3348c14" TYPE="LVM2_member" PARTUUID="1e95b59d-4481-4e04-a016-24a099e7ae64" or
/dev/sdb: UUID="b8222ca7-29dd-44c0-be50-7ffcc3348c14" PARTUUID="1e95b59d-4481-4e04-a016-24a099e7ae64"
```
- find the UUID that matches your device and `copy the UUID (not quotes)`
- type `sudo nano /etc/fstab` where you will store the reboot settings
- add a line at the bottom `UUID=b8222ca7-29dd-44c0-be50-7ffcc3348c14 /mnt/ssd xfs defaults 0 0` replacing the UUID with yours
- press `control-o` and then after, press `enter` to save, followed by `control-x` to exit
- reboot to confirm changes and auto-mounting `sudo reboot`
- when rebooted and logged in type `df -ha` and you should see entries similar to the following ( last line )

```
Filesystem                         Size  Used Avail Use% Mounted on
sysfs                                 0     0     0    - /sys
proc                                  0     0     0    - /proc
udev                               5.7G     0  5.7G   0% /dev
devpts                                0     0     0    - /dev/pts
/dev/sdb                           1.9T    0G  1.9T   0% /mnt/ssd
```

**Adjusting Swap space**

Depending on how many disks you have installed and if they are internal/external, the pathing instructions below would need to be adjusted [see full instructions](https://linuxize.com/post/how-to-add-swap-space-on-ubuntu-20-04/){target=_blank}
- Swap space on some installs are added by default ( not on the Pi ), follow this if you want extra swap space 
- Replace `/swapfile` below with `/mnt/ssd/swapfile` if you want to use the external drive - i.e if the Pi is using a slower MicroSD
- Add swap space (generally a 1:1 with physical memory depending on how much you have) `sudo fallocate -l 8G /swapfile` (or `sudo fallocate -l 8G /swapfile`)
- Set permissions `sudo chmod 600 /swapfile` or  `/mnt/ssd/swapfile`
- Convert the file to swap `sudo mkswap /swapfile` or  `/mnt/ssd/swapfile`
- Turn it on `sudo swapon /swapfile` or  `/mnt/ssd/swapfile`
- Open the boot file to turn it on at reboot `sudo nano /etc/fstab` ( you may notice an existing `swap.img` file already created matching your memory)
- Add an entry at the bottom `/swapfile swap swap defaults 0 0` - then `Control-o`, `Enter` and `Control-x` to save and quit
- Show the swap space available `sudo swapon --show`
---

## BESU BUILD AND INSTALL STEPS
At this point, you should have an updated machine with swap space, a custom user to run the process under and a disk that is ready to go. 

- check for java (`java --version`) - this should either give you a version or tell what versions are available to install
- install java with a current version (`sudo apt install openjdk-17-jre-headless -y`) ( or a higher version )

For Raspberry Pi see:

- Oracle and Java.net
- [sdkman](https://sdkman.io/){target=_blank} 
- [adoptium](https://adoptium.net/temurin/releases/){target=_blank}
- Follow the instructions there 

Once installed
- check for java (`java --version`) to make sure it installed 

### Summarised build steps
```
- install dependencies: sudo apt install libsodium23 libnss3 -y
- make a folder for code: mkdir ~/code
- navigate to the folder: cd ~/code
- clone the source code: git clone --recursive https://github.com/hyperledger/besu
- navigate to source: cd besu
- switch to a release branch (to find these type: git branch -r) e.g. git checkout release-22.4.0 or stay on main for latest
To see all of the gradle tasks that are available (or just skip to installDist)

cd besu (if not already)
./gradlew installDist (wait for it to complete)

```

### Install Steps
- Once the build steps are complete
- Copy the `besu` folder from the build folder to `/usr/bin/` e.g. `sudo cp -r ~/code/besu/build/install/besu  /usr/bin/besu`
- Check your besu version `/usr/bin/besu/bin/besu --version`
- Add user to run the process under e.g. `sudo useradd username` ( e.g. `sudo useradd eth`) - for more in depth options on users: [Creating users with useradd](https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/){target=_blank}

**If using an internal disk**
- Assign ownership of the besu folder `sudo chown -R eth:eth /besu` (replace `eth` with your chosen username) - this is needed to create and maintain files

**If using a mounted disk**
- Assign ownership of the besu folder `sudo chown -R eth:eth /mnt/ssd/besu` - this is needed to create and maintain files

**Create a Service/Unit File**

- type in `sudo nano /etc/systemd/system/besu.service`
- paste in the below after changing the following values:
  - `--sync-mode=FAST` will create a non-archive node - use `--sync-mode=FULL` if you want the archive option
  - change `192.168.50.18` to the earlier set IP in order to use it in your local network
  - change `YourIdentity` to something that you want to use to identify your node
  - `--p2p-host` can be changed to an external IP if fixed for discovery - default is 0.0.0.0
  - `--data-path=` should point to where you want to store the data ( `/besu` or `/mnt/ssd/besu`)

```
[Unit]
Description=Besu daemon
After=network-online.target
Wants=network-online.target

[Service]
PermissionsStartOnly=true
ExecStart=/usr/bin/besu/bin/besu --host-allowlist="*" --data-storage-format=BONSAI --sync-mode=FAST --identity=YourIdentity --data-path=/mnt/ssd/besu --rpc-http-enabled --rpc-http-host=192.168.50.18 --rpc-http-port=8545 --rpc-http-cors-origins="*" --nat-method=NONE --p2p-host=0.0.0.0

Restart=on-failure
TimeoutStopSec=600

# Directory creation and permissions
####################################
User=eth
Group=eth

PrivateTmp=true

# Mount /usr, /boot/ and /etc read-only for the process.
ProtectSystem=full

# Deny access to /home, /root and /run/user
ProtectHome=true

# Disallow the process and all of its children to gain new privileges
# through execve().
NoNewPrivileges=true

# Use a new /dev namespace only populated with API pseudo devices such as
# /dev/null, /dev/zero and /dev/random.
PrivateDevices=true

[Install]
WantedBy=multi-user.target
```

- press `control-o` and then after, press `enter` to save, followed by `control-x` to exit
- type `sudo systemctl start besu` - this should start the service
- type `sudo systemctl status besu` - this should show you the status - similar to:

```
● besu.service - Besu daemon
     Loaded: loaded (/etc/systemd/system/besu.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2022-06-26 19:37:21 UTC; 15h ago
   Main PID: 726 (java)
      Tasks: 78 (limit: 13869)
     Memory: 10.6G
        CPU: 9h 5min 48.784s
     CGroup: /system.slice/besu.service
             └─726 java -Dvertx.disableFileCPResolving=true -Dbesu.home=/usr/bin/besu -Dlog4j.shutdownHookEnabled=false -Dlog4j2.formatMsgNoLookups=true -Djava.util.logging.manager=org.apache.logging.log4j.jul.LogManager --add-opens java.base/sun.security.provider=ALL-UNNAMED --add-opens java.base/java.util=ALL-UNNAMED -Dio.netty.tryReflectionSetAccessible=true --add-exports java.base/jdk.internal.misc=ALL-UNNAMED --add-ope>
```

- type `sudo systemctl enable besu` - this will let it start on reboot

**Monitoring the service**
- type `tail -f /var/log/syslog` to follow the logs `control-c` to exit
- type `sudo systemctl status besu` to see if it is running
- type `dstat` to see the disk usage - if it sits at 0 for a long time it may be stalled
  - create a get block script
  - type `sudo nano getBlock.sh`
  - paste in the following changing the IP address (192.168.50.18) to your server IP
   
    ```
    #!/bin/bash
    val=$(curl -X POST --data '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":51}' http://192.168.50.18:8545 --silent | jq -r '.result')
    echo $(($val))
    ```
  - press `control-o` and then after, press `enter` to save, followed by `control-x` to exit
  - type `sudo chmod +x getBlock.sh` to allow it to be executed
  - to run it type `./getBlock.sh` - this will tell you how far it has gotten
  - additional commands you can create scripts with (e.g. [eth_syncing](https://besu.hyperledger.org/en/stable/Reference/API-Methods/#eth_syncing){target=_blank}) - see [API](https://besu.hyperledger.org/en/stable/Reference/API-Methods/){target=_blank}

### Connecting to your node with Metamask

You should, once your node has synced (you should be seeing lines like the below one) be able to connect to Metamask locally:

```
Jul  6 00:15:37 besutestbed besu[124324]: 2022-07-06 00:15:37.663+00:00 | EthScheduler-Workers-2 | INFO  | PersistBlockTask | Imported #15,085,695 / 17 tx / 0 om / 1,828,694 (6.1%) gas / (0x22135e43ea450cf089fe8d0916a82a3598516badc9363df7bc8e86b1dfbf71da) in 0.289s. Peers: 54
```

Create a new connection under settings, give the ChainId as 1, node address as `http://YOURIP:8545` and a name. You can also add the Symbol as ETH.

Android Metamask Mobile requires an `https` site - another article will show you how to create a reverse proxy to your node. All other Metamask mobile and desktop ones work without the https.

## Final thoughts and security considerations

### Ports and port forwarding
It is possible to sync without opening external ports into your network, however this means all peer initiation and finding will purely be from your node, which potentially will be slower. If you do decided to open a port and forward it into your network, `it should only ever be port 30303 for peering`. As with any port opening and forwarding, do so with caution. [What is port forwarding](https://cybernews.com/what-is-vpn/port-forwarding/){target=_blank}. You might consider adding in a firewall to be more secure.

### Segementing internal networks
If you are up for more advanced networking and your hardware supports it, you could consider creating different VLANs on your network disallowing the node to talk out to your internal network, but you can talk into it to use it as your RPC endpoint for your wallet (e.g. Metamask).

### Publicly exposed IP Addresses
If you are a home user running a node, please keep in mind that your IP address will be visible to other node operators giving them a rough idea of your geolocation. Additionally, if your port forwarding is open, sites such as [ethernodes](https://ethernodes.org/){target=_blank} will index your IP. From a privacy perspective, you may want to run your node over a dedicated IP VPN. Keep in mind this may require other hardware and technical skill.

### Outdate software and operating system
- always check for and apply updates `sudo apt update && sudo apt upgrade -y`

### Future Considerations
- EIP-4844 - 30 days worth of 10mb rolled up data

## Resources
- https://consensys.net/blog/news/bonsai-tries-a-big-update-for-small-state-storage-in-hyperledger-besu/
- https://besu.hyperledger.org/en/stable/HowTo/Get-Started/Installation-Options/Options/
- https://wiki.hyperledger.org/display/BESU/Building+from+source
- https://blog.developerdao.com/eip-4844-and-its-impact-on-ethereum-scalability
- https://www.freedesktop.org/software/systemd/man/systemd.exec.html
- https://netplan.io/examples/
- https://ubuntu.com/server/docs/install/step-by-step
- https://linuxize.com/post/how-to-add-swap-space-on-ubuntu-20-04/
- https://linuxize.com/post/how-to-create-users-in-linux-using-the-useradd-command/
- https://cybernews.com/what-is-vpn/port-forwarding/
- https://ethernodes.org/
- https://besu.hyperledger.org/en/stable/Reference/API-Methods/