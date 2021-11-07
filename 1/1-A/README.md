1.Setup a VPN server in one vm. You can use openvpn for this purpose.<br/>
  a.You should have two network interface one for wan and another for lan. You should setup vpn server which listens on wan interface and provides lan interfaces subnets ip address to the client which connects using openvpn client.<br/>
  steps:<br/>
  -Added two network interface<br/>
  ![briged adapter](https://user-images.githubusercontent.com/53372486/140616900-ae1fe34b-8a2b-4e4f-86e8-115920869992.png)<br/>
![internal network](https://user-images.githubusercontent.com/53372486/140616918-3cfaa8dc-d937-4dff-a542-774a383b545e.png)<br/>
![WM-Screenshots-20211105204035](https://user-images.githubusercontent.com/53372486/140648507-5ef34f05-73b3-4180-96f8-b44180ecb488.png)<br/>
-sudo apt install -y epel-release<br/>
-sudo install openvpn<br/>
![open vpn](https://user-images.githubusercontent.com/53372486/140648524-b37a3b8b-8f8e-4a34-97c5-d97cba86a223.png)<br/>
-wget -O /tmp/easyrsa https://github.com/OpenVPN/easy-rsa-old/archive/2.3.3.tar.gz<br/>
-tar xfz /tmp/easyrsa<br/>
-sudo mkdir /etc/openvpn/easy-rsa<br/>
-sudo cp -rf easy-rsa-old-2.3.3/easy-rsa/2.0/* /etc/openvpn/easy-rsa<br/>
-sudo chown rabindra /etc/openvpn/easy-rsa/<br/>
-cd /etc/openvpn/easy-rsa<br/>
-ls<br/>
![easy](https://user-images.githubusercontent.com/53372486/140648882-b7cd40ec-53b1-4375-ba81-45dc8beb5cdf.png)
-sudo cp /usr/share/doc/openvpn-2.4.11/sample/sample-config-files/server.conf /etc/openvpn/ <br/>
-uncomment these command in /etc/openvpn/server.conf <br/>
 proto tcp<br/>
 proto udp<br/>
 Network topology<br/>
 topology subnet //To give client address<br/>
 server 192.168.10.1 255.255.255.0<br/>
 Push routes to the client to allow it to reach each other private subnets behind the server<br/>
 push "route 192.168.10.0 255.255.255.0"<br/>
 DNS servers<br/>
 push "dhcp-option DNS 8.8.8.8"<br/>
 push "dhcp-option DNS 8.8.4.4"<br/>
 To allow different clients to see each other 
 client-to-client<br/>
 For extra security beyond that provided by SSL/TLS, create an "HMAC firewall" (block DoS attack and UDP port flooding)<br/>
 tls-crypt myvpn.tlsauth <br/>
 For non-windows system
 user nobody<br/>
 group nobody<br/>
 To append log at specific location<br/>
 log     /var/log/openvpn.log<br/>
 <br/>
