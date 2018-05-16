Title: How to use X11 via ssh and sudo
Category: Linux
Date: 2015-12-04 22:00

```
xauth list |grep \:$(echo $DISPLAY|cut -d ":" -f2|cut -d "." -f1) > /tmp/xauth
chmod 666 /tmp/xauth
sudo su – [new user]
cat /tmp/xauth |xargs -l xauth add  
```

