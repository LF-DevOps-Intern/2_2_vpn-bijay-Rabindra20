b.You should create certificates files for both server and client to connect to server and export client certificates to the client vm.<br/>
steps:<br/>
Creating certificates files for both server and client , connect to server<br/>
-sudo mkdir /etc/openvpn/easy-rsa/keys<br/>
-sudo vi /etc/openvpn/easy-rsa/vars<br/>
-change this<br/>
export KEY_COUNTRY="NP"<br/>
export KEY_PROVINCE="BAGMATI"<br/>
export KEY_CITY="Kathmandu"<br/>
export KEY_ORG="LT"<br/>
export KEY_EMAIL="root@example.com"<br/>
export KEY_EMAIL=root@example.com<br/>
68export KEY_CN=192.168.1.68<br/>
export KEY_NAME="EasyRSA"<br/>
export KEY_OU=LT<br/>
![vars](https://user-images.githubusercontent.com/53372486/<br/>140667600-8b32b4dd-3b1d-47fc-9be1-4b377b0017cd.png)<br/>
-cd /etc/openvpn/easy-rsa<br/>
./easyrsa build-ca<br/>
![CA](https://user-images.githubusercontent.com/53372486/140667696-648dc060-dee2-498c-a8d9-90874d6775b2.png)<br/>
cd /etc/openvpn/easy-rsa<br/>
./build-key client<br/>
 ./build-key-server server <br/>
 ./build-dh <br/>
 cd /etc/openvpn/easy-rsa/keys<br/>
 ![keys](https://user-images.githubusercontent.com/53372486/140669021-f04936b2-4b29-4611-8766-1919efe3b74b.png)<br/>
-sudo cp dh2048.pem ca.crt server.crt server.key /etc/openvpn<br/>
-cd /etc/openvpn/easy-rsa<br/>
./build-key client<br/>
cp /etc/openvpn/easy-rsa/openssl-1.0.0.cnf /etc/openvpn/easy-rsa/openssl.cnf
![openssl](https://user-images.githubusercontent.com/53372486/140667895-7309dc33-8256-447a-a541-a03c4d5bc91c.png)<br/>
-sudo firewall-cmd --zone=external --add-service <br/>-openvpn --permanent<br/>
-sudo firewall-cmd --permanent --add-masquerade<br/>
-sudo firewall-cmd --query-masquerade<br/>
-yes<br/>
-sudo firewall-cmd --permanent --direct --passthrough <br/>-ipv4 -t nat -A POSTROUTING -s 192.168.10.1 -o $SHARK -j MASQUERADE<br/>
-sudo firewall-cmd --reload<br/>
-sudo systemctl restart network<br/>
sudo systemctl -f enable openvpn@server.service<br/>
sudo systemctl start openvpn@server.service<br/>
sudo systemctl status openvpn@server.service<br/>
