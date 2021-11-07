# USB Ripper

Well, I got syslog (82M) and auth.json (12M).
There are 10_000 serial, manufacturer and product ids of usb devices in auth.json and 900_000 lines in syslog.

I decided to find serial id from syslog, that is not in the syslog file. There is simple script for it.
```python
import json

with open('auth.json') as f:
    text = f.read()

json.loads(text)
auth = json.loads(text)
            
serial = set()
search = 'SerialNumber: '
search_len = len(search)
with open('syslog') as f:
    for line in f:
        if search in line:
            serial.add(line[line.index(search) + search_len: -1])
            
auth_serial = set(auth['serial'])
print(serial - auth_serial)
```

So, I got one - 71DF5A33EFFDEA5B1882C9FBDC1240C6, and it wasn't a flag. But there is a note: 'once you find it, "crack" it'. I used [Crackstation](https://crackstation.net/) (my thanks to them), successfuly crack this md5 hash and got the flag