# Pewlett-Hackard-Analysis

## Overview

After finding the number of upcoming retirements, Pewlett-Hackard has asked us to determine the number of retiring employees per title, and identify employees who are eligible to participate in a mentorship program. 

## Analysis

There are four major points that stand out from this analysis

- nearly 50,000 senior employees retiring

| Num    | Title | 
| ----------- | ----------- |
|25916 |	"Senior Engineer" |
|24926 |	"Senior Staff" |
|9285 |	"Engineer" |
|7636 |	"Staff" |
|3603 |	"Technique Leader" |
|1090 |	"Assistant Engineer" |
|2 | "Manager" |


![Retiree Promotions](https://github.com/Olibabba/Pewlett-Hackard-Analysis/blob/main/data/retiree_promotions.png)

- 2 managers are retiring
Hauke Zhang manager of sales overseeing 37701 employees
Hilary Kambil manger of research overseeing 15441 employees

-1549 mentorship eligibility 

## Summary


- How many roles will need to be filled as the "silver tsunami" begins to make an impact?
- 72,458 total positions to fill
- Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees? 
NO

extra queries
```
select dr.count, d.dept_name, e.first_name, e.last_name, t.title
into dept_manager_retire_count
from dept_retire dr
	inner join dept_manager dm
		on (dr.dept_no = dm.dept_no)
	left join employees e
		on (dm.emp_no = e.emp_no)
	INNER JOIN departments d
        ON (dr.dept_no = d.dept_no)
	inner join titles t
		on (e.emp_no = t.emp_no)
where 
	dm.to_date = '9999-01-01'
	and t.to_date = '9999-01-01'
group by dr.count, d.dept_name, e.first_name, e.last_name, t.title;
```

![Department Managers Retiree Count](https://github.com/Olibabba/Pewlett-Hackard-Analysis/blob/main/data/Dept%20Managers.png)


```
--count retiring employees who have been promoted
SELECT emp_no, COUNT(emp_no)
into retire_promotions
FROM retirement_titles 
GROUP BY emp_no 
HAVING COUNT(emp_no) > 1;
```

- 42468 promotions!