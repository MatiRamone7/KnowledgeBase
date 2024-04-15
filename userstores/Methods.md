# ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png) Important methods ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png)

## boolean doAuthenticate(String userName, Object credential)

### Behaviour by default

This method returns details on whether the given username and password are matched or not. The credential is usually a string literal.	

### Reason for overriding

If you want to change the authentication logic, you can override this method and write your own implementation. The default task of this method is to compare the given password with the stored password. The given credentials are passed to the preparePassword method to do the salting or encryption before the comparison takes place.

## String preparePassword(Object password, String saltValue)	

### Behaviour by default

This returns the encrypted or plain-text password based on the configurations.

### Reason for overriding

You can override this method if you need to change the way you encrypt the password. If you want to change the algorithm that is used for encryption, you can configure it.

## Properties getDefaultUserStoreProperties()	

### Behaviour by default

The default properties of the user store are returned using this method. These properties are used in user store related operations. Be sure to manually add the following property when you implement the class to control whether the user store is enabled or disabled.: setOptionalProperty("Disabled", "false", "Whether user store is disabled");	

### Reason for overriding

By overriding this method, you can programmatically change the configuration of the user store manager implementation.

## boolean checkUserNameValid(String userName)	

### Behaviour by default

By overriding this method, you can programmatically change the configuration of the user store manager implementation.

### Reason for overriding

This is the criteria used for defining a valid username that can be configured as a regex in user store configurations. If you want to change the way user name validation is done, override this method.

## boolean checkUserPasswordValid(Object credential)	

### Behaviour by default

This returns whether the given password is compatible with the defined criteria. This is invoked when creating a user, updating a password, and authorization.	

### Reason for overriding

Similar to the username, you can configure the format of a valid password in configuration. If you want to change that behavior, you can override this method.

# ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png) Write methods and their default behaviours ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png)

## void doAddUser(String userName, Object credential, String[] roleList, Map<String, String> claims, String profileName, boolean requirePasswordChange)

This method is responsible to create a new user based on the given values. We can change the JDBC query or LDAP attribute name with the user store configuration.

## void doDeleteUser(String userName)

This removes the user store record related to the given username.

## void doUpdateCredential(String userName, Object newCredential, Object oldCredential)

This is responsible to update the credential of the given username after authenticating with the existing password.

## void doUpdateCredentialByAdmin(String userName, Object newCredential)

Admin users can use this method to update the credentials of a given user. This can be done without validating the existing password.

## void doAddRole(String roleName, String[] userList, boolean shared)

This creates a new user role with the given roleName and maps the given users to the newly created role. The shared parameter indicates whether this role is shared among tenants or not.

## void doDeleteRole(String roleName)

This method removes the given role and related mappings from the user store.

## void doUpdateRoleName(String roleName, String newRoleName)

This method is used to update the name of the existing roles.

## void doUpdateRoleListOfUser(String userName, String[] deletedRoles, String[] newRoles)

This is used to delete the existing mappings between the given user and deletedRoles while creating mappings to newRoles .

## void doUpdateUserListOfRole(String roleName, String[] deletedUsers, String[] newUsers)

This is used to delete the existing mappings between the given role and deletedUsers while creating mappings to newUsers .

## void doSetUserClaimValue(String userName, String claimURI, String claimValue, String profileName)

This is responsible for creating a new claim for a given user and profile with the given claim URI and value.

## void doSetUserClaimValues(String userName, Map<String, String> claims, String profileName)

This is responsible for creating a new claim for a given user and profile with the given list of claim URIs and values.

## void doDeleteUserClaimValue(String userName, String claimURI, String profileName)

Removes the existing claim details mapped with the given user and profile

## void doDeleteUserClaimValues(String userName, String[] claims, String profileName)

Removes the given list of claims from a given user

## void addRememberMe(String userName, String token)

This method is used to persist tokens in the user store.

## Group doAddGroup(String groupName, String groupId, List<String> userIds, Map<String, String>claims)

This method is used to create a group with given parameters.

## void doAddGroupWithUserIds(String groupName, List<String> userIds)

This method is used to create a group with given user uuid list.

## void doUpdateGroupNameByGroupId(String groupId, String newGroupName)

This method is used to update the name of the group with the given group uuid..

## void doUpdateUserListOfGroup(String groupId, List<String> deletedUserIds, List<String> newUserIds)

This method is used to update the user list of a group.

## void doDeleteGroupByGroupId(String groupId)

This method is used to delete the group with the given id.

## void doAddGroupWithUserNames(String groupName, List<String> userNames)

This method is used to create a group with the given name and given set of user names.

