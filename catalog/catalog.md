# Catalog

### Smart Catalog - Bringing Data Science to Cataloging

While Owl does not pride itself on being a catalog tool it does automatically maintain a dataset and process catalog.  It is a necessary control for Owl and helpful to the end user.  Without a smart catalog a user could technically overwrite another user's OwlCheck \(DQ check\).  For example -ds "Trade" and -ds "Trade".  Owl believes a healthier habit is to store the full natural name of the dataset and allow the user to alias the name in the event that they wish to make a short-name.  By doing this Owl can protect users from mixing up their results and stops the constant renaming of common objects which leads to more unnecessary business level mapping.  This approach makes it effortless for a user to create a new OwlCheck in the wizard because Owl will warn the user if there is a naming collision.  Owl learns all the server hosts, the database schemas and table names and keeps things automatically organized.  One less catalog to setup, manage and eventually untangle.  

### Automatic Sensitive Data \(PII\) Detection

Owl automatically understands the _semantic_ schema of your data such as CREDIT CARD, EMAIL, SSN and much more.  Additionally Owl will label sensitive data with PII and MNPI classifications.

![](../.gitbook/assets/owl-catalog-pii.png)

### Data Table View of PII

Owl applies many labels to the header of a field / column.  These labels be seen in the data preview table with highlighted errors and findings. 

![](../.gitbook/assets/owl-pii.png)

