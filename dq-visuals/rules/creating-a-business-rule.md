# Creating a Business Rule

Navigate to the Rule page as shown in the screenshot below. By selecting the ![https://lh5.googleusercontent.com/EdHKN\_wQnh2JhRjtF4ueQZzi8FZiWyYcCHgDsM2NsDNH8uFIdiVsoo5051CFpOTY9YbucVEZVCNrWf8VZ1EymiKc5zEKWOIheRNI25mi\_dK6mtBJwgF7yHbbtIM\_Hr3e4d\_k\_XfS](https://lh5.googleusercontent.com/EdHKN_wQnh2JhRjtF4ueQZzi8FZiWyYcCHgDsM2NsDNH8uFIdiVsoo5051CFpOTY9YbucVEZVCNrWf8VZ1EymiKc5zEKWOIheRNI25mi_dK6mtBJwgF7yHbbtIM_Hr3e4d_k_XfS) icon on the top left corner under the Owl icon and select “Rule”. You will see a page as shown below. NOTE: You can get to rules from the DatasetStats page by clicking on Rules under the dataset name and score in the top right of the screen.‌

1. Select a rule type using the dropdown menu.                                                                ![Screen Shot 2019-05-03 at 1.02.30 PM.png](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Rules/WebHome/Screen%20Shot%202019-05-03%20at%201.02.30%20PM.png?width=530&height=366)
2. Search for a dataset name \(that has been Owlcheck’ed - or this information will be auto-populated if coming from a DatasetStat page\). Once a dataset has been loaded the schema on the left will get populated. \(Example: begin typing in shape\_example dataset from the demo.sh script we ran earlier in this document when the dataset if found click “Load”\). 

   ![](../../.gitbook/assets/image%20%2820%29.png)

3. Select a rule type using the dropdown menu                                             ![Screen Shot 2019-05-03 at 1.02.30 PM.png](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Rules/WebHome/Screen%20Shot%202019-05-03%20at%201.02.30%20PM.png?width=530&height=366)
4. Select a rule name. \(Note: If applying a preset rule, the rule name will be auto populated.\)

   ​![Screen Shot 2019-05-03 at 1.03.55 PM.png](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Rules/WebHome/Screen%20Shot%202019-05-03%20at%201.03.55%20PM.png?width=487&height=188)​

5. If applying a simple, freeform sql, or function rule type, provide a value in the condition/sql/function input field. NOTE: keystroke ctrl+space will provide intellisense.

   ​![Screen Shot 2019-05-03 at 1.04.56 PM.png](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Rules/WebHome/Screen%20Shot%202019-05-03%20at%201.04.56%20PM.png?width=637&height=224)​

6. Input a points and percentage value and click submit to save the rule.

   ​![Screen Shot 2019-05-03 at 1.06.53 PM.png](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Rules/WebHome/Screen%20Shot%202019-05-03%20at%201.06.53%20PM.png?width=459&height=222)​

‌The rule will be applied to the next Owlcheck run on that particular dataset.‌

#### **Rule Types** <a id="HRuleTypes"></a>

1. When to use a simple rule:
   1. Simple rules would be applied to filter a condition on a single column in a single table.
   2. Example: city = 'Baltimore'
2. When to use a freeform sql rule:
   1. ​Complex \(freeform sql\) would be used when applying a condition across multiple tables/columns and generally when more flexibility/customization is desired.
   2. ​Example: select \* from dataset where name = 'Owl'
3. When to use a preset rule:
   1. Preset rules would be used for quickly adding strict condition check. Commonly used conditions are available to add to any dataset columns.‌

All built-in spark functions are available to use. \([https://spark.apache.org/docs/2.3.0/api/sql/](https://spark.apache.org/docs/2.3.0/api/sql/)\) for simple and freeform sql rules.‌

#### **Points and Percentage** <a id="HPointsandPercentage"></a>

For every percentage the X condition occurs, deduct Y points from the data quality score. If a rule was triggered 10 times out of 100 rows, break records occurred 10% of the time. If you input 1 point for every 1 percent, 10 points would be deducted from the overall score.‌

#### **Creating Your First Rule** <a id="HCreatingYourFirstRule"></a>

Let’s create a simple rule using the below information. The dataset name.

![](http://18.204.201.140:8080/xwiki/bin/download/Documentation/Admin%20Guide/Rules/WebHome/Screen%20Shot%202019-05-07%20at%2010.19.28%20AM.png?width=544&height=249)

1. Search for “shape\_example” and click “Load”
2. Select “Simple Rule”
3. Rule Name = lnametest
4. @shape\_example.lname = “hootbeck” \(should hit one time day over day\).
5. Points = 1
6. Percentage = 1
7. Click “Submit”

Once the rule has been submitted please find the below list of rules with the new rule we just defined as shown below.

![](../../.gitbook/assets/image%20%2831%29.png)

#### **Seeing Your First Rule Get Triggered** <a id="HSeeingYourFirstRuleGetTriggered"></a>

‌Click on the Owl icon ![https://lh4.googleusercontent.com/AAIhzcT5BnElFn6nenaXJWlDb8qAe8jcbStZescfGaULYy2zzgq44\_AZpPQzLbIVKcRVlzm1Fvy7j5Sz9oJyRrsNW5ONiJWLMD02EE22U35AFYS\_YKcR4Gef-P5nXW8eGpTcEYuL](https://lh4.googleusercontent.com/AAIhzcT5BnElFn6nenaXJWlDb8qAe8jcbStZescfGaULYy2zzgq44_AZpPQzLbIVKcRVlzm1Fvy7j5Sz9oJyRrsNW5ONiJWLMD02EE22U35AFYS_YKcR4Gef-P5nXW8eGpTcEYuL)on the top left hand side of the owl-web application. This brings us to the score cards. Now in the “Demo Score Card” select the cell labeled “99“ that intersects “shape\_example” on the y-axis and “2018-10-04” on the x-axis. If you do not have the demo score card please follow along in section entitled “Browsing to the DQ Score Cards” of this document.‌

Scroll down to the Actions section and show the panel by clicking the ![https://lh6.googleusercontent.com/nY1mGh2J3Q0WkRvkerLjTOXgjZX37mhny7OFRDVOJKQSpViKhzMIw1fKSZ3L1mFxOwXZx1GemkFooib8GaW65L4ng0bBUCE3t-8a-EPxa30BpkK49NwlPW92cc9gV6gl1\_IBan1h](https://lh6.googleusercontent.com/nY1mGh2J3Q0WkRvkerLjTOXgjZX37mhny7OFRDVOJKQSpViKhzMIw1fKSZ3L1mFxOwXZx1GemkFooib8GaW65L4ng0bBUCE3t-8a-EPxa30BpkK49NwlPW92cc9gV6gl1_IBan1h) symbol. As shown in the below screenshot.

![](../../.gitbook/assets/image%20%2810%29.png)

1. Click history to expose the command used
2. Copy the history into the Template text box \(everything to the right of the Owlcheck command itself\)
3. Click Unlock
4. Click Save \(to save the template. NOTE we didn’t use any Template values. The generic date in the ${rd} textbox is just a greyed out value that will not be used\).
5. Click Run to execute the Owlcheck.
6. When complete hit the refresh button on the Browser.

‌

See that the Rule has now been and shows under DQ items as shown below.

![](../../.gitbook/assets/image%20%2823%29.png)

