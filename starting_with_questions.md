Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries: 
```
SELECT sess.city, sess.country,SUM(sr.total_ordered * (sess.productprice/1000000)) AS TransactionalRevenue
FROM public.all_sessions AS sess
JOIN public.sales_report AS sr ON sr.productsku = sess.productsku
WHERE sess.city NOT IN ('not available in demo dataset', '(not set)')
GROUP BY sess.city, sess.country
ORDER BY TransactionalRevenue desc;
```
Answer:
![image](https://github.com/aronpwong/SQL-Project/assets/149037562/a1ab047c-b63b-4c8f-a1c6-9aa4710e13f9)

**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
```
SELECT sess.city, sess.country, AVG(sr.total_ordered) AS avgproductsordered
FROM public.all_sessions AS sess
JOIN public.sales_report AS sr ON sr.productsku = sess.productsku
WHERE sess.city NOT IN ('not available in demo dataset', '(not set)')
GROUP BY sess.city, sess.country 
ORDER BY avgproductsordered DESC;
```

Answer:
![image](https://github.com/aronpwong/SQL-Project/assets/149037562/19e1126b-2876-46ee-b742-4906a4f51a8c)

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```
SELECT sess.city, sess.country,sess.v2productcategory, COUNT(*) AS product_count
FROM public.all_sessions AS sess
WHERE sess.city NOT IN ('not available in demo dataset','(not set)') AND
	  sess.country NOT IN ('(not set)') AND
	  sess.v2productcategory NOT IN ('(not set)')
GROUP BY sess.city, sess.country, sess.v2productcategory
ORDER BY product_count DESC;
```

Answer:
![image](https://github.com/aronpwong/SQL-Project/assets/149037562/de8fb6ed-ac9f-41db-bc80-8542e55e6ecd)


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```
WITH top_sellers AS (
	SELECT sess.city, sess.country, sess.v2ProductName, SUM(sr.total_ordered) AS total_quantity,
	ROW_NUMBER() OVER(PARTITION BY sess.city, sess.country ORDER BY SUM(sr.total_ordered) DESC) AS top_rank
	FROM public.all_sessions AS sess
	JOIN public.sales_report AS sr ON sr.productsku = sess.productsku
	GROUP BY sess.city, sess.country, sess.v2ProductName 
) 

SELECT sess.city, sess.country, sess.v2ProductName AS top_products
FROM top_sellers, public.all_sessions AS sess
WHERE sess.city NOT IN ('not available in demo dataset','(not set)') AND
	  sess.country NOT IN ('(not set)') AND
	  top_rank = 1;
```

Answer:
![image](https://github.com/aronpwong/SQL-Project/assets/149037562/4ea7945d-9058-4ff3-a9b1-b910d719757d)


**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
```
SELECT sess.city, sess.country, SUM(sbs.total_ordered * (sess.productprice/1000000)) AS total_revenue
FROM public.all_sessions AS sess
JOIN public.sales_by_sku AS sbs ON sbs.productsku = sess.productsku
WHERE sess.city NOT IN ('not available in demo dataset','(not set)') AND
	  sess.country NOT IN ('(not set)')
GROUP BY sess.city, sess.country
ORDER BY total_revenue DESC;
```

Answer:
![image](https://github.com/aronpwong/SQL-Project/assets/149037562/ffedaa1b-9f0c-453b-9a3a-878e0afa0e3c)







