What issues will you address by cleaning the data?
1. Removing unneccessary data (ex. not available in demo dataset')
2. Adjusting formatting to be correct





Queries:
Below, provide the SQL queries you used to clean your data.
```
UPDATE public.all_sessions
SET city = '(not set)'
WHERE city IS NULL;
```

```
DELETE FROM public.all_sessions
WHERE city = 'not available in demo dataset'
```

```
UPDATE public.all_sessions
SET country = UPPER(country);
```

```
UPDATE public.all_sessions
SET productSKU = REGEXP_REPLACE(productSKU, '[^a-zA-Z0-9]', '', 'g');
```
