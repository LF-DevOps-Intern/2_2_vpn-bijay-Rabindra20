1.Setup a VPN server in one vm. You can use openvpn for this purpose.<br/>
  a.You should have two network interface one for wan and another for lan. You should setup vpn server which listens on wan interface and provides lan interfaces subnets ip address to the client which connects using openvpn client.<br/>
  steps:<br/>
  -Added two network interface