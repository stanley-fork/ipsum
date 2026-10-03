![Logo](https://i.imgur.com/PyKLAe7.png)

[![License](https://img.shields.io/badge/license-The_Unlicense-red.svg)](https://unlicense.org/)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses, like [IPnoise](https://ipnoise.sekuripy.hr/). All lists are automatically retrieved and parsed on a daily (every 24 hours) basis and the final result is pushed to this repository. The feed contains IP addresses plus an occurrence count (how many source lists each IP appears on). Higher counts generally mean higher confidence and fewer false positives when blocking inbound traffic. Also, list is sorted by occurrence count (highest to lowest).

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

Wall of Shame (2026-10-03)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
45.43.60.98|paifrtoyibbdx.com|9
2.57.122.53|-|8
2.57.122.238|-|8
3.129.187.38|scan.visionheight.com|8
37.120.213.13|-|8
65.49.1.202|-|8
65.49.1.222|-|8
66.132.172.208|208.172.132.66.censys-scanner.com|8
66.132.186.167|167.186.132.66.censys-scanner.com|8
66.132.186.172|172.186.132.66.censys-scanner.com|8
77.90.185.20|-|8
85.217.149.34|o035.scanner.modat.io|8
85.217.149.40|o040.scanner.modat.io|8
85.217.149.43|o043.scanner.modat.io|8
85.217.149.55|o055.scanner.modat.io|8
85.217.149.57|o057.scanner.modat.io|8
94.154.43.69|-|8
94.154.43.223|-|8
103.146.23.23|-|8
199.45.154.120|120.154.45.199.censys-scanner.com|8
2.26.64.195|-|7
20.115.88.250|azpdessxrydp.stretchoid.com|7
39.109.116.214|-|7
40.119.27.225|-|7
45.78.224.198|-|7
45.91.64.7|scan.f6.security|7
45.120.216.232|-|7
45.148.10.61|-|7
45.148.10.152|-|7
45.148.10.157|-|7
45.156.129.60|sh-chi-us-gp1-wk101a.internet-census.org|7
45.156.129.66|sh-chi-us-gp1-wk102b.internet-census.org|7
45.156.129.85|sh-chi-us-gp1-wk135a.internet-census.org|7
45.156.129.87|sh-chi-us-gp1-wk135c.internet-census.org|7
45.156.129.95|sh-chi-us-gp1-wk137a.internet-census.org|7
45.172.152.74|-|7
45.198.224.34|-|7
45.198.224.125|-|7
46.105.31.171|vps-a1b911bb.vps.ovh.net|7
64.62.156.10|-|7
64.62.156.24|-|7
64.62.156.52|-|7
64.62.156.66|-|7
64.62.156.94|-|7
64.62.156.122|-|7
64.62.156.192|-|7
64.62.197.48|-|7
64.62.197.62|-|7
64.62.197.92|-|7
64.62.197.107|-|7
64.62.197.182|-|7
64.62.197.197|-|7
64.62.197.227|-|7
65.49.1.94|-|7
65.49.1.122|-|7
65.49.1.132|-|7
65.49.1.142|-|7
65.49.1.152|-|7
65.49.1.192|-|7
66.132.172.37|37.172.132.66.censys-scanner.com|7
66.132.172.38|38.172.132.66.censys-scanner.com|7
66.132.172.39|39.172.132.66.censys-scanner.com|7
66.132.172.40|40.172.132.66.censys-scanner.com|7
66.132.172.44|44.172.132.66.censys-scanner.com|7
66.132.172.46|46.172.132.66.censys-scanner.com|7
66.132.172.128|128.172.132.66.censys-scanner.com|7
66.132.172.133|133.172.132.66.censys-scanner.com|7
66.132.172.137|137.172.132.66.censys-scanner.com|7
66.132.172.138|138.172.132.66.censys-scanner.com|7
66.132.172.140|140.172.132.66.censys-scanner.com|7
66.132.172.141|141.172.132.66.censys-scanner.com|7
66.132.172.143|143.172.132.66.censys-scanner.com|7
66.132.172.180|180.172.132.66.censys-scanner.com|7
66.132.172.189|189.172.132.66.censys-scanner.com|7
66.132.172.193|193.172.132.66.censys-scanner.com|7
66.132.172.196|196.172.132.66.censys-scanner.com|7
66.132.172.200|200.172.132.66.censys-scanner.com|7
66.132.172.201|201.172.132.66.censys-scanner.com|7
66.132.172.212|212.172.132.66.censys-scanner.com|7
66.132.172.216|216.172.132.66.censys-scanner.com|7
66.132.186.163|163.186.132.66.censys-scanner.com|7
66.132.186.168|168.186.132.66.censys-scanner.com|7
66.132.186.176|176.186.132.66.censys-scanner.com|7
66.132.186.179|179.186.132.66.censys-scanner.com|7
66.132.186.180|180.186.132.66.censys-scanner.com|7
66.132.186.182|182.186.132.66.censys-scanner.com|7
66.132.186.187|187.186.132.66.censys-scanner.com|7
66.132.186.198|198.186.132.66.censys-scanner.com|7
66.132.186.203|203.186.132.66.censys-scanner.com|7
66.132.186.205|205.186.132.66.censys-scanner.com|7
66.132.195.38|38.195.132.66.censys-scanner.com|7
66.132.195.48|48.195.132.66.censys-scanner.com|7
66.132.195.56|56.195.132.66.censys-scanner.com|7
66.132.195.62|62.195.132.66.censys-scanner.com|7
66.132.195.75|75.195.132.66.censys-scanner.com|7
66.132.195.97|97.195.132.66.censys-scanner.com|7
66.132.195.99|99.195.132.66.censys-scanner.com|7
66.132.195.102|102.195.132.66.censys-scanner.com|7
66.132.195.103|103.195.132.66.censys-scanner.com|7
66.132.195.105|105.195.132.66.censys-scanner.com|7
66.132.195.106|106.195.132.66.censys-scanner.com|7
66.132.195.125|125.195.132.66.censys-scanner.com|7
66.132.195.126|126.195.132.66.censys-scanner.com|7
66.132.224.238|238.224.132.66.censys-scanner.com|7
71.6.134.231|-|7
71.6.134.237|server10-debian11134237.aspadmin.net|7
71.6.135.131|soda.census.shodan.io|7
71.6.199.23|einstein.census.shodan.io|7
80.82.77.33|sky.census.shodan.io|7
80.82.77.139|dojo.census.shodan.io|7
81.19.216.97|sw4-r6.8.6-evo.nl.as25369.net|7
85.217.149.0|o001.scanner.modat.io|7
85.217.149.5|o006.scanner.modat.io|7
85.217.149.7|o008.scanner.modat.io|7
85.217.149.12|o013.scanner.modat.io|7
85.217.149.13|o014.scanner.modat.io|7
85.217.149.16|o017.scanner.modat.io|7
85.217.149.17|o018.scanner.modat.io|7
85.217.149.21|o022.scanner.modat.io|7
85.217.149.25|o026.scanner.modat.io|7
85.217.149.26|o027.scanner.modat.io|7
85.217.149.28|o029.scanner.modat.io|7
85.217.149.31|o032.scanner.modat.io|7
85.217.149.35|o036.scanner.modat.io|7
85.217.149.36|o037.scanner.modat.io|7
85.217.149.41|o041.scanner.modat.io|7
85.217.149.42|o042.scanner.modat.io|7
85.217.149.56|o056.scanner.modat.io|7
86.54.31.32|hat.census.shodan.io|7
89.21.67.140|89-21-67-140.infrawat.ch|7
94.154.43.57|-|7
103.46.186.85|-|7
103.237.144.204|-|7
124.158.13.141|-|7
125.21.59.218|-|7
138.226.239.233|-|7
138.226.239.234|-|7
147.185.132.33|-|7
147.185.132.49|-|7
147.185.132.67|-|7
147.185.132.153|-|7
147.185.132.180|-|7
147.185.132.204|-|7
160.187.174.22|-|7
167.94.146.48|48.146.94.167.censys-scanner.com|7
167.94.146.49|49.146.94.167.censys-scanner.com|7
167.94.146.50|50.146.94.167.censys-scanner.com|7
167.94.146.54|54.146.94.167.censys-scanner.com|7
167.94.146.55|55.146.94.167.censys-scanner.com|7
167.94.146.56|56.146.94.167.censys-scanner.com|7
167.94.146.58|58.146.94.167.censys-scanner.com|7
167.94.146.60|60.146.94.167.censys-scanner.com|7
167.94.146.61|61.146.94.167.censys-scanner.com|7
167.94.146.63|63.146.94.167.censys-scanner.com|7
184.105.247.195|-|7
185.177.72.24|-|7
185.226.197.42|zl-amsc-nl-gp1-wk130a.internet-census.org|7
185.242.226.17|security.criminalip.com|7
193.24.211.218|-|7
193.47.62.69|-|7
195.178.110.228|-|7
195.184.76.134|pittman.probe.onyphe.net|7
196.189.236.67|-|7
198.235.24.52|-|7
198.235.24.113|-|7
198.235.24.119|-|7
198.235.24.186|-|7
198.235.24.254|-|7
199.45.154.55|55.154.45.199.censys-scanner.com|7
199.45.154.56|56.154.45.199.censys-scanner.com|7
199.45.154.57|57.154.45.199.censys-scanner.com|7
199.45.154.59|59.154.45.199.censys-scanner.com|7
199.45.154.113|113.154.45.199.censys-scanner.com|7
199.45.154.116|116.154.45.199.censys-scanner.com|7
199.45.155.41|41.155.45.199.censys-scanner.com|7
203.150.107.244|244.107.150.203.sta.inet.co.th|7
205.210.31.72|-|7
205.210.31.83|-|7
205.210.31.108|-|7
205.210.31.110|-|7
205.210.31.238|-|7
210.114.22.126|-|7
211.253.9.49|-|7
216.180.246.19|crawler019.deepfield.net|7
216.226.76.30|-|7
223.197.186.7|223-197-186-7.static.imsbiz.com|7
