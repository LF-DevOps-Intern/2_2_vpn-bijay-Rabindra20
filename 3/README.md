3.Research on IDS/IPS. There are many applications that provide IDS/IPS service. Find one of the opensource service and install it on the VM1 you created previously. Try to set up IDS which block some of the known vulnerabilities signature.<br/>
steps:<br/>
To install suricata <br/>
-yum install epel-release yum-plugin-copr<br/>
-yum copr enable @oisf/suricata-6.0<br/>
-yum install suricata<br/>
![install suricata](https://user-images.githubusercontent.com/53372486/140675181-ee3c84c4-5b69-4395-ab94-757f2d71a6d5.png)<br/>
Edit HOME_NET<br/>
vi /etc/suricata/suricata.yaml<br/>
af-packet:<br/>
    - interface: eth0<br/>
      cluster-id: 99<br/>
      cluster-type: cluster_flow<br/>
      defrag: yes<br/>
      use-mmap: yes<br/>
      tpacket-v3: yes<br/>

![edit home](https://user-images.githubusercontent.com/53372486/140676867-827df825-646f-4511-bf14-45cd1ad1985a.png)
-vim /usr/share/suricata/rules<br/>
![rules](https://user-images.githubusercontent.com/53372486/140677631-73318c49-90de-40e5-903c-2eafbd1487c6.png)
-alert http any any -> any any (msg:"Do not read gossip during work";<br/>
content:"Scarlett"; nocase; classtype:policy-violation; sid:1; rev:1;)<br/>
![test rules](https://user-images.githubusercontent.com/53372486/140677598-72da3dc4-91a1-49c2-8b25-061971e3d373.png)

Add rules name in suricata.yaml<br/>
-vi /usr/share/suricata/rules/suricata.yaml<br/>
Find rule-files<br/>
And under it write <br/>
-/usr/share/suricata/rules/test.rules<br/>
fire Suricata in PCAP live mode by executing<br/>
-suricata -D -c /etc/suricata/suricata.yaml -i eth0
-suricata-update<br/>
-tail -f /var/log/suricata/fast.log<br/>