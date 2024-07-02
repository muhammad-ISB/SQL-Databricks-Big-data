~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

keywords in sql
1. select/from
2. Limit
3. Distinct
4. where
5. -- comments
6. /**/ Multi-line comment
7. Order by

SELECT 
	job_title_short, 
	job_location
FROM 
	job_postings_fact

limit 5

DISTINCT

; = end of sql statement

where = filter out particular data
SELECT
	job_title_short,
    job_location,
    job_via,
    salary_year_avg
FROM
	job_postings_fact
WHERE
	job_title_short = 'Data Analyst'



-- query to comment

SELECT
	job_title_short,
    job_location,
--    job_via, this is ignored
    salary_year_avg
FROM
	job_postings_fact
WHERE
	salary_year_avg > 90000 -- documenting help

Order by

SELECT
	job_title_short,
    job_location,
	job_via, 
    salary_year_avg
FROM
	job_postings_fact
WHERE
	job_title_short =  'Data Analyst' -- documenting help
ORDER BY
	salary_year_avg DESC -- highest first

~~~~~~~~~~~~~~~~ orders to write commanda

select col1, col2....
from table_name
where condition
group by column
having condition
order by col1 [asc/desc]
limit number;
~~~~~~~~~~~~~~~~~

<> and NOT operators

WHERE
	job_via <> 'via LinkedIN'

select 
	job_id,
	job_title_short,
	job_location,
    job_via
from
	job_postings_fact
WHERE 
	job_via <> 'via LinkedIN'
WHERE 
	job_via = 'via Ai-Jobs.net'

_________________

select 
	job_id,
	job_title_short,
	job_location,
    job_via
from
	job_postings_fact
WHERE 
	salary_year_avg > 50000
ORDER BY
	salary_year_avg


~~~~~~~~~~~~~~~~~

select 
	job_id,
	job_title_short,
	job_location,
    job_via
from
	job_postings_fact
WHERE 
	job_title_short = 'Data Analyst'
	AND salary_year_avg > 100000
ORDER BY
	salary_year_avg

~~~~~~~~~~~~~

between and 

select 
	job_id,
	job_title_short,
	job_location,
    job_via
from
	job_postings_fact
WHERE 
	salary_year_avg between 100000 and 200000
ORDER BY
	salary_year_avg

~~~~~~~~~~~~~~~~~~~~~

\IN 

where jobP_location IN ('boston, MA', 'anywhere')


SELECT *
FROM job_postings_fact
where
	job_title_short in ('Data Analyst', 'Data Engineer','Data Scientit')

~~~~~~~~~~~~~~~~~~~~~

SELECT job_title_short, job_location, salary_year_avg
FROM job_postings_fact
where job_location in ('Boston, MA', 'Anywhere') AND 
	((job_title_short = 'Data Analyst' and salary_year_avg > 100000) or
    (job_title_short = 'Business Analyst' and salary_year_avg > 80000))

~~~~~~~~~~~~~~~~~~~~

where
	job_title like '%Data%'

SELECT *
FROM job_postings_fact
where 
	job_title like '%Analyst%'

SELECT job_title
FROM job_postings_fact
where 
	job_title like '%Business_Analyst%'

space = underscore = Business Analyst = Business_Analyst

~~~~~~~~~~~~~~~~~~~~

*********** AS -> can just be put as space instead of AS

SELECT job_title_short AS job_title,
	job_location AS location, 
    job_via as source,
    salary_year_avg as salary
FROM job_postings_fact

SELECT jpc.job_title_short AS job_title,
	jpc.job_location AS location, 
    jpc.job_via as source,
    jpc.salary_year_avg as salary
FROM job_postings_fact as jpc

SELECT jpc.job_title_short  job_title,
	jpc.job_location  location, 
    jpc.job_via  source,
    jpc.salary_year_avg  salary
FROM job_postings_fact  jpc


~~~~~~~~~~~~~~~~~~~~~~~~~~~~
SELECT 
	job_title as job, 
    job_location as LOCATION,
    salary_year_avg AS salary
