# Authentication With Active Directory LDAP

Owl allows customers the ability to integrate with an existing AD solution via the Active Directory Configuration page. Administrators can configure AD integration by navigating to the Admin Console and clicking on the AD Setup Icon.

### Configuration Settings <a id="HConfigurationSettings"></a>

![](https://lh5.googleusercontent.com/Lp43WHEX924HWt6gtRs0LK7XpdFGU917CqHz2HVHvB9yN32FRatIWzmpZWQe2DTlPpK3e4X0OQqn5dOLAXrcQJkM9EHX1JHNhZAC-Eqn0pkYXrvpZqIlhP6kvBOSqEtQ7723K8EE)

1. AD Enabled = flag to enabled AD \(after binding please restart the owl-web application\)
2. Page Size = 100 is recommended.  The number of results in a single page \(NOTE: For really large AD Environments it’s best to narrow down the Base Path and/or possibly using Group Search Path to narrow down to that group explicitly\).
3. Host = Host: ldap://x.x.x.x or ldaps://x.x.x.x Port: is usually 389 for ldap or 636 for ldaps
4. Base Path is the domain specified in the example above owl.com \(equals to DC=owl,DC=com\).
5. Group Search Path = helps to narrow down list to an explicit group or parent group \(example: CN=owladmins\)
6. Bind user = &lt;user&gt;@&lt;domain&gt;
7. Bind Password = users domain password.
8. Click save and you should receive the message below on the top of the owl-web application.

![](https://lh4.googleusercontent.com/Z_btfJeipsC7WQrC2lC80Z9IwmomiBX8VFaNneAgdGOBPRfyArWao7f__C9TEFVXDb0-DyxFpXc3BUrpmhJs20gelNfA8TI7-sVTkyD4aVlV7Q1WUR50dN7MvukyrcBoUysfYgvm)

When binding to AD you do not need a special AD username and password. The application just needs a user to bind with in order to run a read-only query on the groups. The AD credentials are not stored, owl uses this dynamically to understand what groups you want to map.



![](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Authentication%20and%20Authorization/WebHome/Screen%20Shot%202019-05-22%20at%2011.13.40%20AM.png?width=291&height=241)

