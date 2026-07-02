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

Wall of Shame (2026-07-02)
----

|IP|DNS lookup|Number of (black)lists|
|---|---|--:|
80.82.77.139|dojo.census.shodan.io|9
118.26.111.107|-|9
71.6.135.131|soda.census.shodan.io|8
125.20.210.182|-|8
167.94.146.57|57.146.94.167.censys-scanner.com|8
167.94.146.62|62.146.94.167.censys-scanner.com|8
185.242.3.195|-|8
14.103.10.167|-|7
34.178.21.247|247.21.178.34.bc.googleusercontent.com|7
38.191.248.41|-|7
45.148.10.152|-|7
65.49.1.232|-|7
66.132.172.102|102.172.132.66.censys-scanner.com|7
66.132.172.213|213.172.132.66.censys-scanner.com|7
66.132.186.175|175.186.132.66.censys-scanner.com|7
66.132.195.65|65.195.132.66.censys-scanner.com|7
66.132.195.69|69.195.132.66.censys-scanner.com|7
66.132.195.84|84.195.132.66.censys-scanner.com|7
66.132.195.87|87.195.132.66.censys-scanner.com|7
66.132.195.96|96.195.132.66.censys-scanner.com|7
66.132.224.84|84.224.132.66.censys-scanner.com|7
66.132.224.86|86.224.132.66.censys-scanner.com|7
66.132.224.227|227.224.132.66.censys-scanner.com|7
66.132.224.229|229.224.132.66.censys-scanner.com|7
71.6.199.65|-|7
71.6.232.23|-|7
79.72.57.232|-|7
79.76.58.113|-|7
80.82.77.33|sky.census.shodan.io|7
85.217.140.26|o325.scanner.modat.io|7
86.54.31.34|wine.census.shodan.io|7
90.84.168.147|ecs-90-84-168-147.reverse.open-telekom-cloud.com|7
92.118.39.71|-|7
93.89.113.60|93.89.113.60.ip.vitnett.no|7
95.215.0.144|scan.f6.security|7
101.47.15.119|-|7
106.75.185.227|ohkknr.shop|7
148.66.142.9|9.142.66.148.host.secureserver.net|7
160.187.174.22|-|7
167.94.146.48|48.146.94.167.censys-scanner.com|7
167.94.146.52|52.146.94.167.censys-scanner.com|7
167.94.146.53|53.146.94.167.censys-scanner.com|7
167.94.146.54|54.146.94.167.censys-scanner.com|7
167.94.146.60|60.146.94.167.censys-scanner.com|7
167.94.146.61|61.146.94.167.censys-scanner.com|7
176.53.159.197|-|7
176.53.159.198|-|7
182.19.35.57|-|7
185.65.202.199|-|7
193.46.255.86|-|7
195.178.110.228|-|7
195.178.110.232|-|7
199.45.155.67|67.155.45.199.censys-scanner.com|7
199.45.155.68|68.155.45.199.censys-scanner.com|7
222.102.21.104|-|7
