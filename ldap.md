Based on https://aws.nz/best-practice/sssd-ldap/

Install packages 

yum install sssd sssd-tools sssd-ldap openldap-clients

Can connect to ldap


sssd.conf 
```
[root@lab-secure-cass02-cass02T1I01c2fca1f532fa248 efernandezbrei]# cat /etc/sssd/sssd.conf
[sssd]
config_file_version = 2
services = nss, pam
domains = SEA

[nss]
filter_groups = root
filter_users = root
reconnection_retries = 3
debug_level = 6

[pam]

[domain/SEA]
enumerate = false
ldap_referrals = false
auth_provider = ldap
id_provider = ldap
case_sensitive = False
debug_level = 6
cache_credentials = True
ldap_user_principal = userPrincipalName
ldap_user_object_class = user
ldap_group_object_class = group
ldap_group_name = sAMAccountName
ldap_user_name = sAMAccountName
ldap_default_authtok_type = obfuscated_password
ldap_search_base = dc=sea,dc=corp,dc=expecn,dc=com
#ldap_user_search_base = OU=All Users,dc=sea,dc=corp,dc=expecn,dc=com
ldap_user_search_base = OU=All Users,dc=sea,dc=corp,dc=expecn,dc=com?subtree??OU=Service Accounts,OU=Non-User,dc=sea,dc=corp,dc=expecn,dc=com?subtree?
ldap_group_search_base = OU=Security Groups,dc=sea,dc=corp,dc=expecn,dc=com?subtree??OU=Distribution Lists,dc=sea,dc=corp,dc=expecn,dc=com?subtree?
ldap_default_bind_dn = CN=s-adlookup,OU=Service Accounts,OU=Non-User,dc=sea,dc=corp,dc=expecn,dc=com
ldap_uri = ldaps://chcxadcsea002.sea.corp.expecn.com,ldaps://chcxadcsea003.sea.corp.expecn.com
ldap_user_home_directory = unixHomeDirectory
ldap_tls_cacertdir = /etc/openldap/cacerts
ldap_tls_reqcert = never
min_id = 100
ldap_schema = rfc2307bis
# Fall back
#ldap_schema = rfc2307
ldap_id_use_start_tls = False
ldap_default_authtok = AAAgAMiQ/Y06M72J+rzwwH6avIBDxaGpKd+wxvjR7gVq2t52OopfNqPIceRk+Apv15QzacZEenX8dUB4W6znsyEMy2iKLRO8iCczQpKVzufYbfHzAAECAzEC
access_provider = simple
simple_allow_groups = hcom-tech_ops,hcom-pret
```

