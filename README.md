# Description

This docker is a full qmail server with

- sqmail
- vpopmail
- dovecot



# Patch and sources

This docker use sources and patches from

- http://cr.yp.to/daemontools.html
- https://www.fehcom.de/sqmail/sqmail.html
- https://notes.sagredo.eu/ (https://notes.sagredo.eu/files/qmail/patches/)
- https://www.inter7.com/vpopmail-virtualized-email/



# Upgrade to try

- https://github.com/bruceg/qmail-autoresponder



# Docker environment config**s**

- **QMAIL_NB_REMOTE**: Max concurrency remote send (*5*)
- **QMAIL_NB_INCOMING**: Max concurrency incoming mail (*50*)
- **VPOPMAIL_QUOTA**: Default email quota (*1Go*)
- **VPOPMAIL_MYSQL_XXXX**: VPopmail mysql config
  - VPOPMAIL_MYSQL_HOST
  - VPOPMAIL_MYSQL_DB
  - VPOPMAIL_MYSQL_USER
  - VPOPMAIL_MYSQL_PASS



########################

# Ram Disk pour QMAIL
########################
echo -e "tmpfs /var/qmail/tmp tmpfs defaults,size=256M,uid=qmaill,gid=sqmail,mode=777 0 0" >> /etc/fstab
mkdir -p /var/qmail/tmp
chown qmaill.sqmail /var/qmail/tmp
mount /var/qmail/tmp



Now copy the startup script ro */etc/rc.d* (Slackware) or *init.d* and run it. This is a Slackware example:

```
cp contrib/rc.vusaged /etc/rc.d/
/etc/rc.d/rc.vusaged start
```