sudo apt update && sudo apt upgrade && sudo apt autoremove

sudo apt -y install cmake liblog4cpp5-dev libv4l-dev git
git clone https://github.com/mpromonet/v4l2rtspserver.git
cd v4l2rtspserver/
cmake .
make
sudo make install

v4l2-ctl --list-devices

sudo nano /lib/systemd/system/v4l2rtspserver.service

ExecStart=/usr/local/bin/v4l2rtspserver -W 640 -H 480 -F 24 -P 8554 /dev/video0
