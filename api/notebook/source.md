# Source



```java
public class SourceOpt {

    public Boolean on = false;              //-vs
    public Boolean only = false;            //-sourceonly
    public Boolean validateValues = false;  //-validatevalues
    public Boolean matches = false;         //-matches

    public String[] include;               //-valinc
    public String[] exclude;               //-valexc
    public String[] key;                    //valkey
    public Map<String, String> map;         //
    public Double score = 1.0;              // points per validate source found, default 1-5
    public Integer limit = 30;              //-valsrclimit
    public String delimiter = ",";          //-srcdel
    public String fileCharSet = "UTF-8";     //-srcencoding
    public String filePath = StringUtils.EMPTY; //--srcfile

    public String header = null;            //-srcheader
    public String dataset = StringUtils.EMPTY;
    public String driverName = StringUtils.EMPTY;
    public String user = StringUtils.EMPTY;
    public String password = StringUtils.EMPTY;
    public String passwordManager = StringUtils.EMPTY;
    public String connectionName = StringUtils.EMPTY;
    public String connectionUrl = StringUtils.EMPTY;
    public String query = StringUtils.EMPTY;
    public String fileQuery = StringUtils.EMPTY;
    public String lib = StringUtils.EMPTY;
    public Properties connectionProperties;
```

