# AcessPoint integration while not blocking the network card

1. Tool  
[create_ap](https://github.com/oblique/create_ap)
2. Dependencies
```
sudo apt-get install util-linux procps hostapd iproute2 iw haveged dnsmasq iptables openssh-server
```
3. Build & Install  
```
cd /usr/local/bin # or somewhere else and put it in $PATH
git clone https://github.com/oblique/create_ap
cd create_ap
sudo make install
```
4. Run   
Form Bash:
```
sudo create_ap wlan0 wlan0 HR-SophiaX AMysteriousGenericPassPhraseLike'TheForgeIsComing'
```

### Where to hook it up
In ```hr install head``` to be able to SSH into the machine in order to start the stack.
The systemd service doesnt propperly work (keeps creating virtual interfaces), so we'd rather want to put the bash line above into /etc/rc.local.
The password needs to be changed as well as we should consider MAC filtering to avoid unwanted guests in the network. 
Further SSH keys should be preconfigured for every robot machine <-> operator notebook pair to omit credentials when sshing onto the machine.
