---
tags:
  - ubuntu
  - DNS
  - ping
categories:
  - networks
excerpt: >-
   Fix: can ping with IP address but cannot ping with domain name
---
### HOWTO : Fix Temporary Failure In Name Resolution On Ubuntu 

If you are using Ubuntu version, you may encounter a ping problem. That is, you can ping with IP address but cannot ping with domain name. We can fix this problem by the following method.  
  
```
sudo mv /etc/resolv.conf /etc/resolv.conf-original
  
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf  

sudo systemctl restart systemd-resolved`  
```  
You can ping with domain name now.

source: [https://samiux.blogspot.com/2019/01/howto-fix-temporary-failure-in-name.html](https://samiux.blogspot.com/2019/01/howto-fix-temporary-failure-in-name.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIwNTg2NjIxNF19
-->