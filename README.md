![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-The_Unlicense-red.svg)](https://unlicense.org/)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (every 24 hours) basis and the final result is pushed to this repository. The feed contains IP addresses plus an occurrence count (how many source lists each IP appears on). Higher counts generally mean higher confidence and fewer false positives when blocking inbound traffic. Also, list is sorted by occurrence count (highest to lowest).

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl -fsSL https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "^#" | grep -Ev '[[:space:]]([12])$' | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo -i
apt-get update && apt-get install -y iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:ip
for ip in $(curl https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -Ev '[[:space:]]([12])$' | cut -f 1); do ipset add ipsum $ip; done
iptables -D INPUT -m set --match-set ipsum src -j DROP 2>/dev/null
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of Shame (2026-04-28)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
45.142.193.135|-|10
80.82.77.33|sky.census.shodan.io|9
163.7.9.84|-|9
185.38.148.2|2.148.38.185.baremetal.zare.com|9
190.2.135.111|190-2-135-111.hosted-by-worldstream.net|9
213.209.159.159|-|9
2.57.121.112|dns112.personaliseplus.com|8
2.57.122.194|-|8
2.57.122.238|-|8
43.135.124.152|-|8
45.148.10.151|-|8
45.148.10.152|-|8
45.148.10.157|-|8
45.148.10.183|-|8
45.205.1.8|-|8
66.132.224.93|93.224.132.66.censys-scanner.com|8
80.82.77.139|dojo.census.shodan.io|8
86.54.31.34|wine.census.shodan.io|8
87.251.64.149|-|8
88.149.145.190|88-149-145-190.static.eolo.it|8
89.248.167.131|mason.census.shodan.io|8
93.174.95.106|battery.census.shodan.io|8
103.210.22.17|-|8
109.248.170.188|-|8
125.20.210.182|-|8
129.159.149.21|-|8
138.2.102.66|-|8
144.2.91.96|bbcs-91-96.pub.wingo.ch|8
163.7.1.156|-|8
167.94.146.52|52.146.94.167.censys-scanner.com|8
167.94.146.54|54.146.94.167.censys-scanner.com|8
193.24.211.95|-|8
199.45.155.94|94.155.45.199.censys-scanner.com|8
2.57.121.25|hosting25.tronicsat.com|7
2.57.122.189|-|7
2.57.122.191|-|7
2.57.122.192|-|7
2.57.122.193|-|7
2.57.122.195|-|7
2.57.122.196|-|7
2.57.122.197|-|7
5.253.59.171|189809.ip-ptr.tech|7
5.255.122.180|-|7
14.63.196.175|-|7
14.63.217.28|-|7
18.218.118.203|scan.visionheight.com|7
27.79.43.239|localhost|7
27.111.32.174|-|7
36.91.166.34|-|7
45.148.10.121|-|7
45.148.10.147|-|7
45.153.34.205|-|7
45.172.152.74|-|7
45.227.254.170|-|7
45.232.73.84|-|7
59.12.160.91|-|7
61.145.163.164|-|7
61.182.2.26|-|7
66.94.124.248|vmi3248771.contaboserver.net|7
66.132.172.103|103.172.132.66.censys-scanner.com|7
66.132.172.131|131.172.132.66.censys-scanner.com|7
66.132.172.136|136.172.132.66.censys-scanner.com|7
66.132.172.139|139.172.132.66.censys-scanner.com|7
66.132.172.142|142.172.132.66.censys-scanner.com|7
66.132.172.186|186.172.132.66.censys-scanner.com|7
66.132.172.188|188.172.132.66.censys-scanner.com|7
66.132.172.221|221.172.132.66.censys-scanner.com|7
66.132.195.76|76.195.132.66.censys-scanner.com|7
66.132.195.87|87.195.132.66.censys-scanner.com|7
66.132.224.79|79.224.132.66.censys-scanner.com|7
66.132.224.80|80.224.132.66.censys-scanner.com|7
66.132.224.86|86.224.132.66.censys-scanner.com|7
66.132.224.91|91.224.132.66.censys-scanner.com|7
66.132.224.223|223.224.132.66.censys-scanner.com|7
66.132.224.225|225.224.132.66.censys-scanner.com|7
66.132.224.229|229.224.132.66.censys-scanner.com|7
66.132.224.235|235.224.132.66.censys-scanner.com|7
66.240.236.116|ubtuntu20236116.aspadmin.net|7
69.164.217.74|69-164-217-74.ip.linodeusercontent.com|7
71.6.135.131|soda.census.shodan.io|7
71.6.158.166|ninja.census.shodan.io|7
71.6.165.200|census12.shodan.io|7
72.14.178.148|72-14-178-148.ip.linodeusercontent.com|7
79.3.96.178|host-79-3-96-178.business.telecomitalia.it|7
80.94.92.182|-|7
86.54.31.38|blue2.census.shodan.io|7
86.54.31.40|blue.census.shodan.io|7
87.251.64.144|-|7
87.251.64.145|-|7
87.251.64.147|-|7
88.147.30.59|88-147-30-59.static.eolo.it|7
89.190.156.34|smtp-3.goinbox.in|7
91.144.21.210|-|7
92.118.39.195|-|7
92.118.39.235|-|7
94.26.106.206|-|7
94.102.49.193|cloud.census.shodan.io|7
95.167.225.76|-|7
103.161.170.12|-|7
110.35.80.116|IP-80-116.napinfo.net|7
113.193.234.210|-|7
117.6.44.221|-|7
119.96.157.188|-|7
119.96.173.169|-|7
120.241.79.66|-|7
122.168.194.41|abts-mp-static-041.194.168.122.airtelbroadband.in|7
125.21.59.218|-|7
134.209.235.25|portscanner-fra1-03.prod.cyberresilience.io|7
152.32.162.42|-|7
152.32.225.11|mail4.makenzikirol.com|7
167.94.146.48|48.146.94.167.censys-scanner.com|7
167.94.146.49|49.146.94.167.censys-scanner.com|7
167.94.146.50|50.146.94.167.censys-scanner.com|7
167.94.146.57|57.146.94.167.censys-scanner.com|7
167.94.146.58|58.146.94.167.censys-scanner.com|7
167.94.146.59|59.146.94.167.censys-scanner.com|7
167.94.146.61|61.146.94.167.censys-scanner.com|7
167.94.146.62|62.146.94.167.censys-scanner.com|7
177.229.197.38|customer-MCA-TGZ-197-38.megared.net.mx|7
178.49.109.109|l49-109-109.novotelecom.ru|7
183.98.76.106|-|7
187.16.96.250|mvx-187-16-96-250.mundivox.com|7
187.210.77.100|customer-187-210-77-100.uninet-ide.com.mx|7
193.32.162.151|-|7
193.46.255.86|hostingmailto239.statics.servermail.org|7
199.45.155.67|67.155.45.199.censys-scanner.com|7
199.45.155.73|73.155.45.199.censys-scanner.com|7
199.45.155.75|75.155.45.199.censys-scanner.com|7
199.45.155.83|83.155.45.199.censys-scanner.com|7
201.17.133.138|c911858a.virtua.com.br|7
211.20.14.156|211-20-14-156.hinet-ip.hinet.net|7
216.57.110.81|-|7
218.145.181.48|-|7
221.156.126.1|-|7
221.161.235.168|-|7
222.107.156.227|-|7
