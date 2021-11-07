b.You should create certificates files for both server and client to connect to server and export client certificates to the client vm.<br/>
steps:<br/>
Creating certificates files for both server and client , connect to server<br/>
-sudo mkdir /etc/openvpn/easy-rsa/keys<br/>
-sudo vi /etc/openvpn/easy-rsa/vars<br/>
-change this
export KEY_COUNTRY="NP"
export KEY_PROVINCE="KTM"
export KEY_CITY="Kathmandu"
export KEY_ORG="LT"
export KEY_EMAIL="root@example.com"
export KEY_EMAIL=root@example.com
68export KEY_CN=192.168.1.68
export KEY_NAME="EasyRSA"
export KEY_OU=LT
