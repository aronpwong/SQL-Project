What are your risk areas? Identify and describe them.
1. Data Quality Issue
Risk areas would be missing values, duplicates, outliers and inconsistencies in the data.

2. Incorrect Assumptions
Making incorrect assumptions without validating data could lead biased results.

3. Data Privacy and Security
When data is mishandled and/or exposed, it can lead to legal and ethical issues.

4. Data Integrity
Data corruption and unauthorized changes to the data can lead to inaccuracy and unreliability.



QA Process:
Describe your QA process and include the SQL queries used to execute it.

1. Data Profiling to help identify data quality issues in the existing tables
```SELECT COUNT(*) FROM public.all_sessions```

2. Data Cleaning to help improve the data quality
```UPDATE public.all_sessions SET city = 'not available in demo dataset' WHERE city IS NULL;```

3. Data Validation to check the accuracy and integrity of data.
4. Evaluation of data to ensure they answer the question sufficient enough
5. Documenting the process when verifying the data and statements

