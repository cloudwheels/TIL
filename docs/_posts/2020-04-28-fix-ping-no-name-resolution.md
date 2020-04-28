
### HOWTO : Fix Temporary Failure In Name Resolution On Ubuntu 18.04.1

If you are using Ubuntu 18.04.1 Server version, you may encounter a ping problem. That is, you can ping with IP address but cannot ping with domain name. We can fix this problem by the following method.  
  
```
sudo mv /etc/resolv.conf /etc/resolv.conf-original
  
sudo ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf  

sudo systemctl restart systemd-resolved`  
```  
You can ping with domain name now.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExOTczMTg2MDJdfQ==
-->