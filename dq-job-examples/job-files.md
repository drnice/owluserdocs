# DQ Job Files

For example, a large file `transaction_2021-01-01.csv` might contain the following transaction data with two transaction per day spanning all of January.

| transaction\_id | account\_id | date | amount |
| :--- | :--- | :--- | :--- |
| 1 | 1 | 2021-01-01 | 100 |
| 2 | 2 | 2021-01-01 | 120 |
| 3 | 1 | 2021-01-02 | 90 |
| 4 | 2 | 2021-01-02 | 115 |
| ... |  | ... | ... |
| 61 | 1 | 2021-01-31 | 100 |
| 62 | 2 | 2021-01-31 | 999 |

and this file might be located on the directory `~/customer/transaction-2021-01-01/`. 

```bash
~/customer
  ├── transaction-2021-01-01
  │   └── transaction_2021-01-01.csv
  ├── transaction-2021-02-01
  │   └── transaction_2021-02-01.csv
  ... # folders for 2021-03-01 to 2021-11-01 ommitted
  ├── transaction-2021-12-01
  │   └── transaction_2021-12-01.csv
```

Other folders with similar pattern may exist in your directory, such as `~/customer/transaction-2021-02-1`. Note that February data is located in a separate directory with a similar pattern for all the months of 2021. This dataset could similarly have 2 account IDs and 1 transaction per account per day \(= 28 x 2 = 56 rows of data\). For this example, let's assume this is the case for all the files.

To run an Owlcheck on this single file containing multiple dates, you have the following choices.

## Owlchecks with **file** 

**1. Run an Owlcheck on all the rows in a single file.**

```bash
./owlcheck 
    -ds DQCheck_transactions_jan21
    -rd "2021-01-01"
    -f "~/customer/transaction-2021-01-01/transaction_2021-01-01.csv"
    -fq "select * from dataset"
    ... # other relevant options
```

Here we assume that run date \(`-rd`\) is "2021-01-01" because it is currently January 1, 2021.  
  
The above command would lead to an Owlcheck on 62 rows of data spanning all of January 2021 from a single file located at `~/customer/transaction-2021-01-01/transaction_20210101.csv`.   
  
If you were to schedule a job to run this job monthly and next job ran on February 1st, 2021, then same DQ checks will be performed on the **same set of 62 rows** with same score as your Owlcheck run from January 1, 2021.  
  
 For example, the follow-up scheduled job running on February 1st, 2021 would be:

```bash
./owlcheck 
    -ds DQCheck_transactions_jan21
    -rd "2021-02-01"
    -f "~/customer/transaction-2021-01-01/transaction_2021-01-01.csv"
    -fq "select * from dataset"
    ... # other relevant options
```

  
This type of Owlcheck on a single file is suitable if you are verifying a static file `~/customer/transaction-2021-01-01/transaction_20210101.csv` that does not change over time and expect the score to be the same every run. Hence, it is suggested to name the dataset that reflect this, such as `DQCheck_transaction_jan21` to reflect the idea that this dataset is checking the Data Quality of transaction table containing January 2021 data. Similar Owlcheck for February 2021 data would then be a separate and independent dataset named `DQCheck_transaction_feb21`  
  
This type of Owlcheck can also be used if `~/customer/transaction-2021-01-01/transaction_20210101.csv` is changing \(the rows are changing values or new rows are being added\) and want to detect data quality changes. Transaction file doesn't fit with this scenario, but the idea is that the above command specifies Data Quality Owlchecks on the entirety of the file. The run date is a date that you choose to assign for that Owlcheck. It is conventional to have one-to-one mapping between run date and the date corresponding to the date that DQ checks are being performed. Run date does not have to match with the data underlying the file.

**2. Run an Owlcheck on subset of rows from a single file**

The single file contains daily data for January of 2021. To run Data Quality checks on January 1st, January 2nd, ... , and January 31st, you need to run 31 Owlchecks, each with subset of rows from the file. Note the `where` clause in `-fq` matching with the run date `-rd` 

```bash
./owlcheck 
    -ds DQCheck_transactions_jan21
    -rd "2021-01-01"
    -f "~/customer/transaction-2021-01-01/transaction_2021-01-01.csv"
    -fq "select * from dataset where date = '2021-01-01'"
    ... # other relevant options

./owlcheck 
    -ds DQCheck_transactions_jan21
    -rd "2021-01-02"
    -f "~/customer/transaction-2021-01-01/transaction_2021-01-01.csv"
    -fq "select * from dataset where date = '2021-01-02'"
    ... # other relevant options

... # Owlchecks for -rd 2021-01-03 to 2021-01-30 ommitted

./owlcheck 
    -ds DQCheck_transactions_jan21
    -rd "2021-01-31"
    -f "~/customer/transaction-2021-01-01/transaction_2021-01-01.csv"
    -fq "select * from dataset where date = '2021-01-31'"
    ... # other relevant options
    
```

