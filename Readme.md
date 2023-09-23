Part (1):  Subdomain Takeover Recon :-

 1- subfinder :-

subfinder -dL domains.txt -o subfinder.txt subfinder -d inholland.nl -o subfinder.txt

2 - amass :-
 
amass enum -passive -norecursive -noalts -df domains.txt -o amass.txt

3 - assetfinder :-

- cat domains.txt | assetfinder -subs-only > asset.txt 

 ## Then merging all subdomains into one file :-  (all-subs.txt) :-

cat amass.txt subfinder.txt asset.txt | anew all-subs.txt

##(Get live-subs.txt):-

 - cat all-subs.txt | httpx -o live-subs.txt

Part (2): Subdomain Takeover Testing :-

1- Nuclei :-

nuclei -t /root/nuclei-templates/takeovers/ -l live-subs.txt

2- Subzy :-  

-  subzy run --targets live-subs.txt --hide_falis

- subzy run --target test.google.com

- subzy run --target test.google.com,https://test.yahoo.com

## أحيانا ال Tools دي بتطلع False positives عشان كدة حتحتاج تتأكد Manually عن طريق إنك تزور ال Subdomains و تعمل check على ال DNS و ال CNAME Records بتاعتها عن طريق ال Tools دي مثلا :- dig,dnsmap,nslookup

 ## Useful Writeups and Disclosured Reports :-

https://github.com/LukaSikic/subzy
https://github.com/EdOverflow/can-i-take-over-xyz
https://amitp200.medium.com/subdomain-takeover-easy-win-win-6034bb4147f3 https://www.geeksforgeeks.org/subzy-subdomain-takeover-vulnerability-checker-tool/
https://smaranchand.com.np/2019/12/subdomain-takeover-via-pantheon/
https://medium.com/@halilahmad/pantheon-subdomain-takeover-154f03a47057
https://medium.com/@hussain_0x3c/hostile-subdomain-takeover-using-pantheon-ebf4ab813111
https://infosecwriteups.com/fastly-subdomain-takeover-2000-217bb180730f
https://infosecwriteups.com/the-basics-of-subdomain-takeovers-a0bbd4c84a4
https://hackerone.com/reports/407355
https://hackerone.com/reports/38007
https://hackerone.com/greenhouse?type=team
https://blog.sweepatic.com/subdomain-takeover-principles/
https://hackerone.com/reports/32825
https://hackerone.com/reports/175070
https://hackerone.com/reports/172137
https://hackerone.com/reports/325336
