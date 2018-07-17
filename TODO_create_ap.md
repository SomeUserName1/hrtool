# AcessPoint integration while not blocking the network card

1. Tool  
[create_ap](https://github.com/oblique/create_ap)
2. Dependencies
```
sudo apt-get install util-linux procps hostapd iproute2 iw haveged dnsmasq iptables openssh-server
```
3. Build & Install  
```
git clone https://github.com/oblique/create_ap
cd create_ap
sudo make install
```
4. Run   
Form Bash:
```
create_ap wlan0 wlan0 HR-SophiaX AMysteriousGenericPassPhraseLike'TheForgeIsComing'
```
At start-up using systemd:  
```
sudo vim /etc/create_ap.conf
```

```
CHANNEL=default
GATEWAY=10.0.0.1
WPA_VERSION=2
ETC_HOSTS=0
DHCP_DNS=gateway
NO_DNS=0
NO_DNSMASQ=0
HIDDEN=0
MAC_FILTER=0
MAC_FILTER_ACCEPT=/etc/hostapd/hostapd.accept
ISOLATE_CLIENTS=0
SHARE_METHOD=nat
IEEE80211N=0
IEEE80211AC=0
HT_CAPAB=[HT40+]
VHT_CAPAB=
DRIVER=nl80211
NO_VIRT=0
COUNTRY=
FREQ_BAND=2.4
NEW_MACADDR=
DAEMONIZE=1
NO_HAVEGED=0
WIFI_IFACE=wlp4s0
INTERNET_IFACE=wlp4s0
SSID=HR-Sophia
PASSPHRASE=12345678
USE_PSK=1
```
Then enable the service 
```
sudo systemctl enable create_ap.service
```

### Where to hook it up
In ```hr install head``` to be able to SSH into the machine in order to start the stack (using the systemd method).  
The password needs to be changed as well as we should consider MAC filtering to avoid unwanted guests in the network. 
Further SSH keys should be preconfigured for every robot machine <-> operator notebook pair