By using the same dataset name `-ds`, all 31 Owlchecks will appear under one dataset `DQCheck_transaction_jan21` in the Hoot page.

A convenient way to parameterize this run date is to use `${rd}` in the query.

```bash
./owlcheck 
    -ds DQCheck_transactions_jan21
    -rd "2021-01-01"
    -f "~/customer/transaction-2021-01-01/transaction_2021-01-01.csv"
    -fq "select * from dataset where date = '${rd}'"
    ... # other relevant options

```

A daily scheduled job starting on January 1st, 2021 to January 31, 2021 will automatically replace the `${rd}` with "2021-01-01", "2021-01-02", ... , and "2021-01-31" for the respective run date.

**3. Run an Owlcheck on subset of rows from a single file with day lookback**

For certain core components like **Outlier**, a set of rows corresponding to historical training data can be used to establish a baseline. For example, the row with `transaction_id` 62 has amount of 999. This looks like an outlier that we want to catch. This value of 999 seems to be an outlier because past transaction amounts for `account_id`2 are in the 100s range. We can use historical data from January 15th to January 30th and use that info to see if January 31st data contains any outliers.   
  
In this scenario, our single file `~/customer/transaction-2021-01-01/transaction_2021-01-01.csv` contains such historical data because that file contains all the data for all of January. How do we use the same file for both current data \(January 31st\) and historical \(January 15th to January 30th\) data? You do not have to split the files into two. You can simply do exactly what you would do for Owlcheck on "2021-01-31" with a `-fullfile` flag. The `-fullfile` flag tells the Owlcheck that "the file in `-f` contains the historical data. Construct a query and subset those rows for me".

```bash
./owlcheck 
    -ds DQCheck_transactions_jan21
    -rd "2021-01-31"
    -f "~/customer/transaction-2021-01-01/transaction_2021-01-01.csv"
    -fq "select * from dataset where date = '2021-01-31'"
    -fullfile
    # outlier options
    -dc "date"
    -dl
    -tbin "DAY" # look back time bin is day
    -dllb 15 # look back up to 15 days
    ... # other relevant options
```

## Owlchecks with _multiple files_

**4. Run an Owlcheck on a single file with lookback using series of file**

Recall our folder structure:

```bash
~/customer
  ├── transaction-2021-01-01
  │   └── transaction_2021-01-01.csv
  ├── transaction-2021-02-01
  │   └── transaction_2021-02-01.csv
  ... # ommitted for space
  ├── transaction-2021-12-01
  │   └── transaction_2021-12-01.csv
```

If we want to run an Owlcheck for December of 2021 and use July of 2021 to November of 2021 as our historical training dataset, how can we load _multiple_ _files_? Just like how `-fullfile` provides a convenient way to create historical training dataset on a single file, `-fllb` \(file lookback\) provides a convenient way to load _series of files_ with patterns while still pointing to the target file \(December file\) in `-f`

```bash
./owlcheck 
    -ds DQCheck_transactions_dec21
    -rd "2021-12-01"
    -f "~/customer/transaction-2021-12-01/transaction_2021-12-01.csv"
    -fq "select * from dataset"
    -fllb
    # outlier options
    -dc "date"
    -dl
    -tbin "MONTH" 
    -dllb 5 # look back up to 5 months
    ... # other relevant options
```

One caveat to this `-fllb` method __is that the Owlcheck history must be "primed" first so that the OwlDQ knows the file path of the past series of files. In fact, `-fllb` does not use the file path provided in `-f` and loads different files from different folders. _It relies on the Owlcheck history_ under the same `-ds` name. `-fllb` means lookback up to N number of past consecutive Owlchecks. For each of those past Owlcheck, look up the file path `-f` used in the past and follow those paths. The number N is determined by the maximum number of lookbacks from Outlier \(`-dllb`\) and Patterns \(`-fpglb` \). In the Owlcheck above, because `-dllb 5` is provided along with `-fllb`, it means "Look up 5 past owlchecks and load those files as historical dataset".  
  
