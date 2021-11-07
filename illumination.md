## Illumination

It's the easiest one at this moment. I got a folder with .git subfolder - so I used ```git log``` to see the history of commits. There is an interesting one  ```Thanks to contributors, I removed the unique token as it was a security risk.```
Then I used ```git diff 47241a47f62ada864ec74bd6dedc4d33f4374699 ddc606f8fa05c363ea4de20f31834e97dd527381``` to see what changed, and got
```
-       "token": "Replace me with token when in use! Security Risk!",
+       "token": "SFRCe3YzcnNpMG5fYzBudHIwbF9hbV9JX3JpZ2h0P30=",
```

The token looks like base64, so I tried to decode it 
```
echo 'SFRCe3YzcnNpMG5fYzBudHIwbF9hbV9JX3JpZ2h0P30=' | base64 --decode
```
It was success and I got the flag