## void doUpdateGroupName(String currentGroupName, String newGroupName)

This method is used to update name of the group with the given current name.

## void doDeleteGroupByGroupName(String groupName)

This method is used to delete the group with the name


# ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png) Read methods and their default behaviours ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png)

## boolean doCheckExistingUser(String userName)	

Returns whether the provided userName already exists in the user store

## boolean doCheckExistingRole(String roleName)	

Returns whether the provided roleName already exists in the user store

## String[] doListUsers(String filter, int maxItemLimit)	

This method returns a list of usernames that match the given filter string.

## String[] doGetRoleNames(String filter, int maxItemLimit)	

Returns a list of role names that match with the given filter string.

## String[] doGetExternalRoleListOfUser(String userName, String filter)	

Returns a list of external role names of a given user that match with the given filter string

## String[] doGetSharedRoleListOfUser(String userName, String tenantDomain, String filter)	

This method returns a list of shared role names of a given user that match the given filter string.

## Map<String, String> getUserPropertyValues(String userName, String[] propertyNames, String profileName)	

This method returns values for the given propertyNames for a given userName and profileName.

## String[] getUserListFromProperties(String property, String value, String profileName)	

This returns a list of usernames that match with the given value of the given property and profileName.

## String[] doGetDisplayNamesForInternalRole(String[] userNames)	

Returns names to display in the UI for given usernames

## Date getPasswordExpirationTime(String userName)	

This returns the password expiry date of a given user. The default value is null.

## int getUserId(String username)	

This method returns the identifier of a given username. The default value is 0.

## boolean doCheckIsUserInRole(String userName, String roleName)	

True is returned if the given user is already mapped to the given role name.

## String[] getProfileNames(String userName)	

Returns a list of profile names mapped with a given username.

## String[] doGetSharedRoleNames(String tenantDomain, String filter, int maxItemLimit)	

This returns a list of role names that are associated with the given tenant domain and match with the filter.

## String[] doGetUserListOfRole(String roleName, String filter)	

This method returns a list of usernames that are mapped with the given rolename.

## String[] getAllProfileNames()	

All the profile names are returned including the default profile.

## boolean isValidRememberMeToken(String userName, String token)	

This method is used to check if the given token exists for the given user.

## boolean isMultipleProfilesAllowed()	

This returns whether this user store is allowed to have multiple profiles per user. The default value is false.

## boolean isBulkImportSupported()	

This method returns whether this user store allows bulk transactions or not.

## String doGetGroupIdFromGroupName(String groupName)	

This method returns group uuid which has the given group name.

## String doGetGroupNameFromGroupId(String groupId)	

This method returns group name which has the given group uuid.

## Group doGetGroupFromGroupName(String groupName, List<String> requiredAttributes)	

This method returns the group with the given group name.

## Group doGetGroupFromGroupId(String groupId, List<String> requiredAttributes)	

This method returns the group with the given group uuid.

## List<Group> doGetGroupListOfUser(String userId, int limit, int offset, String sortBy, String sortOrder)	

This method returns the group list of a given user.

## List<Group> doListGroups(Condition condition, int limit, int offset, String sortBy, String sortOrder)	

This method return the group list which matches with the given condition.

# ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png) Implementations ![#f03c15](https://placehold.co/15x15/f03c15/f03c15.png)

![#c5f015](https://placehold.co/15x15/c5f015/c5f015.png) Class org.wso2.carbon.user.core.jdbc.UniqueIDJDBCUserStoreManager	

If your user details are stored in a database, you must use this user store manager implementation. With the abstraction provided in this implementation, most of the JDBC-based scenarios can be handled without writing a custom user store manager.

![#c5f015](https://placehold.co/15x15/c5f015/c5f015.png) Class org.wso2.carbon.user.core.ldap.UniqueIDReadOnlyLDAPUserStoreManager	

You can use this class if you have an LDAP user store. This implementation does not allow you to insert or update users from the WSO2 Identity Server side. Instead, you can only read and use them in the product.

![#c5f015](https://placehold.co/15x15/c5f015/c5f015.png) Class org.wso2.carbon.user.core.ldap.UniqueIDReadWriteLDAPUserStoreManager	

If you want to allow WSO2 Identity Server to manipulate user store data, you need to use this implementation.

![#c5f015](https://placehold.co/15x15/c5f015/c5f015.png) Class org.wso2.carbon.user.core.ldap.UniqueIDActiveDirectoryLDAPUserStoreManager	

Active Directory also can be used as the user store of WSO2 Identity Server and you can configure it using this user store manager implementation.
