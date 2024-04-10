### General Auth related knowledge:

## So, what is the difference between authentication and authorization?
Simply put, authentication is the process of verifying who someone is, whereas authorization is the process of verifying what specific applications, files, and data a user has access to.
Authentication is used to verify that users really are who they represent themselves to be. Once this has been confirmed, authorization is then used to grant the user permission to access
different levels of information and perform specific functions, depending on the rules established for different types of users.

# Authentication:
- Determines whether users are who they claim to be	
- Challenges the user to validate credentials (for example, through passwords, answers to security questions, or facial recognition)	
- Usually done before authorization	
- Generally, transmits info through an ID Token	
- Generally governed by the OpenID Connect (OIDC) protocol	
- Example: Employees in a company are required to authenticate through the network before accessing their company email	

# Authorization: 
- Determines what users can and cannot access
- Verifies whether access is allowed through policies and rules
- Usually done after successful authentication
- Generally, transmits info through an Access Token
- Generally governed by the OAuth 2.0 framework
- Example: After an employee successfully authenticates, the system determines what information the employees are allowed to access

# Types of Authentication:
- What you know: Most commonly, this is a password. But it can also be an answer to a security question or a one-time pin that grants user access to just one session or transaction. 
- What you possess: This could be a mobile device or app, a security token, or digital ID card.
- What you are: This is biometric data such as a fingerprint, retinal scan, or facial recognition.

# Types of Authorization:
Role-based access controls (RBAC): This authorization method gives users access to information based on their role within the organization. For example, all employees within a company may be able to view, but not modify,
their personal information such as pay, vacation time, and 401K data. Yet human resources (HR) managers may be given access to all employees’ HR information with the ability to add, delete, and change this data.
By assigning permissions according to each person’s role, organizations can ensure every user is productive, while limiting access to sensitive information.
Attribute-based access control (ABAC): ABAC grants users permissions on a more granular level than RBAC using a series of specific attributes. This may include user attributes such as
the user’s name, role, organization, ID, and security clearance. It may include environmental attributes such as the time of access, location of the data, and current organizational threat levels. 
And it may include resource attributes such as the resource owner, file name, and level of data sensitivity. 
ABAC is a more complex authorization process than RBAC designed to further limit access. 
For example, rather than allowing all HR managers in an organization to change employees’ HR data, access can be limited to certain geographical locations or hours of the day to maintain tight security limits.
