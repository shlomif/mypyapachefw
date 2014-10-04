README - My Python Apache Firewall
=====
MyPyApache FW is a log-analyzer written in python.
The script will work on any access log you pipe into it and will create iptables rules to block
client IP addresses which may be malicious to the system.

## Requires
* python iptables
```
pip install --upgrade python-iptables
```
* python GeoIP
```
(fedora) yum install GeoIP GeoIP-dev
(ubuntu) apt-get install python-devel-all libgeoip-devel

pip install --upgrade GeoIP
pip install --upgrade python-geoip-geolite2
```

## Console run
You need to run the script on the console like
```
cat /var/log/apache2/access.log | python mypyfw.py
```
You may wish to write a cronjob to do it every few minutes, using tail, like
```
*/30 * * * * tail -n 500 /var/log/apache2/other_vhosts_access.log | python /opt/mypyapachefw/mypyfw.py


```

## Help
```
Usage: mypyfw.py [options]

Options:
  -h, --help            show this help message and exit
  -f FILE, --file=FILE  write report to FILE, default is /var/log/mypyfw.log
  -i IPPOSITION, --ippos=IPPOSITION
                        adjust IP position, default is 0
  -b FILE, --blacklist=FILE
                        path to blacklist, default values are Hardcoded
  -w FILE, --whitelist=FILE
                        path to Whitelist, default values are Hardcoded
  -t, --try-run          you want a test run
  -g, --geoIP           add GeoIP data to output

```

## Important Notes
The IP split line may have an error.
By default the IP should be located at cell 1 (for combined logging). If you use the standard apache logging than it may be 0.
```
cat /var/log/apache2/access.log | python mypyfw.py -i 0
```

## Current Rules
* Header: curl
* Header: python
* Header: sqlmap
* Header: -
* Header: Wget

## More Information
For more information please follow:
* [https://jsonsecurity.blogspot.de/] My Blog
* [http://jsonsecurity.blogspot.de/feeds/posts/mypyfw] RSS Feed
