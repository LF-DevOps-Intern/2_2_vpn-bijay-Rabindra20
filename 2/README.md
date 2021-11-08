Create another vm with installing openvpn client and you should create an openvpn client connect file(with extension .ovpn) providing the certificates. You should be able to connect to the vpn server and get an ip address from the LAN subnet that you assigned in the first vm.<br/>
steps:<br/>
-ls
![clientvpn](https://user-images.githubusercontent.com/53372486/140671391-d07dad8e-917f-41d2-85bf-8c32597b2f2c.png)
-vi client.ovpn<br/>
-Add add following lines<br/>
client<br/>
tls-client<br/>
ca ca.crt<br/>
cert myclient.crt<br/>
key myclient.key<br/>
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
![client](https://user-images.githubusercontent.com/53372486/140671196-68e9af7d-7e68-4dd6-a23b-c138727dba73.png)
-mkdir /etc/pam.d/<br/>
-sudo vi /etc/pam.d/openvpn
![pam](https://user-images.githubusercontent.com/53372486/140674039-05679c73-c822-4fb2-ad2f-b61b9e0d58d8.png)
-yum apt install -y openvpn<br/>
To connect to openvpn server<br/>
-yum openvpn --config client.ovpn<br/>
-give username and password<br/>
connected<br/>
-ping 192.168.1.68 on ubuntu