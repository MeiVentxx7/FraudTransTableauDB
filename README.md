# TABLEAU  |  Fraudulent Transaction Dashboard

### Table of Contents
- [Project Overview](#project-overview)
- [Steps](#steps)
- [SQL Queries](#sql-queries)
- [Key Takeaways](#key-takeaways)
- [Recommendations](#recommendations)  
&ensp;  


![Dashboard 1](https://github.com/user-attachments/assets/28de8a8b-0749-4974-a9fc-f607eba81430)
[Check the dashboard in Tableau Public](https://public.tableau.com/views/FraudulentTransactionsDashboard/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)  
&ensp; 


### Project Overview
This fraudulent transaction dashboard project aims to present the findings from the SQL-based exploratory data analysis of fraud transaction data in an easy-to-understand way.
By analyzing various aspects of the fraud transaction data, we seek to reduce the risk of fraudulent transactions and enhance overall security.  
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
⬇️ This column chart displays the total count of fraudulent transactions for each age group.  

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
⬇️ This bar chart shows the total count of fraudulent transactions for each category.

![Tableau 4](https://github.com/user-attachments/assets/755d0473-b6ef-4406-966c-589877e8cba4)

**Findings**: Top 3 purchase category: grocery_pos, shopping_net, misc_net.  
&ensp;


---


### Key Takeaways
- The numbers did not show an improvement in reducing the risk of fraudulent transactions from 2019 to 2020.
- Fraudulent transactions occurred mostly among middle-aged people (30-50).
- Most fraudulent transactions occurred between 10 p.m. and 3 a.m., when most people are asleep.
- The top three purchase categories for fraudulent transactions are grocery_pos, shopping_net, misc_net.  
&ensp;


### Recommendations

Based on the analysis results, individuals and banks can take several steps to prevent fraudulent transactions:

1. Targeted Awareness and Education:

- For Individuals: Educate middle-aged people (30-50) about common fraud tactics and best practices for online security.
- For Banks: Provide targeted awareness campaigns for this age group, highlighting common scams and preventative measures.  
&ensp;


2. Enhanced Monitoring During Vulnerable Hours:

- For Banks: Implement enhanced fraud detection and monitoring systems during peak hours of 10 p.m. to 3 a.m. to identify suspicious activities more effectively.
- For Individuals: Encourage monitoring of accounts and transactions more frequently during these hours.  
&ensp;


3. Security Measures for Top Purchase Categories:

- For Banks: Strengthen security measures for transactions in the top categories identified (e.g., grocery, shopping net) by implementing advanced fraud detection algorithms and transaction monitoring.
- For Individuals: Be cautious when making transactions in these categories, especially online, and use secure payment methods.  
&ensp;

4. Fraud Detection Technology:

- For Banks: Invest in advanced fraud detection technologies that use machine learning and data analytics to identify and prevent fraudulent transactions more accurately.
- For Individuals: Use banks that offer robust fraud detection and protection services.  
&ensp;



**Thank you so much for checking out my project!** 😄