In summary, in order to run an Owlcheck on "2021-12-01" and have that Owlcheck for that date "look up" the files in     
  `~/customer/transaction-2021-07-01/transaction_2021-07-01.csv` ,  
  `~/customer/transaction-2021-08-01/transaction_2021-08-01.csv` ,  
  `~/customer/transaction-2021-09-01/transaction_2021-09-01.csv` ,  
  `~/customer/transaction-2021-10-01/transaction_2021-10-01.csv` , and  
  `~/customer/transaction-2021-11-01/transaction_2021-11-01.csv` ,   
  
you need to have ran Owlchecks for "2021-07-01", "2021-08-01", ... , and "2021-11-01" under the same dataset name. Therefore, it would be more logical, best-practice is to name the dataset  `-ds DQCheck_transaction_2021` and run series of monthly owlchecks up to "2021-12-01" \(but the name of the dataset is up to you\)/

```bash
# Prime past Owlchecks so that "2021-12-01" knows the file path of past months
./owlcheck 
    -ds DQCheck_transactions_2021
    -rd "2021-07-01"
    -f "~/customer/transaction-2021-07-01/transaction_2021-07-01.csv"
    -fq "select * from dataset"
    
./owlcheck 
    -ds DQCheck_transactions_2021
    -rd "2021-08-01"
    -f "~/customer/transaction-2021-08-01/transaction_2021-08-01.csv"
    -fq "select * from dataset"

    
./owlcheck 
    -ds DQCheck_transactions_2021
    -rd "2021-09-01"
    -f "~/customer/transaction-2021-08-01/transaction_2021-09-01.csv"
    -fq "select * from dataset"
    
./owlcheck 
    -ds DQCheck_transactions_2021
    -rd "2021-10-01"
    -f "~/customer/transaction-2021-08-01/transaction_2021-10-01.csv"
    -fq "select * from dataset"

./owlcheck 
    -ds DQCheck_transactions_2021
    -rd "2021-11-01"
    -f "~/customer/transaction-2021-11-01/transaction_2021-11-01.csv"
    -fq "select * from dataset"
    
# Priming 5 past Owlchecks complete. Now run the 2021-12-01
./owlcheck 
    -ds DQCheck_transactions_2021
    -rd "2021-12-01"
    -f "~/customer/transaction-2021-12-01/transaction_202-11-201.csv"
    -fq "select * from dataset"
    -fllb
    # outlier options
    -dc "date"
    -dl
    -tbin "MONTH" 
    -dllb 5 # look back up to 5 months
    ... # other relevant options
```

In this scenario, since the folder paths have a pattern, we can use `-br` for priming in one command instead of writing 5 Owlcheck commands. The flag `-br` runs Owlchecks consecutively from the past and increments by monthly if `-tbin "MONTH"` \(by default `-tbin DAY`so the default behavior is to increment daily\). The different folder paths on each past consecutive run dates are replaced with `${rd}`.  
  
The below command is identical to the above

```bash
# Prime past Owlchecks so that "2021-12-01" knows the file path of past months
./owlcheck 
    -ds DQCheck_transactions_2021
    -rd "2021-12-01"
    -f "~/customer/transaction-${rd}/transaction_${rd}.csv"
    -fq "select * from dataset"
    -br 5 # run 5 runs to in the past
    -tbin "MONTH" # <-- required since we want a MONTHLY backrun. Default "DAY"
    
# Priming complete. Now run the 2021-12-01
./owlcheck 
    -ds DQCheck_transactions_2021
    -rd "2021-12-01"
    -f "~/customer/transaction-2021-12-01/transaction_2021-12-01.csv"
    -fq "select * from dataset"
    -fllb
    # outlier options
    -dc "date"
    -dl
    -tbin "MONTH" 
    -dllb 5 # look back up to 5 months
    ... # other relevant options
```

This pattern is designed so that a single Owlcheck command can be scheduled and `${rd}` be used to replace the folder & file path. Your `~/customer` folder could contain transactions for all the years, spanning all the way back to 1992 and into the future like so:

```bash
~/customer

  ├── transaction-1992-01-01
  │   └── transaction_1992-01-01.csv
  ├── transaction-1992-01-01
  │   └── transaction_1992-01-01.csv
  ... # ommitted for space
  ├── transaction-2021-01-01
  │   └── transaction_2021-01-01.csv
  ├── transaction-2021-02-01
  │   └── transaction_2021-02-01.csv
  ... # ommitted for space
  ├── transaction-2021-12-01
  │   └── transaction_2021-12-01.csv
  ... # hasn't happened yet!
  
```

In this scenario, a monthly scheduled job would get rid of the need to "prime" the Owcheck history, since your past scheduled jobs would have already ran the past Owlchecks.

