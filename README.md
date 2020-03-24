Several years ago I took responsibility of several linux servers, one public facing (sftp). I had limited
experience with linux and my predecessor left no documentation. When the Bash Bug reared its ugly head
I discovered that version 11 of Ubuntu was no longer supported. Because of uptime SLAs and terrible
technical support from the cloud provider, not to mention the documentation and experience issues, replacing
the VM was not realistic.

One thing I wanted to know was who was trying to log in, who succeeded, and from where. The most reasonable
approach was to search the auth logs using Bash. I delveloped some scripts with lots of help from random
Reddit users over the past several years to this end. That cloud provider is long dead, the VMs were migrated
into a rational universe, and I have moved on, but I still want to monitor access.

I have changed four bash scripts into one that does all functions. Check who has logged in and from where,
check who has tried and failed to log in, and failed attempts by geographic region, with the option to
email the results. It was developed and tested under Ubuntu. The usage is as follows:

chkacc - Check auth.log for successful and failed remote logon attempts
 -f - Check for failed logon attempts
 -s - Check for successful logons
 -e - Send output to email
 -g - Use geolocation database to identify source

The first time the script is run it creates the directory /etc/chkacc, sets the access, and puts the file
filter.sed into it. You need to edit the script and insert your email address into the TOEMAIL and FREMAIL
variables for the email option to work. Obviously, postfix will need to be installed and configured.
The geolocation option requires that GeoIP is installed (apt install geoip-bin geoip-database). I also
suggest editing /etc/rsyslog.conf and change $RepeatedMsgReduction to off.

I am open to ideas for future updates. I'd like the options to be combinable (chkacc -f -g -e cannot be
entered as chkacc -fge). Maybe I will have it view a selectable hard window for logs (one week, one month ...).
Support for RHEL/CentOS would be in order. There are many things I could do. I hope I get around to doing them.
