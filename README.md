# What is this?
This is an authentication plugin (v0.3) for Radicale 3. It adds an LDAP authentication backend which can be used for authenticating users against an LDAP server.

It is confirmed to work with [OpenLDAP](https://github.com/osixia/docker-openldap), [LightLDAP](https://github.com/lldap/lldap/) and [Authentik](https://goauthentik.io).

I edited this plugin thanks to https://github.com/nitnelave, the Owner of LLDAP.

## Quick docker compose example
You can find a complete docker-compose example at https://github.com/shroomify-it/docker-deploy_radicale-agendav-lldap

## radicale config with LLDAP, no comments
You may add any other [section] from radicale's documentation.
For example the [rights] section : https://radicale.org/v3.html#authentication-and-rights

```
[auth]
#type = htpasswd
#htpasswd_filename = /etc/radicale/users/radicale-users
#htpasswd_encryption = md5

type = radicale_auth_ldap
ldap_url = ldap://lldap:3890  
ldap_base = dc=example,dc=com
ldap_attribute = uid
ldap_filter = (objectClass=person)
ldap_binddn = uid=admin,ou=people,dc=example,dc=com
ldap_password = CHANGEME
ldap_scope = LEVEL
ldap_support_extended = no
```


## radicale config with OPENLDAP, with comments
You will need to set a few options inside your radicale config file. Example:

```
[auth]
type = radicale_auth_ldap

# LDAP server URL, with protocol and port
ldap_url = ldap://ldap:389

# LDAP base path
ldap_base = ou=Users,dc=example,dc=com

# LDAP login attribute
ldap_attribute = uid

# LDAP filter string
# placed as X in a query of the form (&(...)X)
# example: (objectCategory=Person)(objectClass=User)(memberOf=cn=calenderusers,ou=users,dc=example,dc=com)
ldap_filter = (objectClass=person)

# LDAP dn for initial login, used if LDAP server does not allow anonymous searches
# Leave empty if searches are anonymous
ldap_binddn = cn=admin,dc=example,dc=com

# LDAP password for initial login, used with ldap_binddn
ldap_password = verysecurepassword

# LDAP scope of the search
ldap_scope = LEVEL

# LDAP extended option
# If the server is samba, ldap_support_extended is should be no
ldap_support_extended = yes
```