FROM job_postings_fact 
WHERE 
	(job LIKE '%Data%' or job LIKE '%Business%') AND
    job LIKE '%Analyst%' AND
    job NOT LIKE '%Senior'

~~~~~~~~~~~~~~~~~~~~

Operations ~ Arithmatic 

SELECT 
	project_company,
    nerd_id,
    nerd_role, 
    hours_rate AS rate,
    hours_rate - 5 AS rate_drop,
     hours_rate +5 AS rate_hike
FROM 
	invoices_fact


SELECT 
	project_company,
    nerd_id,
    nerd_role, 
    hours_spent,
    hours_rate AS rate,
     hours_rate +5 AS rate_hike, 
	(hours_rate +5) * hours_spent AS project_total     
FROM 
	invoices_fact
WHERE
	project_total > 1000



~~~~~~~~~~~~~~~~~~~~

modulus operator % - returns the remainder of a division

SELECT 
	activity_id,
    hours_spent,
    hours_spent % 8 AS extra_hours
FROM 
	invoices_fact
WHERE
	(hours_spent BETWEEN 8 AND 16) AND extra_hours > 0
ORDER BY
	hours_spent

~~~~~~~~~~~~~~~~~~

Aggregation function -> single result from input values
sum, count, avg, max, min

SELECT 
	SUM(salary_year_avg) AS salary_sum
FROM job_postings_fact

SELECT 
	SUM(salary_year_avg) AS salary_sum,
    COUNT(*) AS count_rows
FROM job_postings_fact

SELECT 
	min(salary_year_avg) as salary_min, 
    avg(salary_year_avg) as salary_avg, 
    max(salary_year_avg) as salary_max 
FROM job_postings_fact
where
	job_title_short = 'Data Analyst'

SELECT 
	job_title_short as jobs,
	min(salary_year_avg) as salary_min, 
    avg(salary_year_avg) as salary_avg, 
    max(salary_year_avg) as salary_max 
FROM job_postings_fact
GROUP BY
	job_title_short

SELECT 
	job_title_short as jobs,
	min(salary_year_avg) as salary_min, 
    avg(salary_year_avg) as salary_avg, 
    max(salary_year_avg) as salary_max 
FROM job_postings_fact
GROUP BY
	job_title_short
Order by
	salary_avg

~~~~~~~~~~~~~~~~~~

having

SELECT 
	job_title_short as jobs,
    count(job_title_short) as jobs_listed_total, 
	min(salary_year_avg) as salary_min, 
    avg(salary_year_avg) as salary_avg, 
    max(salary_year_avg) as salary_max 
FROM job_postings_fact
GROUP BY
	job_title_short
having 
	count(job_title_short) > 1000
Order by
	salary_avg



SELECT 
	project_id
	hours_spent,
    hours_rate, 
    hours_rate + 5 as rate_hike,
    sum(hours_spent * hours_rate) as total_earnings,
    sum(hours_spent * (hours_rate + 5)) as projected_earning
FROM invoices_fact
group by
	project_id

~~~~~~~~~~~~


SELECT 
	job_title_short as jobs,
	job_location,
    job_via,
    salary_year_avg

FROM job_postings_fact
WHERE
	salary_year_avg IS not null

Order by
	salary_year_avg

~~~~~~~~~~~~~~~~~~~~

Joins

SELECT 
	job_postings.job_title_short,
	job_postings.job_id,
    companies.company_id,
    companies.name

FROM job_postings_fact as job_postings
left join
	company_dim as companies
    ON job_postings.company_id = companies.company_id
    
~~~~~~~~~~~~~~~~~~~~~~~~~~~
SELECT 
	job_postings.job_title_short,
	job_postings.job_id,
    companies.company_id,
    companies.name

FROM job_postings_fact as job_postings
right join
	company_dim as companies
    ON job_postings.company_id = companies.company_id

~~~~~~~~~~~~~~~~~~~~~~~~~~~
