

# Installation Instructions:

## Dependencies required:
```
sudo apt-get install -y pkg-config
sudo apt-get -y install build-essential autoconf automake libtool libboost-all-dev libgmp-dev libssl-dev libcurl4-openssl-dev git
sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update
sudo apt-get install libdb4.8-dev libdb4.8++-dev
```
## Compiling from source:
```
sudo git clone https://github.com/SocialSend/SocialSend.git
```
rename SocialSend to socialsend
```
cd socialsend
sudo chmod +x share/genbuild.sh
sudo chmod +x autogen.sh
sudo chmod 755 src/leveldb/build_detect_platform
sudo ./autogen.sh
sudo ./configure
```
you might have to do this:
```
sudo apt-get install libqt4-dev
sudo apt-get install libjack0
sudo apt-get install libjack-dev
sudo apt-get install libasound2-dev
sudo apt-get install libsndfile1-dev
```
```
sudo make
sudo make install
```
## Move to bin folder for easier access:
```
cd src
sudo cp sendd /usr/local/bin/
sudo cp send-cli /usr/local/bin/
```
## To Execute:
```
sendd
```
Follow instructions.

To Start Server:
```
sendd -daemon
```
## To input wallet commands:
```
send-cli -[InsertWalletCommand]
```
# Add seeds

open debug console in wallet, then add following:
```
addnode 92.231.227.4:50050 add
addnode 45.76.175.211:50050 add
addnode 158.69.209.241:50050 add
addnode 165.227.106.170:50050 add
addnode 108.61.23.239:50050 add
addnode 142.91.104.115 add
addnode 104.156.225.130 add
addnode 45.55.111.224 add
addnode 66.55.159.5 add
addnode 145.239.29.157 add
addnode 67.205.181.236 add
```



## Create swap file

You will need to choose a location for your file. In this tutorial, it will be stored at the root of the server. We will create a 2GB swap file by running the following command:
```
dd if=/dev/zero of=/swapfile count=2048 bs=1M
```
The dd command will produce output in a similar format to:

2048+0 records in
2048+0 records out
2147483648 bytes (2.1 GB) copied, 10.5356 s, 204 MB/s

Next, verify that the file is located at the root of your Vultr VPS by running:
```
ls / | grep swapfile
```
Proceed if you see the swapfile file.

## Activate the swap file

Swap files are not recognized automatically. We will need to tell the server how to format the file and enable it so it can be used as a valid swap file. As a security measure, update the swapfile permissions to only allow R/W for root and no other users. Run:
```
chmod 600 /swapfile
```
The permission change can be verified by running the following command:
```
ls -lh /swapfile
```
You will see a file display:

-rw------- 1 root root 2.0G Oct  2 18:47 /swapfile

Next, tell the server to setup the swap file by running:
```
mkswap /swapfile
```
After running it, you will see the following output:

Setting up swapspace version 1, size = 2097148 KiB
no label, UUID=ff3fc469-9c4b-4913-b653-ec53d6460d0e

If everything is shown as above, you are now ready to move on to the next step.
## Turn swap on

Once your file is ready to be used as swap, you need to enable it by running:
```
swapon /swapfile
```
You can verify that the swap file is active by running the free command again.
```
free -m
```
total       used       free     shared    buffers     cached
Mem:          1840       1754         86         16         23       1519
-/+ buffers/cache:        210       1630
Swap:         2047          0       2047

If Swap shows something other than 0, then you have successfully setup swap.
## Enable swap on reboot

By default, your server will not automatically enable this new swap file. To enable it on boot, you can update the /etc/fstab file. Any text editor will suffice. In this example, I will be using nano.
```
nano /etc/fstab
```
Add the following line at the end of the file:
```
/swapfile   none    swap    sw    0   0
```
Save and close when you are finished editing the file. We are all done!
