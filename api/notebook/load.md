# Load

```java
package com.owl.common.options;

import org.apache.commons.lang3.StringUtils;

import java.util.Properties;

/**
 * Owl Options related to data loading
 */
public class LoadOpt {
    // Options order: "unsorted",
    // "dataset scope columns", "dataset scope rows", "look back",
    // "common options for both data sources", "file as data source", "db as data source"

    public static final String SINGLE_QUOTE = "'";
    public static final String DOUBLE_QUOTE = "\"";
    public static final String BACK_TICK = "`";

    /**
     * If true, don't save any metadata
     * TODO confirm if this is correct
     */
    public Boolean readonly = false;

    /**
     * The Password manager.
     */
    public String passwordManager = null;

    /**
     * Catalog alias (Catalog name)
     */
    public String alias = StringUtils.EMPTY;

    // --- Dataset Scope Column specifications ------- //
    // Properties that select columns for Dataset activities or modifies (data type or new columns)
    // prior and/or during loading into Spark DF
    /**
     * Dataset scope query. (IMPORTANT)
     * The query should contain all the columns necessary to run the activities.
     * TODO: figure out if this gets used when using files
     */
    public String query = StringUtils.EMPTY;

    /**
     * Concatenated column names (sep = ",") for columns that are keys
     * TODO: confirm
     */
    public String key = StringUtils.EMPTY;

    /**
     * SELECT expression to transform expressions with assignment by "=" and delimited by "|".
     * e.g. colname=cast(colname as string)|colname2=colname2(cast as date)
     */
    public String expression = StringUtils.EMPTY;

    /**
     * Add "OWL_RUN_ID" UNIX timestamp (s) column to Spark DF usng the OwlOptions.runId.
     * Does not obey timeStampDivisor (timestamp in seconds because Spark)
     */
    public Boolean addDateColumn = false;

    /**
     * Fill null values in Spark DF with 0 (numeric columns only)
     */
    public Boolean zeroFillNull = false;

    /**
     * A string that indicates a null value; any value matching this string will be set as nulls in the Spark DF
     * Default: "" -> NULL
     * Example: 'null' -> NULL
     * --
     * Note: to emptyStirngFillNull (replace String column null -> "", use expression
     */
    public String replaceNulls = StringUtils.EMPTY;

    /**
     * All data types forced to strings for type safe processing.
     * Not implemented in activity (yet)
     */
    public Boolean stringMode = false;

    // --- Dataset Scope Row specifications ------- //
    // Properties that filter rows for Dataset activities
    // prior and/or during loading into Spark DF
    /**
     * Convert row into string and only use rows containing this value.
     * Strict matching only.
     */
    public String filter = StringUtils.EMPTY;

    /**
     * Convert row into string and only use rows containing this value.
     * Strict matching only.
     */
    public String filterNot = StringUtils.EMPTY;

    // --- Look back ------- //
    // For Look back feature
    /**
     * Build up history of OwlChecks. Does not include current OwlCheck.
     * TODO: Document the relationship with unionLookBack
     */
    public Integer backRun = null;

    /**
     * Whether to load data for looking back in history.
     * How much historical data to load is based on OutlierOpt.lookback and PatternOpt.lookback.
     */
    public Boolean unionLookBack = false;

    // --- Shared Data Loading Options ------- //
    // Properties that affect data loading & pre-processing for both files and db as source
    /**
     * Whether to use cached data for activities
     */
    public Boolean cache = true;

    /**
     * The year, month, and day format of date columns in the dataset for loading the data only.
     * Default = "yyyy-MM-dd"
     */
    public String dateFormat = "yyyy-MM-dd";

    /**
     * The hour, minute, second, and milisecond format of date columns in the dataset for loading the data only/
     * Default = "HH:mm:ss.SSS"
     * Not used. Questionably why separate timeFormat variable exists when dateFromat can represent hms as well.
     */
    public String timeFormat = "HH:mm:ss.SSS";

    /**
     * Whether to convert date columns (specified by activity opts) in dataset
     * into timestamp in ms (to make it seconds, set Props.timeStampDivisor = "s")
     * TODO: Needs LoadOpt.timeStampDivisor and fix Utils.scala date2Timestamp
     */
    public Boolean timestamp = false;

    /* TODO add timeStampDivisor here and map between owl props?
     public String timeStampDivisor = "ms"
     */

    // --- Using file as data source ------- //
    // Properties that control where & how static file is read
    /**
     * Full path to the file.
     * If hdfs, then "hdfs://...".
     * If s3, then "s3://...", "s3a://...", or "s3n://...".
     * If parquet, then "...parquet" or "...PARQUET"
     */
    public String filePath = StringUtils.EMPTY;

    /**
     * SQL query used on file.
     * owl_id is added if not included in select clause.
     * If empty, then defaults to full file query.
     * (Does not update LoadOpts.fullFile to true).
     */
    public String fileQuery = StringUtils.EMPTY;

    /**
     * Whether to use full file (i.e. use all columns) on data load
     */
    public Boolean fullFile = false;

    /**
     * File column names, comma separated
     */
    public String fileHeader = null;

    /* TODO checkHeader needs to be moved here from DupeOpt
     public Boolean checkHeader = true;*/

    /**
     * Whether to have Spark infer the schema of data source
     * If props.profile2 == true, this is overwritten to false!
     * If xml file, this is ignored and schema is always inferred by Spark on xml data load.
     * If avro file, this value is respected (but may get overwritten by props.profile2)
     * (see activity2.Load.file)
     */
    public Boolean inferSchema = true;

    /**
     * Sample without replacement from file. Valid value is a fraction [0, 1.0].
     * Only affects when filetype is xml or unspecified (and therefore assumed to be delimited table)
     */
    public Double sample = 1.0;

    /**
     * Filetype (avro, json, orc, parquet, xml). Unspecified file
     */
    public FileType fileType = null;

    /**
     * Delimiter for file. If number of characters after replacing "\" with "" is 2 or more character
     * (e.g. compound delimiters like \t\t), then defaults to "\t" and attempts to read file as tsv
     * See Activity2.load.file for details
     */
    public String delimiter = ",";

    /**
     * File character encoding
     */
    public String fileCharSet = "UTF-8";

    /**
     * The Avro schema for relevant avro file. Ignored if empty string
     */
    public String avroSchema = StringUtils.EMPTY;

    /**
     * The Xml row tag for xml file. Ignored if empty string.
     */
    public String xmlRowTag = StringUtils.EMPTY;

    /**
     * Whether to flatten arrays in nested schema
     * TODO explain better. Does this only affect JSON file?
     */
    public Boolean flatten = false;

    /**
     * Whether data contains maps in json that requires extra handling"
     * TODO explain better. Does this only affect JSON file?
     */
    public Boolean handleMaps = false;

    /**
     * Whether to handle mixed json.
     * TODO explain better. Does this only affect JSON file?
     */
    public Boolean handleMixedJson = false;

    /**
     * Spark.read option multiline, for JSON file only
     */
    public Boolean multiLine = false;

    // --- Using database as data source ------ //
    /**
     * Path to DB Driver. (e.g. /opt/owl/driver/postgres)
     */
    public String lib = StringUtils.EMPTY;

    /**
     * DB Driver name (Java namespace, e.g. org.postgresql.Driver).
     * Leave as null (default) and LoadOpts.connectionURL will resolve the driver name.
     */
    public String driverName = null;

    /**
     * Connections name in metastore DB (public.connections.aliasname).
     * Does not refer to the "name" of the database. Refers to "aliasname" that the user set when
     * uploading connection config to Owl.
     */
    public String connectionName = StringUtils.EMPTY;

    /**
     * The Connection url, prefixed by jdbc.
     * e.g. "jdbc:postgresql://localhost:5432"
     */
    public String connectionUrl = StringUtils.EMPTY;

    /**
     * DB username
     */
    public String userName = StringUtils.EMPTY;

    /**
     * DB password
     */
    public String password = StringUtils.EMPTY;

    /**
     * JDBC Connection properties (e.g. fetchsize)
     */
    public Properties connectionProperties = null;

    /**
     * Whether data source is Hive Native (not using JDBC)
     * TODO: Why is the default null as opposed to false?
     */
    public Boolean hiveNative = null;

    /**
     * Whether data source is Hive Hadoop Web Cluster (not using JDBC)
     */
    public Boolean hiveNativeHWC = false;

    // --- Parallel JDBC ------- //
    /**
     * When running parallel JDBC, use LoadOpts.query and OwlOptions.dataset as base table
     */
    public Boolean useSql = true;

    /**
     * When running parallel JDBC, specify column name
     * ?? Activity2.Load and web has hard-coded magic string "OWLAUTOJDBC"
     */
    public String columnName = null;

    /**
     * When running parallel JDBC, the upper bound for partition column.
     * (e.g. "1000000")
     */
    public String lowerBound = null;

    /**
     * When running parallel JDBC, the upper bound for partition column.
     * (e.g. "5000000")
     */
    public String upperBound = null;

    /**
     * When running parallel JDBC, the number of partitions used.
     * If 0, then numPartitions used is based on the number of available Spark Executor (1/2 ~ 2/3)
     * If > 20, then overwritten to 20 (no more than 20 concurrent connections to a database on a single dataset)
     */
    public Integer numPartitions = 0;

    // --- SQL Query properties ---------- //
    // TODO: does this effect DB as source or file as source as well?
    /**
     * Whether the escape character would be back tick (`).
     * Ignored if escapeCharacter is non-empty (if using OwlCheck from Options).
     * Marked as true if props.escapeCharacter is a tick
     * (to preserve bijection between props and opts, and vice versa).
     */
    public Boolean escapeWithBackTick = false;
    /**
     * Whether the escape character would be single quote (').
     * Ignored if escapeCharacter is non-empty (if using OwlCheck from Options).
     * Marked as true if props.escapeCharacter is a tick
     * (to preserve bijection between props and opts, and vice versa).
     */
    public Boolean escapeWithSingleQuote = false;
    /**
     * Whether the escape character would be double quote (").
     * Ignored if escapeCharacter is non-empty(if using OwlCheck from Options).
     * Marked as true if props.escapeCharacter is a tick
     * (to preserve bijection between props and opts, and vice versa).
     */
    public Boolean escapeWithDoubleQuote = false;

    /**
     * Specify custom escape character. This takes precedence over all other escapeWithXYZ options.
     * i.e. if non-empty, then other escapeWithXYZ options are ignored.
     * If empty (default), no escaping attempt is made (and SQL query may fail if it contains reserved word)
     *
     * @deprecated Access level of this field will be changed to private. Please use {@link #setEscapeCharacter(String)} instead.
     */
    @Deprecated
    public String escapeCharacter = StringUtils.EMPTY;

    // ----------------- //
    // Getters and setters

    /**
     * Gets readonly.
     *
     * @return the readonly
     */
    public Boolean getReadonly() {
        return readonly;
    }

    /**
     * Sets readonly.
     *
     * @param readonly the readonly
     */
    public void setReadonly(Boolean readonly) {
        this.readonly = readonly;
    }

    /**
     * Gets full file.
     *
     * @return the full file
     */
    public Boolean getFullFile() {
        return fullFile;
    }

    /**
     * Sets full file.
     *
     * @param fullFile the full file
     */
    public void setFullFile(Boolean fullFile) {
        this.fullFile = fullFile;
    }

    /**
     * Gets file query.
     *
     * @return the file query
     */
    public String getFileQuery() {
        return fileQuery;
    }

    /**
     * Sets file query.
     *
     * @param fileQuery the file query
     */
    public void setFileQuery(String fileQuery) {
        this.fileQuery = fileQuery;
    }

    /**
     * Gets file header.
     *
     * @return the file header
     */
    public String getFileHeader() {
        return fileHeader;
    }

    /**
     * Sets file header.
     *
     * @param fileHeader the file header
     */
    public void setFileHeader(String fileHeader) {
        this.fileHeader = fileHeader;
    }

    /**
     * Gets has header.
     *
     * @return the has header
     */
    public Boolean getHasHeader() {
        return fileHeader == null;
    }

    /**
     * Gets file type.
     *
     * @return the file type
     */
    public FileType getFileType() {
        return fileType;
    }

    /**
     * Sets file type.
     *
     * @param fileType the file type
     */
    public void setFileType(FileType fileType) {
        this.fileType = fileType;
    }

    /**
     * Sets file type.
     *
     * @param fileTypeString the file type string
     */
    public void setFileType(String fileTypeString) {
        this.fileType = FileType.valueOf(fileTypeString);
    }

    /**
     * Gets password manager.
     *
     * @return the password manager
     */
    public String getPasswordManager() {
        return passwordManager;
    }

    /**
     * Sets password manager.
     *
     * @param passwordManager the password manager
     */
    public void setPasswordManager(String passwordManager) {
        this.passwordManager = passwordManager;
    }

    /**
     * Gets avro schema.
     *
     * @return the avro schema
     */
    public String getAvroSchema() {
        return avroSchema;
    }

    /**
     * Sets avro schema.
     *
     * @param avroSchema the avro schema
     */
    public void setAvroSchema(String avroSchema) {
        this.avroSchema = avroSchema;
    }

    /**
     * Gets xml row tag.
     *
     * @return the xml row tag
     */
    public String getXmlRowTag() {
        return xmlRowTag;
    }

    /**
     * Sets xml row tag.
     *
     * @param xmlRowTag the xml row tag
     */
    public void setXmlRowTag(String xmlRowTag) {
        this.xmlRowTag = xmlRowTag;
    }

    /**
     * Gets date format.
     *
     * @return the date format
     */
    public String getDateFormat() {
        return dateFormat;
    }

    /**
     * Sets date format.
     *
     * @param dateFormat the date format
     */
    public void setDateFormat(String dateFormat) {
        this.dateFormat = dateFormat;
    }

    /**
     * Gets time format.
     *
     * @return the time format
     */
    public String getTimeFormat() {
        return timeFormat;
    }

    /**
     * Sets time format.
     *
     * @param timeFormat the time format
     */
    public void setTimeFormat(String timeFormat) {
        this.timeFormat = timeFormat;
    }

    /**
     * Gets file path.
     *
     * @return the file path
     */
    public String getFilePath() {
        return filePath;
    }

    /**
     * Sets file path.
     *
     * @param filePath the file path
     */
    public void setFilePath(String filePath) {
        this.filePath = filePath;
    }

    /**
     * Gets delimiter.
     *
     * @return the delimiter
     */
    public String getDelimiter() {
        return delimiter;
    }

    /**
     * Sets delimiter.
     *
     * @param delimiter the delimiter
     */
    public void setDelimiter(String delimiter) {
        this.delimiter = delimiter;
    }

    /**
     * Gets union look back.
     *
     * @return the union look back
     */
    public Boolean getUnionLookBack() {
        return unionLookBack;
    }

    /**
     * Sets union look back.
     *
     * @param unionLookBack the union look back
     */
    public void setUnionLookBack(Boolean unionLookBack) {
        this.unionLookBack = unionLookBack;
    }

    /**
     * Gets cache.
     *
     * @return the cache
     */
    public Boolean getCache() {
        return cache;
    }

    /**
     * Sets cache.
     *
     * @param cache the cache
     */
    public void setCache(Boolean cache) {
        this.cache = cache;
    }

    /**
     * Gets timestamp.
     *
     * @return the timestamp
     */
    public Boolean getTimestamp() {
        return timestamp;
    }

    /**
     * Sets timestamp.
     *
     * @param timestamp the timestamp
     */
    public void setTimestamp(Boolean timestamp) {
        this.timestamp = timestamp;
    }

    /**
     * Gets infer schema.
     *
     * @return the infer schema
     */
    public Boolean getInferSchema() {
        return inferSchema;
    }

    /**
     * Sets infer schema.
     *
     * @param inferSchema the infer schema
     */
    public void setInferSchema(Boolean inferSchema) {
        this.inferSchema = inferSchema;
    }

    /**
     * Gets key.
     *
     * @return the key
     */
    public String getKey() {
        return key;
    }

    /**
     * Sets key.
     *
     * @param key the key
     */
    public void setKey(String key) {
        this.key = key;
    }

    /**
     * Gets lib.
     *
     * @return the lib
     */
    public String getLib() {
        return lib;
    }

    /**
     * Sets lib.
     *
     * @param lib the lib
     */
    public void setLib(String lib) {
        this.lib = lib;
    }

    /**
     * Gets lower bound.
     *
     * @return the lower bound
     */
    public String getLowerBound() {
        return lowerBound;
    }

    /**
     * Sets lower bound.
     *
     * @param lowerBound the lower bound
     */
    public void setLowerBound(String lowerBound) {
        this.lowerBound = lowerBound;
    }

    /**
     * Gets upper bound.
     *
     * @return the upper bound
     */
    public String getUpperBound() {
        return upperBound;
    }

    /**
     * Sets upper bound.
     *
     * @param upperBound the upper bound
     */
    public void setUpperBound(String upperBound) {
        this.upperBound = upperBound;
    }

    /**
     * Gets num partitions.
     *
     * @return the num partitions
     */
    public Integer getNumPartitions() {
        return numPartitions;
    }

    /**
     * Sets num partitions.
     *
     * @param numPartitions the num partitions
     */
    public void setNumPartitions(Integer numPartitions) {
        this.numPartitions = numPartitions;
    }

    /**
     * Gets sample.
     *
     * @return the sample
     */
    public Double getSample() {
        return sample;
    }

    /**
     * Sets sample.
     *
     * @param sample the sample
     */
    public void setSample(Double sample) {
        this.sample = sample;
    }

    /**
     * Gets use sql.
     *
     * @return the use sql
     */
    public Boolean getUseSql() {
        return useSql;
    }

    /**
     * Sets use sql.
     *
     * @param useSql the use sql
     */
    public void setUseSql(Boolean useSql) {
        this.useSql = useSql;
    }

    /**
     * Gets zero fill null.
     *
     * @return the zero fill null
     */
    public Boolean getZeroFillNull() {
        return zeroFillNull;
    }

    /**
     * Sets zero fill null.
     *
     * @param zeroFillNull the zero fill null
     */
    public void setZeroFillNull(Boolean zeroFillNull) {
        this.zeroFillNull = zeroFillNull;
    }

    /**
     * Gets string mode.
     *
     * @return the string mode
     */
    public Boolean getStringMode() {
        return stringMode;
    }

    /**
     * Sets string mode.
     *
     * @param stringMode the string mode
     */
    public void setStringMode(Boolean stringMode) {
        this.stringMode = stringMode;
    }

    /**
     * Gets alias.
     *
     * @return the alias
     */
    public String getAlias() {
        return alias;
    }

    /**
     * Sets alias.
     *
     * @param alias the alias
     */
    public void setAlias(String alias) {
        this.alias = alias;
    }

    /**
     * Gets back run.
     *
     * @return the back run
     */
    public Integer getBackRun() {
        return backRun;
    }

    /**
     * Sets back run.
     *
     * @param backRun the back run
     */
    public void setBackRun(Integer backRun) {
        this.backRun = backRun;
    }

    /**
     * Gets column name.
     *
     * @return the column name
     */
    public String getColumnName() {
        return columnName;
    }

    /**
     * Sets column name.
     *
     * @param columnName the column name
     */
    public void setColumnName(String columnName) {
        this.columnName = columnName;
    }

    /**
     * Gets driver name.
     *
     * @return the driver name
     */
    public String getDriverName() {
        return driverName;
    }

    /**
     * Sets driver name.
     *
     * @param driverName the driver name
     */
    public void setDriverName(String driverName) {
        this.driverName = driverName;
    }

    /**
     * Gets connection name.
     *
     * @return the connection name
     */
    public String getConnectionName() {
        return connectionName;
    }

    /**
     * Sets connection name.
     *
     * @param connectionName the connection name
     */
    public void setConnectionName(String connectionName) {
        this.connectionName = connectionName;
    }

    /**
     * Gets file char set.
     *
     * @return the file char set
     */
    public String getFileCharSet() {
        return fileCharSet;
    }

    /**
     * Sets file char set.
     *
     * @param fileCharSet the file char set
     */
    public void setFileCharSet(String fileCharSet) {
        this.fileCharSet = fileCharSet;
    }

    /**
     * Gets hive native.
     *
     * @return the hive native
     */
    public Boolean getHiveNative() {
        return hiveNative;
    }

    /**
     * Sets hive native.
     *
     * @param hiveNative the hive native
     */
    public void setHiveNative(Boolean hiveNative) {
        this.hiveNative = hiveNative;
    }

    /**
     * Gets hive native hwc.
     *
     * @return the hive native hwc
     */
    public Boolean getHiveNativeHWC() {
        return hiveNativeHWC;
    }

    /**
     * Sets hive native hwc.
     *
     * @param hiveNativeHWC the hive native hwc
     */
    public void setHiveNativeHWC(Boolean hiveNativeHWC) {
        this.hiveNativeHWC = hiveNativeHWC;
    }

    /**
     * Gets add date column.
     *
     * @return the add date column
     */
    public Boolean getAddDateColumn() {
        return addDateColumn;
    }

    /**
     * Sets add date column.
     *
     * @param addDateColumn the add date column
     */
    public void setAddDateColumn(Boolean addDateColumn) {
        this.addDateColumn = addDateColumn;
    }

    /**
     * Gets filter.
     *
     * @return the filter
     */
    public String getFilter() {
        return filter;
    }

    /**
     * Sets filter.
     *
     * @param filter the filter
     */
    public void setFilter(String filter) {
        this.filter = filter;
    }

    /**
     * Gets filter not.
     *
     * @return the filter not
     */
    public String getFilterNot() {
        return filterNot;
    }

    /**
     * Sets filter not.
     *
     * @param filterNot the filter not
     */
    public void setFilterNot(String filterNot) {
        this.filterNot = filterNot;
    }

    /**
     * Gets flatten.
     *
     * @return the flatten
     */
    public Boolean getFlatten() {
        return flatten;
    }

    /**
     * Sets flatten.
     *
     * @param flatten the flatten
     */
    public void setFlatten(Boolean flatten) {
        this.flatten = flatten;
    }

    /**
     * Gets handle maps.
     *
     * @return the handle maps
     */
    public Boolean getHandleMaps() {
        return handleMaps;
    }

    /**
     * Sets handle maps.
     *
     * @param handleMaps the handle maps
     */
    public void setHandleMaps(Boolean handleMaps) {
        this.handleMaps = handleMaps;
    }

    /**
     * Gets handle mixed json.
     *
     * @return the handle mixed json
     */
    public Boolean getHandleMixedJson() {
        return handleMixedJson;
    }

    /**
     * Sets handle mixed json.
     *
     * @param handleMixedJson the handle mixed json
     */
    public void setHandleMixedJson(Boolean handleMixedJson) {
        this.handleMixedJson = handleMixedJson;
    }

    /**
     * Gets multi line.
     *
     * @return the multi line
     */
    public Boolean getMultiLine() {
        return multiLine;
    }

    /**
     * Sets multi line.
     *
     * @param multiLine the multi line
     */
    public void setMultiLine(Boolean multiLine) {
        this.multiLine = multiLine;
    }

    /**
     * Gets replace nulls.
     *
     * @return the replace nulls
     */
    public String getReplaceNulls() {
        return replaceNulls;
    }

    /**
     * Sets replace nulls.
     *
     * @param replaceNulls the replace nulls
     */
    public void setReplaceNulls(String replaceNulls) {
        this.replaceNulls = replaceNulls;
    }

    /**
     * Gets expression.
     *
     * @return the expression
     */
    public String getExpression() {
        return expression;
    }

    /**
     * Sets expression.
     *
     * @param expression the expression
     */
    public void setExpression(String expression) {
        this.expression = expression;
    }

    /**
     * Gets escape with back tick.
     *
     * @return the escape with back tick
     */
    public Boolean getEscapeWithBackTick() {
        return escapeWithBackTick;
    }

    /**
     * Sets escape with back tick.
     *
     * @param escapeWithBackTick the escape with back tick
     */
    public void setEscapeWithBackTick(Boolean escapeWithBackTick) {
        this.escapeWithBackTick = escapeWithBackTick;
    }

    /**
     * Gets escape character.
     *
     * @return the escape character
     */
    public String getEscapeCharacter() {

        if (StringUtils.EMPTY.equalsIgnoreCase(escapeCharacter)) {
            if (getEscapeWithSingleQuote()) {
                return SINGLE_QUOTE;
            }
            if (getEscapeWithDoubleQuote()) {
                return DOUBLE_QUOTE;
            }
            if (getEscapeWithBackTick()) {
                return BACK_TICK;
            }
        }

        return escapeCharacter;
    }

    /**
     * Sets escape character.
     *
     * @param escapeCharacter the escape character.
     */
    public void setEscapeCharacter(String escapeCharacter) {
        this.escapeCharacter = escapeCharacter;

        setEscapeWithSingleQuote(SINGLE_QUOTE.equalsIgnoreCase(escapeCharacter));
        setEscapeWithDoubleQuote(DOUBLE_QUOTE.equalsIgnoreCase(escapeCharacter));
        setEscapeWithBackTick(BACK_TICK.equalsIgnoreCase(escapeCharacter));
    }

    /**
     * Gets escape with single quote.
     *
     * @return the escape with single quote
     */
    public Boolean getEscapeWithSingleQuote() {
        return escapeWithSingleQuote;
    }

    /**
     * Sets escape with single quote.
     *
     * @param escapeWithSingleQuote the escape with single quote
     */
    public void setEscapeWithSingleQuote(Boolean escapeWithSingleQuote) {
        this.escapeWithSingleQuote = escapeWithSingleQuote;
    }

    /**
     * Gets escape with double quote.
     *
     * @return the escape with double quote
     */
    public Boolean getEscapeWithDoubleQuote() {
        return escapeWithDoubleQuote;
    }

    /**
     * Sets escape with double quote.
     *
     * @param escapeWithDoubleQuote the escape with double quote
     */
    public void setEscapeWithDoubleQuote(Boolean escapeWithDoubleQuote) {
        this.escapeWithDoubleQuote = escapeWithDoubleQuote;
    }

    /**
     * Gets connection url.
     *
     * @return the connection url
     */
    public String getConnectionUrl() {
        return connectionUrl;
    }

    /**
     * Sets connection url.
     *
     * @param connectionUrl the connection url
     */
    public void setConnectionUrl(String connectionUrl) {
        this.connectionUrl = connectionUrl;
    }

    /**
     * Gets user name.
     *
     * @return the user name
     */
    public String getUserName() {
        return userName;
    }

    /**
     * Sets user name.
     *
     * @param userName the user name
     */
    public void setUserName(String userName) {
        this.userName = userName;
    }

    /**
     * Gets password.
     *
     * @return the password
     */
    public String getPassword() {
        return password;
    }

    /**
     * Sets password.
     *
     * @param password the password
     */
    public void setPassword(String password) {
        this.password = password;
    }

    /**
     * Gets query.
     *
     * @return the query
     */
    public String getQuery() {
        return query;
    }

    /**
     * Sets query.
     *
     * @param query the query
     */
    public void setQuery(String query) {
        this.query = query;
    }

    /**
     * Gets connection properties.
     *
     * @return the connection properties
     */
    public Properties getConnectionProperties() {
        return connectionProperties;
    }

    /**
     * Sets connection properties.
     *
     * @param connectionProperties the connection properties
     */
    public void setConnectionProperties(Properties connectionProperties) {
        this.connectionProperties = connectionProperties;
    }

    /**
     * The enum File type.
     */
    public enum FileType {
        /**
         * Avro file type.
         */
        avro,
        /**
         * Json file type.
         */
        json,
        /**
         * Orc file type.
         */
        orc,
        /**
         * Parquet file type.
         */
        parquet,
        /**
         * Xml file type.
         */
        xml
    }
}

```

