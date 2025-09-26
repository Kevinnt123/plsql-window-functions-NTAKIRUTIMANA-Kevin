# plsql-window-functions-NTAKIRUTIMANA-Kevin
**problem definition:**

In the retail company working in three districts (Kigali,Muhanga, Nyanza) there is a problem in managing data and how to segment customers for marketing.

**success criteria**

  1.	Top 5 products per region/ quarter: RANK ()

  2.	Running monthly sales totals: SUM () OVER ()

  3.	Month-over-month growth: LAG () / LEAD ()

  4.	Customer quartiles: NTILE (4)

  5.	3-month moving average: AVG () OVER () 

**database schema**

  1. customers(customer_id, name, region)
 
  2. transactions(product_id, name, category)
  
  3. transactions(transaction_id, customer_id,product_id, sale_date, amount)
  
  4. ER Diagram(it is included in the document above)


**queries and outputs**

1.ranking: RANK()

select c.region, p.product_id, p.name as product_name, sum(t.amount) as total_sales, rank() over(partition by c.region order by sum(t.amount) desc) as ranking from transactions t join customers c on t.customer_id= c.customer_id join products p on p.product_id= t.product_id;

2. aggregate: SUM() OVER()

select sale_date, sum(amount) over (order by sale_date) as running_total from transactions;

3. navigation: LAG()

select transaction_id, sale_date, amount, lag(amount) over (order by sale_date)as prev_amount from transactions;

4. distribution: NTILE()

select customer_id, sum(amount) as total_spent, NTILE(4) over (order by sum(amount) desc)as quartile from transactions;


**result analysis** 
1. Descriptive: top product differ by region
2. Diagnostic: Seasonality drives
3. prescriptive: focus marketing on quartile customers.

**references**

1. https://www.youtube.com/watch?v=Ww71knvhQ-s&t=196s

2. https://www.youtube.com/watch?v=g0J7L-HfQAU 
