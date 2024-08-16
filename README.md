# TABLEAU  |  Fraudulent Transaction Dashboard

<div class='tableauPlaceholder' id='viz1723789646306' style='position: relative'><noscript><a href='#'><img alt='Dashboard 1 ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Fr&#47;FraudulentTransactionsDashboard&#47;Dashboard1&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='FraudulentTransactionsDashboard&#47;Dashboard1' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Fr&#47;FraudulentTransactionsDashboard&#47;Dashboard1&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /><param name='filter' value='publish=yes' /></object></div>  
&ensp;

### Project Overview
This Tableau dashboard project aims to present the findings and key insights in an easy-to-understand way.  
&ensp;

### Steps
1. Copied each queried output from MS SQL Server, pasted it into an Excel sheet, and created four separate sheets.
2. Imported the data into Tableau Public and created visualizations for each dataset.
3. Compiled the visualizations into a dashboard and organized them to present the findings.  
&ensp;

### SQL Queries
The following SQL queries were used to extract data for this Fraudulent Transaction Dashboard project.  
&ensp;

**Query 1.**
```sql
-- Q4. Did the fraud transaction rate decreased over the year?
-- Let's see the percentage of fraud transaction commpare to the entire transaction per year.

select trans_year, count(*) as total_trans, 
sum(case when is_fraud = 'Yes' then 1 else 0 end) as total_fraud_trans,
(sum(case when is_fraud = 'Yes' then 1 else 0 end)*100 / count(*)) as fraud_percentage
from DataCleaningProject.dbo.fraud_data
group by trans_year
order by trans_year
```  
⬇️ This shows the yearly statistics of fraudulent transaction numbers.  

![Tableau 1](https://github.com/user-attachments/assets/d29345cd-ba81-47d7-85f6-6dbdab1f40b8)  
&nbsp;
**Findings**: <br/>
There is little difference between the numbers for 2019 and 2020. <br/>
The occurrence of fraudulent transactions decreased by only 1% from 2019.  
&ensp;

              
---             


**Query 2.**
```sql
-- Q2. Are older people more likely to be targeted? 
-- Is there a correlation between age and the occurrence of fraud transactions?

select age, sum(amt) as total_amt, count(trans_date_trans_time)
from DataCleaningProject.dbo.fraud_data
where is_fraud = 'Yes'
group by age
order by 1 desc
```  
⬇️ This bar chart displays the total count of fraudulent transactions for each age group.  

![Tableau 2](https://github.com/user-attachments/assets/badff26a-d811-471d-91df-17c1f6184569)  

**Findings**: The 30s to 50s age group experienced three times more fraudulent transactions than the 70s and 80s age group.  
&ensp;


---


**Query 3.**
```sql
-- Q5. Is there a correlation between transaction hours and occurrence?

select DATEPART(HOUR, trans_date_trans_time) as trans_hour, count(is_fraud) as fraud_count
from DataCleaningProject.dbo.fraud_data
where is_fraud = 'Yes'
group by DATEPART(HOUR, trans_date_trans_time)
order by 2 desc
```
⬇️ This line chart displays the total count of fraudulent transactions by hour.

![Tableau 3](https://github.com/user-attachments/assets/405bfa41-d626-4319-8ab5-0c04670e1f5d)

**Findings**: Most fraudulent transactions occurred between 10 p.m. and 3 a.m., when most people are asleep.  
&ensp;


---


**Query 4.**
```sql
-- Q6. Which categories have the highest percentage of fraud transactions compare to total transactions?

select category, count(*) as total_trans,
sum(case when is_fraud = 'Yes' then 1 else 0 end) as fraud_trans,
(sum(case when is_fraud = 'Yes' then 1 else 0 end) * 100 / count(*)) as fraud_percentage
from DataCleaningProject.dbo.fraud_data
group by category
order by 4 desc
```
⬇️







