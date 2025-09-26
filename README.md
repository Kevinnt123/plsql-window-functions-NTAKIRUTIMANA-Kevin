# plsql-window-functions-NTAKIRUTIMANA-Kevin
step1: 
Business context: A retail company operating in Rwanda with branches Kigali, Muhanga, Nyanza wants to analyze its sale performance.
Data challenge: problem in managing data and how to segment customers for marketing.
Expected outcome: finding out customers buying behavior, sales trend and segmentation to support marketing.
step 2:  Success criteria
1.	Top 5 products per region/ quarter: RANK ()
Expected output: each region should list its top 5 products ranked by sales value.
2.	Running monthly sales totals: SUM () OVER ()
Expected output: sales totals that keep increasing from month to month.
3.	Month-over-month growth: LAG () / LEAD ()
Expected output: a positive or negative growth rate for each month after the first.
4.	Customer quartiles: NTILE (4)
Expected output: division of customers into 4 equal groups, ordered by total spending.
5.	3-month moving average: AVG () OVER ()
Expected output: a smoothed sales trend where each month’s value is averaged with the two months before it. 
step 3: included in the document
step 4: window functions implementation
1.ranking: RANK()
select c.region, p.product_id, p.name as product_name, sum(t.amount) as total_sales, rank() over(partition by c.region order by sum(t.amount) desc) as ranking from transactions t join customers c on t.customer_id= c.customer_id join products p on p.product_id= t.product_id;
2. aggregate: SUM() OVER()
select sale_date, sum(amount) over (order by sale_date) as running_total from transactions;
3. navigation: LAG()
select transaction_id, sale_date, amount, lag(amount) over (order by sale_date)as prev_amount from transactions;
4. distribution: NTILE()
select customer_id, sum(amount) as total_spent, NTILE(4) over (order by sum(amount) desc)as quartile from transactions;
step 6: Result analysis 
1. Descriptive: top product differ by region
2. Diagnostic: Seasonality drives
3. prescriptive: focus marketing on quartile customers.

step 7: References
https://www.youtube.com/watch?v=Ww71knvhQ-s&t=196s :RANK, DENSE RANK, LEAD/ LAG
https://www.youtube.com/watch?v=g0J7L-HfQAU : NTILE
