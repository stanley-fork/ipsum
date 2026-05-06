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

Wall of Shame (2026-05-06)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
138.2.102.66|-|10
45.148.10.183|-|9
89.248.167.131|mason.census.shodan.io|9
103.210.22.17|-|9
125.20.210.182|-|9
167.94.146.61|61.146.94.167.censys-scanner.com|9
185.38.148.2|2.148.38.185.baremetal.zare.com|9
213.209.159.56|-|9
216.57.110.81|-|9
2.57.122.192|-|8
2.57.122.238|-|8
14.63.217.28|-|8
45.148.10.152|-|8
45.156.24.224|-|8
66.132.224.79|79.224.132.66.censys-scanner.com|8
66.132.224.87|87.224.132.66.censys-scanner.com|8
66.132.224.224|224.224.132.66.censys-scanner.com|8
66.132.224.227|227.224.132.66.censys-scanner.com|8
80.82.77.139|dojo.census.shodan.io|8
86.54.31.32|hat.census.shodan.io|8
87.251.64.144|-|8
87.251.64.145|-|8
87.251.64.147|-|8
87.251.64.149|-|8
93.174.95.106|battery.census.shodan.io|8
120.241.79.66|-|8
128.203.202.236|azpdcg55r8oy.stretchoid.com|8
129.159.149.21|-|8
144.2.91.96|bbcs-91-96.pub.wingo.ch|8
163.7.1.156|-|8
163.7.9.84|-|8
167.94.146.50|50.146.94.167.censys-scanner.com|8
167.94.146.52|52.146.94.167.censys-scanner.com|8
167.94.146.59|59.146.94.167.censys-scanner.com|8
185.226.197.47|zl-amsc-nl-gp1-wk131a.internet-census.org|8
190.2.135.111|190-2-135-111.hosted-by-worldstream.net|8
193.24.211.95|-|8
199.45.155.96|96.155.45.199.censys-scanner.com|8
213.209.159.158|-|8
2.57.121.25|hosting25.tronicsat.com|7
2.57.122.189|-|7
2.57.122.190|-|7
2.57.122.191|-|7
2.57.122.194|-|7
2.57.122.195|-|7
2.57.122.196|-|7
2.57.122.197|-|7
3.129.187.38|scan.visionheight.com|7
3.130.168.2|scan.visionheight.com|7
5.253.59.171|189809.ip-ptr.tech|7
14.29.198.130|-|7
14.63.196.175|-|7
18.218.118.203|scan.visionheight.com|7
20.15.200.100|azpdcs981gn1.stretchoid.com|7
20.163.60.206|azpdwsvn6zf2.stretchoid.com|7
23.94.213.157|23-94-213-157-host.colocrossing.com|7
36.93.144.67|-|7
43.135.124.152|-|7
45.82.13.133|188189.ip-ptr.tech|7
45.148.10.121|-|7
45.148.10.141|-|7
45.148.10.147|-|7
45.148.10.151|-|7
45.148.10.157|-|7
45.153.34.205|-|7
45.172.152.74|-|7
45.205.1.8|-|7
45.227.254.170|-|7
54.196.240.224|ec2-54-196-240-224.compute-1.amazonaws.com|7
59.12.160.91|-|7
59.22.201.143|-|7
61.155.106.101|-|7
66.132.172.132|132.172.132.66.censys-scanner.com|7
66.132.172.208|208.172.132.66.censys-scanner.com|7
66.132.172.217|217.172.132.66.censys-scanner.com|7
66.132.186.161|161.186.132.66.censys-scanner.com|7
66.132.186.162|162.186.132.66.censys-scanner.com|7
66.132.186.179|179.186.132.66.censys-scanner.com|7
66.132.186.195|195.186.132.66.censys-scanner.com|7
66.132.195.84|84.195.132.66.censys-scanner.com|7
66.132.224.80|80.224.132.66.censys-scanner.com|7
66.132.224.81|81.224.132.66.censys-scanner.com|7
66.132.224.82|82.224.132.66.censys-scanner.com|7
66.132.224.85|85.224.132.66.censys-scanner.com|7
66.132.224.88|88.224.132.66.censys-scanner.com|7
66.132.224.89|89.224.132.66.censys-scanner.com|7
66.132.224.91|91.224.132.66.censys-scanner.com|7
66.132.224.92|92.224.132.66.censys-scanner.com|7
66.132.224.93|93.224.132.66.censys-scanner.com|7
66.132.224.226|226.224.132.66.censys-scanner.com|7
66.132.224.228|228.224.132.66.censys-scanner.com|7
66.132.224.229|229.224.132.66.censys-scanner.com|7
66.132.224.231|231.224.132.66.censys-scanner.com|7
66.132.224.232|232.224.132.66.censys-scanner.com|7
66.132.224.233|233.224.132.66.censys-scanner.com|7
66.240.192.138|census8.shodan.io|7
66.240.236.116|ubtuntu20236116.aspadmin.net|7
71.6.135.131|soda.census.shodan.io|7
71.6.165.200|census12.shodan.io|7
71.6.199.23|einstein.census.shodan.io|7
71.6.232.20|-|7
71.6.232.28|-|7
79.3.96.178|host-79-3-96-178.business.telecomitalia.it|7
79.104.0.82|-|7
80.82.77.33|sky.census.shodan.io|7
80.94.92.186|-|7
85.217.140.48|o347.scanner.modat.io|7
85.217.149.64|o064.scanner.modat.io|7
86.54.31.38|blue2.census.shodan.io|7
88.147.30.59|88-147-30-59.static.eolo.it|7
92.118.39.195|-|7
92.118.39.197|-|7
92.118.39.235|-|7
94.26.106.206|-|7
95.167.225.76|-|7
102.88.137.80|-|7
103.148.100.146|-|7
103.237.144.204|-|7
107.189.24.162|162.24.189.107.static.cloudzy.com|7
109.105.210.62|zl-dfwc-us-gp1-wk108a.internet-census.org|7
110.35.80.116|IP-80-116.napinfo.net|7
117.6.44.221|-|7
123.253.162.254|-|7
129.151.225.209|-|7
146.190.29.141|portscanner-ams3-01.prod.cyberresilience.io|7
147.135.3.156|rane-r.vps.co.ve|7
152.32.162.42|-|7
152.32.209.62|mail3.sexyfreewebcams.com|7
165.245.180.161|-|7
167.94.146.48|48.146.94.167.censys-scanner.com|7
167.94.146.51|51.146.94.167.censys-scanner.com|7
167.94.146.57|57.146.94.167.censys-scanner.com|7
167.94.146.58|58.146.94.167.censys-scanner.com|7
167.94.146.60|60.146.94.167.censys-scanner.com|7
167.94.146.62|62.146.94.167.censys-scanner.com|7
167.94.146.63|63.146.94.167.censys-scanner.com|7
167.99.149.55|portscanner-nyc1-05.prod.cyberresilience.io|7
176.32.193.16|-|7
178.20.210.185|billfish.banhkemcantho.com|7
185.93.89.95|-|7
185.226.197.48|zl-amsc-nl-gp1-wk131b.internet-census.org|7
187.16.96.250|mvx-187-16-96-250.mundivox.com|7
187.210.77.100|customer-187-210-77-100.uninet-ide.com.mx|7
192.34.128.202|-|7
192.42.116.15|this-is-a-tor-exit-node-hviv115.hviv.nl|7
192.42.116.19|this-is-a-tor-exit-node-hviv119.hviv.nl|7
193.32.162.145|-|7
193.32.162.151|-|7
193.46.255.86|-|7
199.45.154.115|115.154.45.199.censys-scanner.com|7
199.45.154.139|139.154.45.199.censys-scanner.com|7
199.45.155.75|75.155.45.199.censys-scanner.com|7
199.45.155.90|90.155.45.199.censys-scanner.com|7
199.45.155.94|94.155.45.199.censys-scanner.com|7
201.76.120.30|30.120.76.201.in-addr.arpa.verointernet.com.br|7
203.145.143.163|-|7
217.154.92.76|ip217-154-92-76.pbiaas.com|7
220.80.223.144|-|7
221.156.126.1|-|7
221.229.218.50|-|7
222.107.156.227|-|7
