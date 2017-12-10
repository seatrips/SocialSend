

Installation Instructions:

Dependencies required:
sudo apt-get install -y pkg-config
sudo apt-get -y install build-essential autoconf automake libtool libboost-all-dev libgmp-dev libssl-dev libcurl4-openssl-dev git
sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update
sudo apt-get install libdb4.8-dev libdb4.8++-dev

Compiling from source:
sudo git clone https://github.com/SocialSend/SocialSend.git
rename SocialSend to socialsend
cd socialsend
sudo chmod +x share/genbuild.sh
sudo chmod +x autogen.sh
sudo chmod 755 src/leveldb/build_detect_platform
sudo ./autogen.sh
sudo ./configure
sudo make
sudo make install

Move to bin folder for easier access:
cd src
sudo cp sendd /usr/local/bin/
sudo cp send-cli /usr/local/bin/

To Execute:
sendd
Follow instructions.

To Start Server:
sendd -daemon

To input wallet commands:
send-cli -[InsertWalletCommand]
