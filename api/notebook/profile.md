# Profile



```java
public class ProfileOpt {

    public Boolean on = true;         //Whether to run profile
    public Boolean only = false;      //Whether to run only profile
    public String[] include;          //Which columns to include
    public String[] exclude;          //Which columns to exclude
    public Boolean shape = true;      //Disable shape detection
    public Boolean correlation = null;//On/Off Pearsons Correlation, null=auto
    public Boolean histogram = null;  //On/Off Histograming, null=auto
    public Boolean semantic = null;   //On/Off Semantic discovery, null=auto     

    public Integer limit = 300;
    public Integer histogramLimit = 0;
    public Double score = 1.0;         //downscore points per Shape issue
    public Integer shapeTotalScore = 0;
    public Double shapeSensitivity = 0.00;
    public Integer shapeMaxPerCol = 0;
    public Integer shapeMaxColSize = 0;
    public String behavioralDimension = StringUtils.EMPTY;
    public String behavioralDimensionGroup = StringUtils.EMPTY;
    public String behavioralValueColumn = StringUtils.EMPTY;
    public Boolean behaviorScoreOff = false;  // disable behavior scoring  
```

