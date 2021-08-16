---
description: OwlOptions is the new standard for configuring Owl within a notebook.
---

# Owl Options API

## Field mappings

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **dataset** | _ds_ | dataset name, example: userTable or users or user\_file |
| **rundId** | _rd_ | run date, must be in format **yyyy-MM-dd** or for incremental use Hours or Minutes **yyyy-MM-dd HH:mm** |
| **rundIdEnd** | _rdEnd_ | end date for query ranges **t\_date &gt;= ${rd} and t\_date &lt; ${rdEnd}**, must be in format **yyyy-MM-dd** or for incremental use Hours or Minutes **yyyy-MM-dd HH:mm** |
| **passFail** | _passfaillimit_ | Limit for passing or failing runs |
| **jobId** |  |  |
| **onReadOnly** | _readonly_ | Do not persist results to the Owl meta-store - useful during testing. |

## Load Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **fullFile** | _fullfile_ | use entire file for lookbacks instead of just filequery |
| **fileQuery** |  |  |
| **header** |  |  |
| **headerSrc** |  |  |
| **hasHeader** |  |  |
| **isParallel** |  |  |
| **isJson** |  |  |
| **isMixedJson** |  |  |
| **isMapsJson** |  |  |
| **flatten** |  |  |
| **isMultiLine** |  |  |
| **sparkprinc** |  |  |
| **sparkkeytab** |  |  |
| **jdbcprinc** |  |  |
| **jdbckeytab** |  |  |
| **srcpwdmgr** |  |  |
| **pwdmgr** |  |  |
| **pguser** | pguser |  |
| **pgpassword** | pgpassword |  |
| **pghost** | host |  |
| **pgport** | port |  |
| **executorcores** |  |  |
| **isParquet** |  |  |
| **isAvro** |  |  |
| **avroSchema** |  |  |
| **isXml** |  |  |
| **xmlRowTag** |  |  |
| **isOrc** |  |  |
| **dateFmt** |  |  |
| **timeFmt** |  |  |
| **datasetSafety** |  |  |
| **filePath** |  |  |
| **delimiter** |  |  |
| **fileLookBack** |  |  |
| **dbLookBack** |  |  |
| **connectionURL** |  |  |
| **userName** |  |  |
| **password** |  |  |
| **sqlQuery** |  |  |
| **connectionProps** |  |  |
| ~~zkHost~~ | ~~~~ | _**Deprecated**_ |
| ~~zkPort~~ | ~~~~ | _**Deprecated**_ |
| ~~zkPath~~ | ~~~~ | _**Deprecated**_ |

## Outlier Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **on** | dl | deep learning |
| **lookback** | dllb | deep learning lookback example value 5, for 5 days |
| **key** | dlkey | deep learning key. comma delim key ex: symbol,date |
| **dateField** |  |  |
| **bin** |  |  |
| **includes** | dlinc | deep learning col limit, example : open,close,high,volume |
| **excludes** | dlexc | deep learning col exclusion, example : open,close,high,volume |
| **categorical** |  |  |
| **by** |  |  |
| **limit** |  |  |
| **historyLimit** |  |  |
| **score** |  |  |

## FPG Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **on** | fpgon | pattern mining |
| **lookback** | fpglb | lookback interval for pattern mining. Ex: **-fpglb 5** |
| **key** | fpgkey | natural key for pattern mining activity |
| **dateField** | fpgdc | date column for pattern mining. Ex: **-fpgdc date\_col** |
| ~~**lowFreq**~~ |  | _**Deprecated**_ |
| **includes** | fpginc | pattern mining is expensive use this input to limit the observed cols |
| **excludes** | fpgexc | pattern mining is expensive use this input to limit the observed cols |
| **timeBin** | fpgtbin | time bin for pattern mining. Ex: **-fpgtbin DAY** |
| **score** | fpgscore | score for pattern mining records |
| **minSupport** | fpgsupport |  |
| **confidence** | fpgconfidence |  |

## Dupe Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **on** | dupe | duplicate record detection |
| **includes** | dupeinc | duplicate record detection, column inclusion list |
| **excludes** | dupeexc | duplicate record detection, column exclusion list |
| **depth** |  |  |
| **lowerBound** | dupelb | duplicate lower bounds on percent match default \[85\] |
| **upperBound** |  |  |
| **blocksize** |  |  |
| **useCache** |  |  |
| **checkHeader** |  |  |
| **exactMatch** |  |  |
| **ignoreCase** | dupenocase | duplicate record detection, column exclusion list |
| **score** | dupescore |  |
| **limit** | dupelimit | Limit for dupe rows stored |

## Profile Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **on** |  |  |
| **includes** |  |  |
| **excludes** |  |  |
| **dataShapeOn** |  |  |
| **statsOn** |  |  |
| **correlationOn** |  |  |
| **histogramOn** |  |  |
| **cardinalityOn** |  |  |
| **dataShapeColsInc** |  |  |
| **dataShapeColsExc** |  |  |

## Source Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **on** |  |  |
| **includes** |  |  |
| **excludes** |  |  |
| **key** |  |  |
| **fileQuery** |  |  |
| **map** |  |  |
| **score** |  |  |
| **datasetSrc** |  |  |
| **driverSrc** |  |  |
| **userNameSrc** |  |  |
| **passwordSrc** |  |  |
| **connectionURLSrc** |  |  |
| **sqlQuerySrc** |  |  |
| **connectionPropsSrc** |  |  |

## Rule Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **on** |  |  |
| **rulesOnly** |  |  |
| **semantic** |  |  |

## ColMatch Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **colMatchParallelProcesses** |  |  |
| **colMatchDurationMins** |  |  |
| **colMatchBatchSize** |  |  |
| **connectionList** |  |  |

## Spark Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **numExecutors** |  |  |
| **executorMemory** |  |  |
| **driverMemory** |  |  |
| **executorCores** |  |  |
| **master** |  |  |
| **jars** |  |  |
| **libs** |  |  |
| **driver** |  |  |

## Misc Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **obslimit** |  |  |
| **nullValue** |  |  |



