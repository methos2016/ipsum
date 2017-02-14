![Logo](logo.png)

[![License](https://img.shields.io/badge/license-Public_domain-red.svg)](https://wiki.creativecommons.org/wiki/Public_domain)

About
----

**IPsum** is a threat intelligence feed based on 30+ different publicly available [lists](https://github.com/stamparm/maltrail) of suspicious and/or malicious IP addresses. All lists are automatically retrieved and parsed on a daily (24h) basis and the final result is pushed to this repository. List is made of IP addresses together with a total number of (black)list occurrence (for each). Greater the number, lesser the chance of false positive detection and/or dropping in (inbound) monitored traffic. Also, list is sorted from most (problematic) to least occurent IP addresses.

As an example, to get a fresh and ready-to-deploy auto-ban list of "bad IPs" that appear on at least 3 (black)lists you can run:

```
curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1
```

If you want to try it with `ipset`, you can do the following:

```
sudo su
apt-get -qq install iptables ipset
ipset -q flush ipsum
ipset -q create ipsum hash:net
for ip in $(curl --compressed https://raw.githubusercontent.com/stamparm/ipsum/master/ipsum.txt 2>/dev/null | grep -v "#" | grep -v -E "\s[1-2]$" | cut -f 1); do ipset add ipsum $ip; done
iptables -I INPUT -m set --match-set ipsum src -j DROP
```

In directory [levels](levels) you can find preprocessed raw IP lists based on number of blacklist occurrences (e.g. [levels/3.txt](levels/3.txt) holds IP addresses that can be found on 3 or more blacklists).

Wall of shame (2017-02-14)
----

|IP|Number of (black)lists|
|---|--:|
119.249.54.71|10
89.234.157.254|10
197.231.221.211|10
171.25.193.77|10
176.126.252.12|9
221.194.47.208|9
218.2.108.2|9
176.10.104.243|9
178.217.187.39|9
185.106.22.73|9
110.167.224.182|8
118.255.205.246|8
128.52.128.105|8
171.25.193.131|8
207.244.70.35|8
65.19.167.131|8
191.96.249.48|8
218.83.155.86|8
121.18.238.109|8
218.3.140.74|8
71.6.146.185|8
151.80.42.102|8
121.18.238.114|8
117.252.29.254|8
115.239.248.71|8
185.129.62.63|8
109.163.234.4|8
221.194.44.219|8
113.240.250.156|8
221.194.44.224|8
176.123.27.28|8
121.18.238.98|8
179.233.94.73|8
173.254.216.66|8
163.172.67.180|8
185.38.14.171|8
91.197.235.12|8
37.187.129.166|8
185.110.132.202|8
77.247.181.165|8
181.57.149.131|8
203.162.235.234|8
