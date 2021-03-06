# Owl's Scorecard and 9 Dimensions of DQ

## Scorecard

![OwlCheck Score Card](.gitbook/assets/image-2.png)



Owl provides a data quality assessment that that scans 9 dimensions of a data set to assure the integrity of that data. The 9 dimensions are behavior, rules, outliers, pattern, source, record, schema, duplicates, and shapes. OwlCheck produces a data quality score from 0-100. 100 represents that there were no integrity issues found in the data set. The score numerically represents the integrity of that data. For example, the score of 100 would tell the data analyst that zero data quality issues in that data set.

Owl will scan your data with the same frequency, that you load your data - Owl scans 9 dimensions of DQ out of the box 

**1. Behavior - imagine a column going null, automatic row count checks - does you data behave/look/feel the same way it has in the past** 

![](.gitbook/assets/behavior.jpg)

**2. Rules - assures only values compliant with your data rules are allowed within a data object** 

![](.gitbook/assets/rules.jpg)

**3. Outliers - data point that differs significantly from other observations** 

![](.gitbook/assets/outliers.jpg)

**4. Pattern - recognizing relevant patterns between data examples** 

![](.gitbook/assets/pattern.jpg)

**5. Source- validating source to target accuracy** 

![](.gitbook/assets/source.jpg)

**6. Record - deltas for a given column** 

![](.gitbook/assets/record.jpg)

**7. Schema - columns dropped** 

![](.gitbook/assets/schema.jpg)

8. Dupes - fuzzy matching to identify entries that have been added multiple times with similar but not exact detail 

![](.gitbook/assets/dupes.jpg)

**9. Shapes - infrequent formats**

![](.gitbook/assets/shapes.jpg)

## List View with Impact Analysis

![](.gitbook/assets/list-view-with-impact.jpg)

