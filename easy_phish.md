## Easy Phish
Some customers of secure-startup.com have been recieving some very convincing phishing emails. The first thing I did was use  ```dnsrecon -d secure-startup.com``` command to get information about DNS. So there I found two TXT records containing a flag, one of which is DMARC record.

I didn't know about [DMARC](https://en.wikipedia.org/wiki/DMARC) previously, so I think the task is very usefull for me =)
[Here link to quickstart](https://trendlineinteractive.com/resources/article/what-are-dmarc-dkim-and-spf/)

But it was too easy to find the flag and I decided to get it somehow different, by using default *nix commmands

Well, few more other options that I could think of
```
dig -t txt secure-startup.com _dmarc.secure-startup.com

host -t txt secure-startup.com
host -t txt _dmarc.secure-startup.com

nslookup -ty=txt secure-startup.com
nslookup -ty=txt _dmarc.secure-startup.com
```