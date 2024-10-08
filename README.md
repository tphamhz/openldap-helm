# Setup OpenLDAP

To connect, use port 389 for LDAP and port 636 for LDAPs

```
kubectl create ns openldap

helm install test-ldap . -f ldaps-rbac.yaml  -n openldap 

kubectl exec -it ldap-0 -n openldap  -- bash   


ldapsearch -LLL -x -H ldap://localhost:389 -b 'dc=tpham,dc=com' -D "cn=hzsa,dc=tpham,dc=com" -w 'Developer!'

ldapsearch -LLL -x -H ldap://ldap.openldap.svc.cluster.local:389 -b 'dc=tpham,dc=com' -D "cn=hzsa,dc=tpham,dc=com" -w 'Developer!'

```

The LDAP accounts are populated from `values.yaml`. User credential password follows the username naming convention i.e <username>-secret

## Browse LDAP on desktop

1. Install Apache Directory Studio
2. kubectl port-forward -n openldap  ldap-0 10636:636
or kubectl port-forward -n openldap  ldap-0 1389:389
3. Connect Apache Directory Studio to localhost:<port>