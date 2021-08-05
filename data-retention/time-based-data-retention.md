---
description: Setup and Configuration
---

# Time Based Data Retention

## **Setting up Retention Based Data Purge**

Retention based purge of data can be turned on to allow data to automatically be cleaned based on an organization's data retention policy.

### **Setup**

In order to set up retention based data purge, three \(3\) environment variables need to be set up in the owl-env.sh configuration script.  Note:  a restart of the webapp is required for this configuration to take place.

* **cleaner\_retention\_enabled**
  * TRUE or FALSE on whether this feature is enabled
* **cleaner\_retention\_days**
  * Number of days to retain data
* **cleaner\_retention\_field**
  * Controls which field to use to select eligible dataset runs
  * Potential values
    * updt\_ts:  consider the last time a dataset run was updated
    * run\_id:  consider the run id field of the dataset

### Configuration

**Example configuration in owl-env.sh**

Organization wants to purge data where the updt\_ts is more than 1 year old

**In owl-env.sh, add the following lines**

```
export cleaner_retention_enabled=TRUE
export cleaner_retention_days=365
export cleaner_retention_field="updt_ts" 

```

