Title:  Add trusted CA to OpenLDAP client
Category: LDAP
Date: 2015-02-03 22:23

```
# cat /etc/openldap/ldap.conf
TLS_CACERTDIR   /etc/openldap/certs

# TLS_CACERTDIR=/etc/openldap/certs 
HASH=`openssl x509 -noout -hash -in /etc/openldap/certs/cacert1.pem` 
cd /etc/openldap/certs; ln -s cacert1.pem ${HASH}.0 
```

## Search
```
$ ldapsearch -d 256 -x -D "cn=directory manager" -w **** -b dc=example,dc=com -H ldaps://host:1636 "uid=myuid"
```

Reference: [http://www.openldap.org/faq/data/cache/185.html]
