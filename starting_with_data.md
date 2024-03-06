Question 1: How many units have been sold and what is our top 5 selling products?

SQL Queries:
```
SELECT ase.v2ProductName AS Product, SUM(sr.total_ordered) AS Total_Units_Sold
FROM public.all_sessions AS ase
JOIN public.sales_report AS sr ON sr.productsku = ase.productsku
GROUP BY v2ProductName
ORDER BY Total_Units_Sold DESC
LIMIT 5;
```

Answer: 
![image](https://github.com/aronpwong/SQL-Project/assets/149037562/4ac05a1e-d2fb-478e-827f-f567c9586479)



Question 2: What is the average sentiment score and magnitude of products purchased by visitors from each country?

SQL Queries:
```
SELECT ase.country, AVG(sr.sentimentScore) AS Avg_Sentiment_Score, AVG(sr.sentimentMagnitude) AS Avg_Sentiment_Magnitude
FROM public.all_sessions AS ase
JOIN public.sales_report AS sr ON sr.productsku = ase.productsku
WHERE country NOT IN ('(not set)')
GROUP BY country;
```

Answer:
![image](https://github.com/aronpwong/SQL-Project/assets/149037562/b1238718-7297-4260-a004-0c2f822f7903)




Question 3: What is the average time spent on the site by vistors from each city and country?

SQL Queries:
```
SELECT ase.city, ase.country, AVG(ase.timeOnSite) AS Avg_Time_On_Site
FROM public.all_sessions AS ase
WHERE city NOT IN ('not available in demo dataset','(not set)')
GROUP BY ase.city, ase.country;
```
Answer:
![image](https://github.com/aronpwong/SQL-Project/assets/149037562/c1768e8b-3f76-4758-b14f-846516b413e9)




