# README
---

## TODO
- [x] Create initial deployment


## Inventory File for cp-ansible
Here are the important bits for RBAC configuration using this openldap deployment.

```
all:
  vars:
    rbac_enabled: true
    mds_super_user: mds
    mds_super_user_password: mds
    kafka_broker_ldap_user: mds
    kafka_broker_ldap_password: mds
    schema_registry_ldap_user: schemaregistryUser
    schema_registry_ldap_password: schemaregistryUser
    kafka_connect_ldap_user: connectAdmin
    kafka_connect_ldap_password: connectAdmin
    ksql_ldap_user: ksqlDBAdmin
    ksql_ldap_password: ksqlDBAdmin
    kafka_rest_ldap_user: restAdmin
    kafka_rest_ldap_password: restAdmin
    control_center_ldap_user: controlcenterAdmin
    control_center_ldap_password: controlcenterAdmin
    kafka_connect_replicator_ldap_user: replicatorUser
    kafka_connect_replicator_ldap_password: replicatorUser
    # replicator configuration defaults to kafka_connect_replicator_ldap_user if unset, otherwise uncomment below for individual principals
    # kafka_connect_replicator_consumer_ldap_user: replicatorConsumer
    # kafka_connect_replicator_consumer_ldap_password: replicatorConsumer
    # kafka_connect_replicator_producer_ldap_user: replicatorProducer
    # kafka_connect_replicator_producer_ldap_password: replicatorProducer
    # kafka_connect_replicator_monitoring_interceptor_ldap_user: replicatorMonitoringUser
    # kafka_connect_replicator_monitoring_interceptor_ldap_password: replicatorMonitoringUser

    kafka_broker_custom_properties:
      ldap.java.naming.factory.initial: com.sun.jndi.ldap.LdapCtxFactory
      ldap.com.sun.jndi.ldap.read.timeout: 3000
      ldap.java.naming.provider.url: ldap://localhost:1389
      ldap.java.naming.security.principal: cn=admin,dc=confluentdemo,dc=io
      ldap.java.naming.security.credentials: admin
      ldap.search.mode: GROUPS
      ldap.group.search.base: ou=groups,dc=confluentdemo,dc=io
      ldap.group.name.attribute: cn
      ldap.group.member.attribute: memberUid
      ldap.group.object.class: posixGroup
      ldap.group.member.attribute.pattern: cn=(.*),ou=users,dc=confluentdemo,dc=io
      ldap.user.search.base: ou=users,dc=confluentdemo,dc=io
      ldap.user.name.attribute: uid
      ldap.user.object.class: inetOrgPerson
```
