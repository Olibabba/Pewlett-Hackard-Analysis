# Pewlett-Hackard-Analysis

## Overview

After finding the number of upcoming retirements, Pewlett-Hackard has asked us to determine the number of retiring employees per title, and identify employees who are eligible to participate in a mentorship program. 

## Analysis

There are four major points that stand out from this analysis

- nearly 50,000 senior employees are retiring

| Num    | Title | 
| ----------- | ----------- |
|25916 |	"Senior Engineer" |
|24926 |	"Senior Staff" |
|9285 |	"Engineer" |
|7636 |	"Staff" |
|3603 |	"Technique Leader" |
|1090 |	"Assistant Engineer" |
|2 | "Manager" |

- 2 managers are retiring
Hauke Zhang manager of sales oversees 37701 employees
Hilary Kambil manger of research oversees 15441 employees

- 1,549 retirement-ready employees are eligible for mentorship 

- 

## Summary


How many roles will need to be filled as the "silver tsunami" begins to make an impact?
- There will be 72,458 total positions to fill

Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees? 
- There are not nearly enough elibible mentors. If every 1,549 eligible mentors decide to do so, each one would need to mentor about 45 new employees.

### Extra Queries

It will be useful to see how many retirements each manager will need to oversee.
 
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


If Pewlett-Hackard is interested in recognizing the retirees, they should know how many emplyees have been promoted while at the company!

![Retiree Promotions](https://github.com/Olibabba/Pewlett-Hackard-Analysis/blob/main/data/retiree_promotions.png)

- 42468 retirement-ready employees have been promoted during their tenure at Pewlett-Hackard!