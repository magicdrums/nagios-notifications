nagios-extensions
=================

## Setup

1. Download the scripts and modify the $url and $from variables as appropriate for your nagios URL and the from email address desired.
2. Make the files executable. 
3. Update your nagios `/etc/nagios/objects/commands.cfg` file with the appropriate location of where you place these 2 files. I like to put them in `/etc/nagios/conf.d`
```
define command{ 
command_name notify-host-by-email 
command_line /etc/nagios/conf.d/host_email "$NOTIFICATIONTYPE$" "$HOSTNAME$" "$HOSTALIAS$" "$HOSTSTATE$" "$HOSTADDRESS$" "$HOSTOUTPUT$" "$SHORTDATETIME$" "$SERVICEDESC$" "$SERVICESTATE$" "$CONTACTEMAIL$" "$TOTALHOSTSUP$" "$TOTALHOSTSDOWN$" "$HOSTACKAUTHOR$" "$HOSTACKCOMMENT$" 
}
define command{ 
command_name notify-service-by-email 
command_line /etc/nagios/conf.d/service_email "$NOTIFICATIONTYPE$" "$HOSTNAME$" "$HOSTALIAS$" "$HOSTSTATE$" "$HOSTADDRESS$" "$SERVICEOUTPUT$" "$SHORTDATETIME$" "$SERVICEDESC$" "$SERVICESTATE$" "$CONTACTEMAIL$" "$SERVICEDURATIONSEC$" "$SERVICEEXECUTIONTIME$" "$TOTALSERVICESWARNING$" "$TOTALSERVICESCRITICAL$" "$TOTALSERVICESUNKNOWN$" "$LASTSERVICEOK$" "$LASTSERVICEWARNING$" "$SERVICENOTIFICATIONNUMBER$" "$SERVICEACKAUTHOR$" "$SERVICEACKCOMMENT$" 
}
```

## Notes
This sends mail via PHP. I use the ssmtp package to manage the mail settings. https://wiki.archlinux.org/index.php/SSMTP

## Credits
* host_email and service_email were originally written by shawnbrito at http://exchange.nagios.org/directory/Addons/Notifications/Send-HTML-Alert-Email-v2/details and I made some of my own tweaks to better suit my needs.

* twitter_alert script source: @EdVoncken - http://edvoncken.net/2011/08/twagios-2-0-nagios-notifications-revisited/
