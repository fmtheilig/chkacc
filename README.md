Several years ago I took responsibility of several linux servers, one public facing (sftp). I had
limited experience with linux and my predecessor left no documentation. When the Bash Bug reared
its ugly head I discovered that the repositories for my outdated version of Ubuntu were no longer
online. Because of uptime SLAs and terrible technical support from the cloud provider, not to
mention the documentation and experience issues, replacing the VM was not realistic.

I felt I needed to know was who was trying to log in, who succeeded, and from where. I figured
the most reasonable approach was to search the auth logs using Bash. I delveloped some scripts with
lots of help from random Reddit users over the past several years to this end. That cloud provider
is long dead, the VMs were upgraded and migrated into a rational environment, and I have moved on,
but the need to monitor access persists.

I changed the four bash scripts into one that handles all functions. Check who has logged in and
from where, check who has tried and failed to log in, and report by geographic region, with the
option to email the results. It was developed and tested under Ubuntu. The usage is as follows:

chkacc - Check auth.log for successful and failed remote logon attempts
 -f - Check for failed logon attempts
 -s - Check for successful logons
 -g - Use geolocation database to identify source
 -e - Send output to email
 -a - Enable all options

The first time the script is run it creates the directory /etc/chkacc, sets the access, and puts
the file filter.sed into it. You must edit the script and insert your email address into the
TOEMAIL and FREMAIL variables for the email option to work. Also, postfix must to be installed
and configured. The geolocation option requires that GeoIP is installed (apt install
geoip-bin geoip-database). I also suggest editing /etc/rsyslog.conf and change
$RepeatedMsgReduction to off.

I am open to ideas for future updates. Maybe I will have it view a selectable hard window for
logs (one week, one month ...). Support for RHEL/CentOS would be in order. Any other ideas?
