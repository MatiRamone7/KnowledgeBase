# General Knowledge related to user store

OOTB: JDBC (Java Database Connectivity), LDAP (Lightweight Directory Access Protocol) and Active Directory.
Another ones: Custom User Stores, connected by User Store Managers.

## JDBC:

- JDBC server is used for updating data and processing queries to a relational database

## LDAP:

- LDAP server is used to process queries and data updates to an LDAP information directory.
- LDAP information directory is a type of database, but it's not a relational database.
- LDAP is preferred for static data. LDAP is more optimal for read operations.

https://is.docs.wso2.com/en/5.9.0/administer/ldap-vs-jdbc/#:~:text=A%20JDBC%20server%20is%20used,it's%20not%20a%20relational%20database.

## Primary User Store (Mandatory)
This is the main user store that is shared among all the tenants in the system. Only one user store should be configured as the primary user store and it is configured in the <IS_HOME>/repository/conf/deployment.toml file.By default, WSO2 identity server uses an embedded Read/Write LDAP as the primary user store.
By default, WSO2 Identity Server uses the embedded H2 database as the primary user store. It is recommended to change this default configuration in the production system.

## Secondary User Store (Optional)

Adapters used to connect with different users stores are called User Store Managers. By default, there are user store managers for JDBC, LDAP and Active Directory user stores. If you need to add a new user store implementation, see Writing a Custom User Store Manager. When you configure the user store, you have to set the user store manager class name.

https://is.docs.wso2.com/en/5.10.0/setup/configuring-user-stores/#primary-user-store-mandatory
https://is.docs.wso2.com/en/5.10.0/setup/writing-a-custom-user-store-manager/
