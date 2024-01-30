systemctl stop slapd.service
rm -rf slapd.d/*
rm /var/lib/ldap/*
slapadd -n 0 -F slapd.d -l slapd.ldif -v
chown -R openldap:openldap slapd.d/
systemctl restart slapd.service
ldapadd -Y EXTERNAL -H ldapi:/// -f rootdn-test.ldif -v
ldapsearch  -b "dc=tugraz,dc=at" -x
ldapadd -Y EXTERNAL -H ldapi:/// -f basedn-test.ldif -v

