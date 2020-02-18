---
description: API for base options OwlOptions()
---

# OwlOptions \(base\)

## OwlOptions

| Property | Description | Default value |
| :--- | :--- | :--- |
|  |  |  |
|  |  |  |

```java
package com.owl.common.options;

import com.fasterxml.jackson.annotation.JsonIgnore;
import org.apache.commons.lang3.StringUtils;

import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

/**
 * OwlOptions
 */
public class OwlOptions {

    /**
     * Dataset ID. Cannot contain [".", "-", "#", and "@"] gets replaced with "_"
     */
    public String dataset = StringUtils.EMPTY;

    /**
     * A unique runId in date format string. yyyy-MM-dd
     */
    public String runId = StringUtils.EMPTY;

    /**
     * Valid runId for executing backruns
     */
    public String runIdEnd = StringUtils.EMPTY;

    /**
     * Indicating if the
     */
    public RunState runState = RunState.DRAFT;

    /**
     * Whether the resulting OwlCheck Hoot score is above passFailLimit threshold.
     * The value of this property depends on the result of OwlCheck run.
     * TODO Most likely unnecessary in OwlOptions and is available here by accident.
     */
    public Integer passFail = 1;

    /**
     * Passing cutoff for Hoot.score. passFail = 0 if Hoot.Score < passFailLimit.
     */
    public Integer passFailLimit = 75;

    /**
     * The Job id.
     */
    public Integer jobId = 0;

    /**
     * Column names in target dataframe to link results in OwlCheck output
     */
    public String[] linkId = null;

    /**
     * The License key for Owl
     */
    public String licenseKey = StringUtils.EMPTY;

    /**
     * The Log file.
     */
    public String logFile = StringUtils.EMPTY;

    /**
     * The Log level.
     */
    public String logLevel = StringUtils.EMPTY;

    /**
     * The Hoot only.
     */
    public Boolean hootOnly = false;

    /**
     * Whether to pretty print in Hoot
     */
    public Boolean prettyPrint = true;

    /**
     * Whether to use existing dataset as template
     */
    public Boolean useTemplate = false;

    /**
     * Whether to run OwlCheck in parallel
     */
    public Boolean parallel = false;

    /**
     * Whether to show OwlCheck Plan in logs.
     */
    public Boolean plan = false;

    /**
     * Whether to save DataPreview while running Activities
     */
    public Boolean dataPreviewOff = false;

    /**
     * If true, do not enforce dataset safety rule (dataset name can repeat; usually for testing)
     * If false, enforce safety rule can be ignored (whether dataset name is unqiue)
     * Note: The booloean is negation of Props.dataSafety
     */
    public Boolean datasetSafeOff = false;

    /**
     * Observation limit for different activities.
     * Note that there are activity-specific observation limits ("limits") base on context of the activity
     * that are independent of obslimit.
     * However, at current implementation, this distinction is not very clearly leveraged in all activities (yet)
     *
     * Outliers: TODO document what it does
     * FreqPatternMining: No effect. TODO find out if this is an oversight or purposeful
     */
    public Integer obslimit = 300;

    /**
     * Metastore DB user. If empty, application properties is used
     */
    public String pgUser = StringUtils.EMPTY;

    /**
     * Metastore DB password. If empty, application properties is used
     */
    public String pgPassword = StringUtils.EMPTY;

    /**
     * Metastore DB host. If null, application properties is used
     */
    public String host = null;

    /**
     * Metastore DB port. If null, application properties is used
     */
    public String port = null;

    /**
     * Owl username
     */
    public String user = "anonymous : use -owluser";

    /**
     * Email to alert user when job is finished. No email sent if not specified.
     */
    public String alertEmail;

    /**
     * Schema score (based on DatasetScoring)
     * The value of this property depends on the result of OwlCheck run.
     * TODO Most likely unnecessary in OwlOptions and is available here by accident.
     */
    public Double schemaScore = 1.0;

    // Activities -----------------
    /**
     * The Load.
     */
    public LoadOpt load = new LoadOpt();

    /**
     * The Outlier.
     */
    public OutlierOpt outlier = new OutlierOpt();

    /**
     * The Pattern.
     */
    public PatternOpt pattern = new PatternOpt();

    /**
     * The Dupe.
     */
    public DupeOpt dupe = new DupeOpt();

    /**
     * The Profile.
     */
    public ProfileOpt profile = new ProfileOpt();

    /**
     * The Source.
     */
    public SourceOpt source = new SourceOpt();

    /**
     * The Rule.
     */
    public RuleOpt rule = new RuleOpt();

    /**
     * The Col match.
     */
    public ColMatchOpt colMatch = new ColMatchOpt();

    /**
     * The Spark.
     */
    public SparkOpt spark = new SparkOpt();

    /**
     * The Env.
     */
    public EnvOpt env = new EnvOpt();

    /**
     * The Record.
     */
    public RecordOpt record = new RecordOpt();

    /**
     * The Transforms.
     */
    public List<TransformOpt> transforms = new ArrayList<>();

    // public List<OutlierOpt> outliers;
    // public List<PatternOpt> patterns;

    @JsonIgnore
    private Date runDate = null;

    @JsonIgnore
    private Date runDateEnd = null;

    /**
     * Create default OwlOption
     */
    public OwlOptions() {
    }


    /**
     * Create default OwlOption with specified dataset id
     *
     * @param dataset dataset id
     */
    public OwlOptions(String dataset) {
        setDataset(dataset);
    }

    private Date getDateValue(String dateString, Date dateValue) {
        if (dateValue != null) {
            return dateValue;
        }
        String del = "-";
        String dateStr = dateString;
        SimpleDateFormat s1 = new SimpleDateFormat("yyyy" + del + "MM" + del + "dd");
        s1.setLenient(false);
        SimpleDateFormat s2 = new SimpleDateFormat("yyyy" + del + "MM" + del + "dd HH");
        s2.setLenient(false);
        SimpleDateFormat s3 = new SimpleDateFormat("yyyy" + del + "MM" + del + "dd HH:mm");
        s3.setLenient(false);

        if (dateStr.length() >= 16) {

            try {
                return s3.parse(dateStr);
            } catch (Exception e) {
                System.out.println("Invalid date format");
            }

        } else if (dateStr.length() >= 13) {

            try {
                return s2.parse(dateStr);
            } catch (Exception e) {
                System.out.println("Invalid date format");
            }

        } else if (dateStr.length() == 10) {
            try {
                return s1.parse(dateStr);

            } catch (Exception e) {
                System.out.println("Invalid date format");
            }
        }

        return null;
    }

    /**
     * Gets run date.
     *
     * @return the run date
     */
    public Date getRunDate() {
        Date dateValue = getDateValue(this.runId, this.runDate);
        return dateValue != null ? dateValue : new Date();
    }

    /**
     * Sets run date.
     *
     * @param runDate the run date
     */
    public void setRunDate(Date runDate) {
        this.runDate = runDate;
    }

    /**
     * Gets run date end.
     *
     * @return the run date end
     */
    public Date getRunDateEnd() {
        Date dateValue = getDateValue(this.runIdEnd, this.runDateEnd);
        return dateValue;
    }

    /**
     * Sets run date end.
     *
     * @param runDateEnd the run date end
     */
    public void setRunDateEnd(Date runDateEnd) {
        this.runDateEnd = runDateEnd;
    }

    /**
     * Gets dataset.
     *
     * @return the dataset
     */
    public String getDataset() {
        return dataset;
    }

    /**
     * Sets dataset.
     *
     * @param dataset the dataset
     */
    public void setDataset(String dataset) {
        this.dataset = dataset;
    }

    /**
     * Gets run id.
     *
     * @return the run id
     */
    public String getRunId() {
        return runId;
    }

    /**
     * Sets run id.
     *
     * @param runId the run id
     */
    public void setRunId(String runId) {
        this.runId = runId;
    }

    /**
     * Gets run id end.
     *
     * @return the run id end
     */
    public String getRunIdEnd() {
        return runIdEnd;
    }

    /**
     * Sets run id end.
     *
     * @param runIdEnd the run id end
     */
    public void setRunIdEnd(String runIdEnd) {
        this.runIdEnd = runIdEnd;
    }

    /**
     * Gets pass fail.
     *
     * @return the pass fail
     */
    public Integer getPassFail() {
        return passFail;
    }

    /**
     * Sets pass fail.
     *
     * @param passFail the pass fail
     */
    public void setPassFail(Integer passFail) {
        this.passFail = passFail;
    }

    /**
     * Gets pass fail limit.
     *
     * @return the pass fail limit
     */
    public Integer getPassFailLimit() {
        return passFailLimit;
    }

    /**
     * Sets pass fail limit.
     *
     * @param passFailLimit the pass fail limit
     */
    public void setPassFailLimit(Integer passFailLimit) {
        this.passFailLimit = passFailLimit;
    }

    /**
     * Gets job id.
     *
     * @return the job id
     */
    public Integer getJobId() {
        return jobId;
    }

    /**
     * Sets job id.
     *
     * @param jobId the job id
     */
    public void setJobId(Integer jobId) {
        this.jobId = jobId;
    }

    /**
     * Get link id string [ ].
     *
     * @return the string [ ]
     */
    public String[] getLinkId() {
        return linkId;
    }

    /**
     * Sets link id.
     *
     * @param linkId the link id
     */
    public void setLinkId(String[] linkId) {
        this.linkId = linkId;
    }

    /**
     * Gets license key.
     *
     * @return the license key
     */
    public String getLicenseKey() {
        return licenseKey;
    }

    /**
     * Sets license key.
     *
     * @param licenseKey the license key
     */
    public void setLicenseKey(String licenseKey) {
        this.licenseKey = licenseKey;
    }

    /**
     * Gets log file.
     *
     * @return the log file
     */
    public String getLogFile() {
        return logFile;
    }

    /**
     * Sets log file.
     *
     * @param logFile the log file
     */
    public void setLogFile(String logFile) {
        this.logFile = logFile;
    }

    /**
     * Gets log level.
     *
     * @return the log level
     */
    public String getLogLevel() {
        return logLevel;
    }

    /**
     * Sets log level.
     *
     * @param logLevel the log level
     */
    public void setLogLevel(String logLevel) {
        this.logLevel = logLevel;
    }

    /**
     * Gets hoot only.
     *
     * @return the hoot only
     */
    public Boolean getHootOnly() {
        return hootOnly;
    }

    /**
     * Sets hoot only.
     *
     * @param hootOnly the hoot only
     */
    public void setHootOnly(Boolean hootOnly) {
        this.hootOnly = hootOnly;
    }

    /**
     * Gets pretty print.
     *
     * @return the pretty print
     */
    public Boolean getPrettyPrint() {
        return prettyPrint;
    }

    /**
     * Sets pretty print.
     *
     * @param prettyPrint the pretty print
     */
    public void setPrettyPrint(Boolean prettyPrint) {
        this.prettyPrint = prettyPrint;
    }

    /**
     * Gets use template.
     *
     * @return the use template
     */
    public Boolean getUseTemplate() {
        return useTemplate;
    }

    /**
     * Sets use template.
     *
     * @param useTemplate the use template
     */
    public void setUseTemplate(Boolean useTemplate) {
        this.useTemplate = useTemplate;
    }

    /**
     * Gets parallel.
     *
     * @return the parallel
     */
    public Boolean getParallel() {
        return parallel;
    }

    /**
     * Sets parallel.
     *
     * @param parallel the parallel
     */
    public void setParallel(Boolean parallel) {
        this.parallel = parallel;
    }

    /**
     * Gets plan.
     *
     * @return the plan
     */
    public Boolean getPlan() {
        return plan;
    }

    /**
     * Sets plan.
     *
     * @param plan the plan
     */
    public void setPlan(Boolean plan) {
        this.plan = plan;
    }

    /**
     * Gets dataset safe off.
     *
     * @return the dataset safe off
     */
    public Boolean getDatasetSafeOff() {
        return datasetSafeOff;
    }

    /**
     * Sets dataset safe off.
     *
     * @param datasetSafeOff the dataset safe off
     */
    public void setDatasetSafeOff(Boolean datasetSafeOff) {
        this.datasetSafeOff = datasetSafeOff;
    }

    /**
     * Gets obslimit.
     *
     * @return the obslimit
     */
    public Integer getObslimit() {
        return obslimit;
    }

    /**
     * Sets obslimit.
     *
     * @param obslimit the obslimit
     */
    public void setObslimit(Integer obslimit) {
        this.obslimit = obslimit;
    }

    /**
     * Gets pg user.
     *
     * @return the pg user
     */
    public String getPgUser() {
        return pgUser;
    }

    /**
     * Sets pg user.
     *
     * @param pgUser the pg user
     */
    public void setPgUser(String pgUser) {
        this.pgUser = pgUser;
    }

    /**
     * Gets pg password.
     *
     * @return the pg password
     */
    public String getPgPassword() {
        return pgPassword;
    }

    /**
     * Sets pg password.
     *
     * @param pgPassword the pg password
     */
    public void setPgPassword(String pgPassword) {
        this.pgPassword = pgPassword;
    }

    /**
     * Gets host.
     *
     * @return the host
     */
    public String getHost() {
        return host;
    }

    /**
     * Sets host.
     *
     * @param host the host
     */
    public void setHost(String host) {
        this.host = host;
    }

    /**
     * Gets port.
     *
     * @return the port
     */
    public String getPort() {
        return port;
    }

    /**
     * Sets port.
     *
     * @param port the port
     */
    public void setPort(String port) {
        this.port = port;
    }

    /**
     * Gets user.
     *
     * @return the user
     */
    public String getUser() {
        return user;
    }

    /**
     * Sets user.
     *
     * @param user the user
     */
    public void setUser(String user) {
        this.user = user;
    }

    /**
     * Gets alert email.
     *
     * @return the alert email
     */
    public String getAlertEmail() {
        return alertEmail;
    }

    /**
     * Sets alert email.
     *
     * @param alertEmail the alert email
     */
    public void setAlertEmail(String alertEmail) {
        this.alertEmail = alertEmail;
    }

    /**
     * Gets schema score.
     *
     * @return the schema score
     */
    public Double getSchemaScore() {
        return schemaScore;
    }

    /**
     * Sets schema score.
     *
     * @param schemaScore the schema score
     */
    public void setSchemaScore(Double schemaScore) {
        this.schemaScore = schemaScore;
    }

    /**
     * Gets load.
     *
     * @return the load
     */
    public LoadOpt getLoad() {
        return load;
    }

    /**
     * Sets load.
     *
     * @param load the load
     */
    public void setLoad(LoadOpt load) {
        this.load = load;
    }

    /**
     * Gets outlier.
     *
     * @return the outlier
     */
    public OutlierOpt getOutlier() {
        return outlier;
    }

    /**
     * Sets outlier.
     *
     * @param outlier the outlier
     */
    public void setOutlier(OutlierOpt outlier) {
        this.outlier = outlier;
    }

    /**
     * Gets pattern.
     *
     * @return the pattern
     */
    public PatternOpt getPattern() {
        return pattern;
    }

    /**
     * Sets pattern.
     *
     * @param pattern the pattern
     */
    public void setPattern(PatternOpt pattern) {
        this.pattern = pattern;
    }

    /**
     * Gets dupe.
     *
     * @return the dupe
     */
    public DupeOpt getDupe() {
        return dupe;
    }

    /**
     * Sets dupe.
     *
     * @param dupe the dupe
     */
    public void setDupe(DupeOpt dupe) {
        this.dupe = dupe;
    }

    /**
     * Gets profile.
     *
     * @return the profile
     */
    public ProfileOpt getProfile() {
        return profile;
    }

    /**
     * Sets profile.
     *
     * @param profile the profile
     */
    public void setProfile(ProfileOpt profile) {
        this.profile = profile;
    }

    /**
     * Gets source.
     *
     * @return the source
     */
    public SourceOpt getSource() {
        return source;
    }

    /**
     * Sets source.
     *
     * @param source the source
     */
    public void setSource(SourceOpt source) {
        this.source = source;
    }

    /**
     * Gets rule.
     *
     * @return the rule
     */
    public RuleOpt getRule() {
        return rule;
    }

    /**
     * Sets rule.
     *
     * @param rule the rule
     */
    public void setRule(RuleOpt rule) {
        this.rule = rule;
    }

    /**
     * Gets col match.
     *
     * @return the col match
     */
    public ColMatchOpt getColMatch() {
        return colMatch;
    }

    /**
     * Sets col match.
     *
     * @param colMatch the col match
     */
    public void setColMatch(ColMatchOpt colMatch) {
        this.colMatch = colMatch;
    }

    /**
     * Gets spark.
     *
     * @return the spark
     */
    public SparkOpt getSpark() {
        return spark;
    }

    /**
     * Sets spark.
     *
     * @param spark the spark
     */
    public void setSpark(SparkOpt spark) {
        this.spark = spark;
    }

    /**
     * Gets env.
     *
     * @return the env
     */
    public EnvOpt getEnv() {
        return env;
    }

    /**
     * Sets env.
     *
     * @param env the env
     */
    public void setEnv(EnvOpt env) {
        this.env = env;
    }

    /**
     * Gets record.
     *
     * @return the record
     */
    public RecordOpt getRecord() {
        return record;
    }

    /**
     * Sets record.
     *
     * @param record the record
     */
    public void setRecord(RecordOpt record) {
        this.record = record;
    }

    /**
     * Gets data preview off.
     *
     * @return the data preview off
     */
    public Boolean getDataPreviewOff() {
        return dataPreviewOff;
    }

    /**
     * Sets data preview off.
     *
     * @param dataPreviewOff the data preview off
     */
    public void setDataPreviewOff(Boolean dataPreviewOff) {
        this.dataPreviewOff = dataPreviewOff;
    }

    /***
     * Gets run state.
     * @return the run state.
     */
    public RunState getRunState() {
        return runState;
    }

    /**
     * Sets run state.
     *
     * @param runState the run state.
     */
    public void setRunState(RunState runState) {
        this.runState = runState;
    }

    public void setRunState(String runState) {
        this.runState = RunState.valueOf(runState);
    }

    public enum RunState {

        DRAFT {
            @Override
            public String toString() {
                return "DRAFT";
            }
        },
        DRY {
            @Override
            public String toString() {
                return "DRY";
            }
        },
        CERTIFIED {
            @Override
            public String toString() {
                return "CERTIFIED";
            }
        }
    }
}

```



