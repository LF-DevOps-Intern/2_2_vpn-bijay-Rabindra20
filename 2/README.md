Create another vm with installing openvpn client and you should create an openvpn client connect file(with extension .ovpn) providing the certificates. You should be able to connect to the vpn server and get an ip address from the LAN subnet that you assigned in the first vm.<br/>
steps:<br/>
-sudo nano client.ovpn<br/>
-Add add following lines<br/>
client<br/>
tls-client<br/>
ca ca.crt<br/>
cert client.crt<br/>
key client.key<br/>
tls-crypt myvpn.tlsauth<br/>
remote-cert-eku "TLS Web Server Authentication"<br/>
proto tcp<br/>
remote 192.168.1.68 1194 udp<br/>
dev tun<br/>
topology subnet<br/>
pull<br/>
user nobody<br/>
group nobody<br/>
auth-user-pass<br/>
-mkdir /etc/pam.d/<br/>
-sudo vi /etc/pam.d/openvpn
-sudo apt install -y openvpn
To connect to openvpn server
-sudo openvpn --config client.ovpn
