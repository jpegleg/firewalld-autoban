# firewalld-autoban

see https://simple-evcorr.github.io/
and https://github.com/firewalld


Block IPs that SSH repeatedly and fail to authenticate.


Install with
chmod +x install
./install

...

Create a single exception by editing the config section from:

action=pipe '$0' /usr/local/sbin/autoban

To:

action=pipe '$0' /usr/local/sbin/autoban keeganbowen.com

where keeganbowen.com reverse lookup IP is an IP that you want to never ban.
Note that changing IPs in a round robin could eventually get them all banned
if each server fails repeated and the attempt comes from every member of a rotating pool.
Rather than allow this to happen if for some reason that is required,
see the next section on permanent excludes.

In addition to the one custom ACL in the first argument to autoban,
autoban also never blocks IPs starting with 10. as they are private IPs, see rfc5735 for more.
Additional IPs or IP regex or IP ranges can be added along with this by changing "10\.....\|192\.16\.....\|172\.16\....\|172\.17\...." to "what ever regex"
to add in 172.151.X.Y (example regex by simply leaving off the third and fourth octet)

...

autoban attempts to write an IPv4 rich rule type with the offending source
and checks to see if a reverse lookup returns an IP and uses that if present.
If the ipv4 rich rule fails, then autoban writes an IPv6 rule.
