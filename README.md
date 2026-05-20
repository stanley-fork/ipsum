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

Wall of Shame (2026-05-20)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
152.32.132.28|-|11
213.209.159.56|-|11
190.2.135.111|190-2-135-111.hosted-by-worldstream.net|10
2.57.121.112|dns112.personaliseplus.com|9
152.32.226.205|test1236.asia|9
220.80.223.144|-|9
2.57.121.25|hosting25.tronicsat.com|8
2.57.122.238|-|8
66.240.192.138|census8.shodan.io|8
71.6.135.131|soda.census.shodan.io|8
71.6.199.23|einstein.census.shodan.io|8
80.82.77.139|dojo.census.shodan.io|8
89.185.81.112|153823.ip-ptr.tech|8
93.174.95.106|battery.census.shodan.io|8
125.20.210.182|-|8
130.110.250.40|-|8
167.94.146.52|52.146.94.167.censys-scanner.com|8
167.94.146.54|54.146.94.167.censys-scanner.com|8
167.94.146.58|58.146.94.167.censys-scanner.com|8
167.94.146.59|59.146.94.167.censys-scanner.com|8
178.17.53.215|-|8
185.100.212.141|-|8
193.32.162.145|-|8
213.209.159.158|-|8
216.194.172.68|ded2288.inmotionhosting.com|8
20.224.168.82|-|7
34.72.208.101|101.208.72.34.bc.googleusercontent.com|7
34.175.118.185|185.118.175.34.bc.googleusercontent.com|7
36.62.94.189|-|7
37.120.213.13|-|7
38.12.31.247|-|7
38.137.11.14|-|7
41.86.34.139|-|7
43.128.105.214|-|7
43.133.148.170|-|7
43.134.13.135|-|7
43.134.37.25|-|7
43.134.67.7|-|7
43.134.102.240|-|7
43.134.124.193|-|7
43.134.174.204|-|7
43.152.72.38|-|7
43.153.208.208|-|7
43.160.206.186|-|7
43.163.86.65|-|7
43.163.92.224|-|7
43.173.67.129|-|7
43.173.84.162|-|7
43.228.112.254|-|7
45.33.12.122|45-33-12-122.ip.linodeusercontent.com|7
45.82.13.133|188189.ip-ptr.tech|7
45.91.64.6|scan.f6.security|7
45.148.10.121|-|7
45.148.10.141|-|7
45.148.10.151|-|7
45.148.10.152|-|7
45.148.10.183|-|7
45.148.10.240|-|7
45.227.254.170|-|7
46.161.50.109|scan.f6.security|7
49.51.73.28|-|7
49.51.233.105|-|7
50.84.211.204|syn-050-084-211-204.biz.spectrum.com|7
59.12.160.91|-|7
59.17.95.129|-|7
61.76.112.4|-|7
66.132.172.138|138.172.132.66.censys-scanner.com|7
66.132.172.178|178.172.132.66.censys-scanner.com|7
66.132.186.200|200.186.132.66.censys-scanner.com|7
66.132.195.52|52.195.132.66.censys-scanner.com|7
66.132.195.62|62.195.132.66.censys-scanner.com|7
66.132.195.83|83.195.132.66.censys-scanner.com|7
69.6.222.198|vps-14704481.gebello.com.br|7
70.65.44.183|S01061033bfa5ff8b.rd.shawcable.net|7
71.6.165.200|census12.shodan.io|7
80.82.77.33|sky.census.shodan.io|7
80.94.92.171|-|7
80.94.92.182|-|7
81.9.145.130|cm-81-9-145-130.telecable.es|7
81.28.167.30|-|7
81.161.239.16|-|7
83.248.155.53|c83-248-155-53.bredband.tele2.se|7
86.54.31.32|hat.census.shodan.io|7
86.54.31.38|blue2.census.shodan.io|7
86.54.31.40|blue.census.shodan.io|7
87.251.64.145|-|7
87.251.64.149|-|7
91.210.169.154|925871-ca42523.tmweb.ru|7
92.118.39.236|-|7
94.102.49.193|cloud.census.shodan.io|7
101.47.158.137|-|7
103.167.89.222|-|7
103.182.132.154|-|7
103.210.22.17|-|7
107.175.33.240|107-175-33-240-host.colocrossing.com|7
109.49.23.192|a109-49-23-192.cpe.netcabo.pt|7
110.14.190.217|-|7
117.164.191.217|localhost|7
118.45.101.159|-|7
120.241.79.66|-|7
122.114.69.235|-|7
123.253.162.254|-|7
124.156.193.46|-|7
125.91.33.72|-|7
129.226.93.131|-|7
139.59.6.237|-|7
144.2.91.96|bbcs-91-96.pub.wingo.ch|7
144.31.224.193|-|7
150.109.13.44|-|7
150.109.93.60|-|7
152.32.172.177|-|7
152.200.205.180|-|7
161.132.38.88|-|7
164.164.197.148|-|7
167.94.146.51|51.146.94.167.censys-scanner.com|7
167.94.146.53|53.146.94.167.censys-scanner.com|7
167.94.146.56|56.146.94.167.censys-scanner.com|7
167.94.146.57|57.146.94.167.censys-scanner.com|7
170.106.101.241|-|7
178.20.210.186|tetragonolobus.banhkemcantho.com|7
181.104.43.225|host225.181-104-43.telecom.net.ar|7
185.113.10.178|-|7
185.221.216.189|-|7
187.110.238.50|187.110.238.50.mobtelecom.com.br|7
187.212.47.18|dsl-18-47-212-187-dynamic.prod-infinitum.com.mx|7
189.165.70.195|dsl-195-70-165-189-dynamic.prod-infinitum.com.mx|7
191.84.224.210|-|7
192.42.116.19|this-is-a-tor-exit-node-hviv119.hviv.nl|7
196.216.81.126|-|7
199.21.150.105|difgo4.com|7
199.45.154.117|117.154.45.199.censys-scanner.com|7
199.45.155.92|92.155.45.199.censys-scanner.com|7
199.45.155.110|110.155.45.199.censys-scanner.com|7
201.184.50.251|static-adsl201-184-50-251.une.net.co|7
202.70.82.95|-|7
208.109.53.78|78.53.109.208.host.secureserver.net|7
211.20.14.156|211-20-14-156.hinet-ip.hinet.net|7
218.22.187.66|-|7
218.250.28.248|n218250028248.netvigator.com|7
220.247.224.226|-|7
