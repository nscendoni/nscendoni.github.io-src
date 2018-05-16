Title: Configure OUD SMTP Notifications
Category: LDAP
Date: 2017-04-03 22:00

Perform following commands:
```
./dsconfig -h localhost -p 4444 -D "cn=directory manager" -j /tmp/pwd -X -n \
list-alert-handlers

dsconfig -h localhost -p 4444 -D "cn=directory manager" -j /tmp/pwd -X -n \
set-global-configuration-prop --set smtp-server:localhost

dsconfig -h localhost -p 4444 -D "cn=directory manager" -j /tmp/pwd -X -n \
create-alert-handler --handler-name "my SMTP Handler" --type smtp \
--set enabled:true --set message-body:"OUD Alert $HOSTNAME: %%alert-type%%
\n\nAlert ID: %%alert-id%%\n\nAlert Message: %%alert-message%%" \
--set message-subject:"$HOSTNAME OUD Alert Message" \
--set recipient-address:scendoni@gmail.com \
--set sender-address:scendoni@gmail.com
```
