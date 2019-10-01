---
description: Using OwlOptions will be the newest way how you can configure your notebooks.
---

# Owl Options API

## Field mappings

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **dataset** | _ds_ | dataset name, example: userTable or users or user\_file |
| **rundId** | _rd_ | run date, must be in format **yyyy-MM-dd** or for incremental use Hours or Minutes **yyyy-MM-dd HH:mm** |
| **rundIdEnd** | _rdEnd_ |  |
| **passFail** | _passfaillimit_ | Limit for passing or failing runs |
| **jobId** |  |  |
| **onReadOnly** | _readonly_ | Do not connect to meta store good for testing or trials |

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
| **pguser** |  |  |
| **pgpassword** |  |  |
| **pghost** | \*\*\*\* |  |
| **pgport** |  |  |
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
| ~~zkHost~~ | ~~~~ | ~~_**Deprecated**_~~ |
| ~~zkPort~~ | ~~~~ | ~~_**Deprecated**_~~ |
| ~~zkPath~~ | ~~~~ | ~~_**Deprecated**_~~ |

## Outlier Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **on** |  |  |
| **lookback** |  |  |
| **key** |  |  |
| **dateField** |  |  |
| **bin** |  |  |
| **includes** |  |  |
| **excludes** |  |  |
| **categorical** |  |  |
| **by** |  |  |
| **limit** |  |  |
| **historyLimit** |  |  |
| **score** |  |  |

## FPG Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **on** | \*\*\*\* |  |
| **lookback** |  |  |
| **key** |  |  |
| **dateField** |  |  |
| **lowFreq** |  |  |
| **includes** |  |  |
| **excludes** |  |  |
| **timeBin** |  |  |
| **score** |  |  |

## Dupe Options

| Field name | CLI prop | Description |
| :--- | :--- | :--- |
| **on** |  |  |
| **includes** |  |  |
| **excludes** |  |  |
| **depth** |  |  |
| **lowerBound** |  |  |
| **upperBound** |  |  |
| **blocksize** |  |  |
| **useCache** |  |  |
| **checkHeader** |  |  |
| **exactMatch** |  |  |
| **ignoreCase** |  |  |
| **score** |  |  |
| **limit** |  |  |

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



