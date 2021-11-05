## Emdee five for life has

I've saw a site, with a single string and single field. The name and the field placeholder says to send a md5 hash.
I sent an incorrect string (simple '1') and got a message 'Too slow', so it's clear that I need a script to solve it.

Well, I just calculated the position (I think it's the fastest way to get needed string), and used default libraries - requests (surprisingly) to sent requests (in one session coz server saves the initial string in it I think, and without our cookie thinks that the result is an error) and hashlib to string md5 encoding.

```python
import hashlib
import requests

url = 'http://178.62.96.143:30644'

# setup session for single PHP session
md5_issue = requests.session()

r = md5_issue.get(url)
hash = hashlib.md5(r.content[167:187]).hexdigest()
r = md5_issue.post(url, data={'hash': hash})
print(r.text)
```