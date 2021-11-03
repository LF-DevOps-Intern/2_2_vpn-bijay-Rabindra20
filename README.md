1.Setup a VPN server in one vm. You can use openvpn for this purpose.<br/>
  a.You should have two network interface one for wan and another for lan. You should setup vpn server which listens on wan interface and provides lan interfaces subnets ip address to the client which connects using openvpn client.<br/>
  <br/>
  b.You should create certificates files for both server and client to connect to server and export client certificates to the client vm.<br/>
<br/>
2.Create another vm with installing openvpn client and you should create openvpn client connect file(with extension .ovpn) providing the certificates. You should be able to connect tothe vpn server and get ip address from lan subnet that you assigned in first vm.<br/>
<br/>
3.Research on IDS/IPS. There are many applications that provide IDS/IPS service. Find one of the opensource service and install it on the VM1 you created previously. Try to set up IDS which block some of the known vulnerabilities signature.<br/>
