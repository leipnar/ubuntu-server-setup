# ubuntu-server-setup

🌟 A simple bash script for setting up Ubuntu Server

What does this script do? you can select to:

Update & Upgrade Server 🧬
Install essential packages 🎉
Install Speedtest 🚀
Create SWAP File 💾
Enable BBR 🛸
Automatically update and restart the server every night at 01:00 GMT+3:30 ⏳
Install X-UI (Marzban) 🦄
Install Pi-Hole Adblocker 🛡️
Install & set WARP Proxy ✨
Install Erlang MTProto Proxy 💫
Install Hysteria II 🌈
Install TUIC v5 🔥
⚠️ Manually set the parameters yourself when prompted during the setup.

How to run ❓
Run it only on a fresh install of Ubuntu 22.04.

curl -O https://raw.githubusercontent.com/leipnar/ubuntu-server-setup/blob/main/setup.sh && chmod +x setup.sh && sed -i -e 's/\r$//' setup.sh && ./setup.sh

💠 After setup has completed, don't forget to:
Add your desired adlists via Pi-hole web interface
https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts
https://raw.githubusercontent.com/d3ward/toolz/master/src/d3host.txt
https://big.oisd.nl/
https://raw.githubusercontent.com/hagezi/dns-blocklists/main/domains/pro.txt
https://blocklistproject.github.io/Lists/abuse.txt
https://blocklistproject.github.io/Lists/ads.txt
https://blocklistproject.github.io/Lists/crypto.txt
https://blocklistproject.github.io/Lists/drugs.txt
https://blocklistproject.github.io/Lists/fraud.txt
https://blocklistproject.github.io/Lists/gambling.txt
https://blocklistproject.github.io/Lists/malware.txt
https://blocklistproject.github.io/Lists/phishing.txt
https://blocklistproject.github.io/Lists/ransomware.txt
https://blocklistproject.github.io/Lists/redirect.txt
https://blocklistproject.github.io/Lists/scam.txt
https://raw.githubusercontent.com/MasterKia/PersianBlocker/main/PersianBlockerHosts.txt
Update Pi-hole Database
pihole -g
Modify Lighttpd
⭕ If you have installed Pi-hole, then Lighttpd is listening on port 80 by default. If you haven't changed the Lighttpd port, it's necessary to stop it before obtaining SSL certificates. Below, you can find commands to start, stop, restart, and modify the configuration of Lighttpd.

sudo nano /etc/lighttpd/lighttpd.conf
sudo systemctl start lighttpd.service
sudo systemctl stop lighttpd.service
sudo systemctl restart lighttpd.service
Obtain SSL Certificates
sudo certbot certonly --standalone --preferred-challenges http --agree-tos --email yourmail@gmail.com -d sub.domain.com
Change SSH Port
sudo nano /etc/ssh/sshd_config
sudo systemctl reload sshd
Setup UFW
sudo nano /etc/default/ufw
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow SSHPORT/tcp
sudo ufw limit SSHPORT/tcp
sudo ufw allow PORT
sudo ufw enable
sudo ufw status verbose
sudo systemctl enable ufw
Change WARP License Key
warp-cli set-license <your-warp-plus-license-key>
WARP Status
bash <(curl -fsSL git.io/warp.sh) status
Change Server DNS to use Pi-hole
sudo nano /etc/resolv.conf
nameserver 127.0.0.53
If /resolv.conf managed by systemd-resolved, then you have to follow these steps:

cd /etc/netplan/
ls
nano ab-cloud-init.yaml
sudo netplan apply
You need to add the following settings to the 'ab-cloud-init.yaml' file:

nameservers:
  addresses: [127.0.0.53]
Restart your server with
sudo shutdown -r now
Optional: Install qbittorrent-nox 🔮
sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable
sudo apt update
sudo apt install qbittorrent-nox
sudo nano /etc/systemd/system/qbittorrent-nox.service
qbittorrent-nox
sudo adduser --system --group qbittorrent-nox
sudo adduser root qbittorrent-nox
sudo systemctl daemon-reload
sudo systemctl enable qbittorrent-nox
sudo systemctl start qbittorrent-nox
sudo systemctl status qbittorrent-nox
qbittorrent-nox.service configuration
[Unit]
Description=qBittorrent-nox
After=network.target

[Service]
Type=forking
ExecStart=/usr/bin/qbittorrent-nox -d --webui-port=8000
Restart=on-failure

[Install]
WantedBy=multi-user.target
Optional: Install AriaFileServer 🪄
See HTTPS version at https://github.com/ErfanNamira/AriaFileServer

⭐ HTTP Version
✨ http://IP:Port

cd /home/qbittorrent-nox/Downloads
wget https://raw.githubusercontent.com/ErfanNamira/AriaFileServer/main/AriaFileServerHTTP.py
sudo apt install python3-pip
pip3 install flask passlib
python3 AriaFileServerHTTP.py
Optional: Install simplefileserver 🪩
⚠️ simplefileserver DO NOT Support Authentication

cd /home/qbittorrent-nox/Downloads
wget https://github.com/sssvip/simple-file-server/releases/download/v0.1.4/simple-file-server_0.1.4_linux_amd64.tar.gz
tar -xzvf simple-file-server_0.1.4_linux_amd64.tar.gz
chmod 777 simplefileserver
sudo /home/qbittorrent-nox/Downloads/simplefileserver 80
Optional: WARP XrayConfig ✨
{
  "protocol": "socks",
  "settings": {
    "servers": [
      { 
        "address": "127.0.0.1",
        "port":40000
      }
    ]
  },
  "tag":"warp"
},
Used Projects 💞
https://github.com/pi-hole
https://github.com/alireza0/x-ui
https://github.com/MHSanaei/3x-ui
https://github.com/deathline94/tuic-v5-installer
https://github.com/deathline94/Hysteria-Installer
https://github.com/sssvip/simple-file-server
https://github.com/seriyps/mtproto_proxy
https://github.com/P3TERX/warp.sh
https://github.com/blocklistproject/Lists
