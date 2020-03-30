# Bank Loans

It is common for banks to lend money in return for monthly payments with interest.  However to do so a bank must make sure that the applications are valid and wellformed to begin the underwriting and approval process.  Below we will apply some basic lending concepts to OwlDQ. 

1. Credit Score Validation
2. SSN Validation
3. Loan to Value Validation
4. Interest Rate Validation
5. Duplicate Loan Applications
6. Loan Amount Validation
7. Loan Completeness Validation

## 1. Credit Score

<table>
  <thead>
    <tr>
      <th style="text-align:left">Business Check</th>
      <th style="text-align:left">OwlDQ Feature</th>
      <th style="text-align:left">Manual vs Auto</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Is the credit score a whole number</td>
      <td style="text-align:left">BEHAVIOR</td>
      <td style="text-align:left">AUTO</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Is the credit score within a valid range</p>
        <p>(between 300 - 850)</p>
      </td>
      <td style="text-align:left">RULE</td>
      <td style="text-align:left">credit_score between 300 and 850</td>
    </tr>
    <tr>
      <td style="text-align:left">Is the credit score NULL or Missing</td>
      <td style="text-align:left">BEHAVIOR</td>
      <td style="text-align:left">AUTO</td>
    </tr>
  </tbody>
</table>##  2. SSN Validation

| Business Check | OwlDQ Feature |  |
| :--- | :--- | :--- |
| Is a valid formatted SSN | RULE | AUTO-SSN detection |
| SSN is PII | SENSITIVITY | AUTO-SSN labeled |
| Is the SSN NULL or Missing | BEHAVIOR | AUTO |
| Does the SSN belong to the Applicant | PATTERN | SSN -&gt; first\_name, last\_name |

## 3. Loan to Value 

<table>
  <thead>
    <tr>
      <th style="text-align:left">Business Check</th>
      <th style="text-align:left">OwlDQ Feature</th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Is Loan amount and</p>
        <p>asset value (home or auto) valid numbers</p>
      </td>
      <td style="text-align:left">BEHAVIOR</td>
      <td style="text-align:left">AUTO</td>
    </tr>
    <tr>
      <td style="text-align:left">95% loan to value ratio to approve</td>
      <td style="text-align:left">RULE</td>
      <td style="text-align:left">loan / asset_value &lt; .95</td>
    </tr>
  </tbody>
</table>## 4. Interest Rate

<table>
  <thead>
    <tr>
      <th style="text-align:left">Business Check</th>
      <th style="text-align:left">OwlDQ Feature</th>
      <th style="text-align:left"></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">
        <p>Interest rate between</p>
        <p>min and max allowable range</p>
        <p>for the loans credit rating.</p>
      </td>
      <td style="text-align:left">RULE COMPLEX</td>
      <td style="text-align:left">
        <p>loan l join rates r on l.credit_rating = r.credit_rating</p>
        <p>where l.rate between r.min_rate and r.max_rate</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>## 5. Duplicate Loan Applications

Can't give someone the same loan twice!

| Business Check | OwlDQ Feature | Manual vs Auto |
| :--- | :--- | :--- |
| Ensure we don't issue the same loan twice | DUPE | first\_n, last\_n, SSN, Address |

## 6. Loan Amount

<table>
  <thead>
    <tr>
      <th style="text-align:left">Business Check</th>
      <th style="text-align:left">OwlDQ Feature</th>
      <th style="text-align:left">Manual vs Auto</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Loan Amount within lendable range</td>
      <td style="text-align:left">OUTLIER</td>
      <td style="text-align:left">AUTO</td>
    </tr>
    <tr>
      <td style="text-align:left">
        <p>Loan Amount within lendable range</p>
        <p>only lend money between 50K and 3M</p>
      </td>
      <td style="text-align:left">RULE</td>
      <td style="text-align:left">loan_amount between 50000 and 3000000</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>