# AD Group to Owl Role Mapping

By Mapping an AD Group to an Owl role you are granting all users from the selected AD Group, role based access to the selected Owl role as depicted in the steps below. There will be more on creating custom application roles in the RBAC Section of this document.

Application properties set in owl-env.sh can be set to determine which LDAP properties correspond to LDAP Query results. For group mapping you will need the full path \(unique\) as well as the display name. 

For example:

```text
LDAP_GROUP_RESULT_DN_ATTRIBUTE=distinguishedname
LDAP_GROUP_RESULT_NAME_ATTRIBUTE=CN
```



![](https://lh4.googleusercontent.com/jrTaHJvax02-T0eoYKWigqTiB6nzcrPZPNRyI6wmg0pwIQ5Y8w9ZSne1GwMEx7Adtj1jdB8koDdcfniYx7cKQcoCjgi5tQ22yhcKvRlU3Xa9kOxA-KrwBfzM1IafIzyE4Bmdm1NX)

1. Click on “ROLE MAPPING”
2. Select a ROLE in the drop down list - \(Alternatively this is a time you can add a new Owl ROLE to map the AD Group\(s\) you want to include in that Owl ROLE\).
3. Click Load Groups
4. Select Group in the left box \(use the filter on top to filter base on what you provide in the text box\).
5. click the name to move it left to right.
6. click “Save” and you’ll get a response back to Owl-web like the following.

![](https://lh5.googleusercontent.com/b6FG3k6y73mbVt9eXl8AG9CORfKRGwvcJhR5pRNtx5F4lkjeWc8ZB6uKSd6M0BpoNmYv6Iw8Aai78XNH4fq3bEe6eITdr5f9DFOy9eBDg5b58KWMf94OZoza8I8cwNPMA3uStoUQ)

Now that we’ve mapped an AD Group to an AD Role we can now log out and try to login as a domain user.  \(REMEMBER: you will have to restart the owl-web by running ./owlmanage.sh restart\_owlweb when toggling AD Enabled\).

When logging into the Owl Web application please make sure to append the domain to the end of the user name as depicted below.

![](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Authentication%20and%20Authorization/WebHome/Screen%20Shot%202019-05-22%20at%2011.13.40%20AM.png?width=291&height=241)

