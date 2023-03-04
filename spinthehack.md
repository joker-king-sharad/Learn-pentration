chaos.projectdiscovery.io

Subfinder - Amass - crt.sh - all in one-resolving

Subfinder
----------

subfinder -d vk.com -t 100 -v -o /home/kali/Desktop/mrecon/site.com/sub.txt

cat allsub.txt | wc -l   // for count many subdomain in file
**********

Amass
-----------
amass enum -brute -d vk.com -o sub2.txt

virustotal and censys api key required.
**************

crt.sh
-------
https://raw.githubusercontent.com/hannob/tlshelpers/main/getsubdomain

save code crt.sh

chmod +rwx crt.sh

./crt.sh vk.com > sub3.txt

**************

Sorting 
--------

sort sub1.txt sub2.txt sub3.txt | uniq -u > subdomain.txt

***************

Httpx
---------
cat subdomain.txt | httpx -threads 200 | tee -a finalsubdomain.txt

************

Waybackurls
------------

cat subdomain.txt | waybackurls | tee -a waybackurls.txt

*************

Dirsearch 
----------
./dirsearch.py -l /root/Desktop/subdomain.txt -t 100 --plain-text-report /root/Desktop/dir.txt -e html,php,txt -i 200  --full-url

cat dir.txt | grep 403

**********

Nmap
--------
nmap -iL/root/Desktop/finalsubdomain.txt -p- --open -sV -oG /root/Desktop/nmap.txt

********

Gf
---

cat /root/Desktop/waybackurls.txt | gf xss | tee -a /root/Desktop/gfxss.txt

cat /root/Desktop/waybackurls.txt | gf sqli | tee -a /root/Desktop/gfsqli.txt

*******

Subzy | Subdomain Takeover tools
--------

subzy -targets subdomain.txt -concurrency 100 | tee -a subzy.txt
