# 2021.1.6 sudo using root password

Add line `Defaults rootpw` in /etc/sudoers, note that you will use `visudo` in root privilege in order to modify this file.

```bash
sudo visudo

...
Defaults rootpw
...
#save and will take effect immediately
```

