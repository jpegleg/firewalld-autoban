# firewalld-autoban
Block IPs that SSH repeatedly and fail to authenticate.

Create a single exception by editing the config section from:

action=pipe '$0' /usr/local/sbin/autoban

To:

action=pipe '$0' /usr/local/sbin/autoban keeganbowen.com

where keeganbowen.com reverse lookup IP is an IP that you want to never ban.

In addition to the one custom ACL in the first argument to autoban,
autoban also never blocks IPs starting with 10. as they are LAN IPs.
