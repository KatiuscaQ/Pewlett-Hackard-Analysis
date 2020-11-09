# Pewlett-Hackard-Analysis

## Analysis overview: 
The purpose of this analysis is to determine the number of retiring employees per title and identify employees who are eligible to participate in a mentorship program.

## Results: 
From the two analysis deliverables it was found that:
1.	There is a total of 300,024 employees.
2.	A total of 90,398 employees will be ready for retirement. This is around 30.13% of the workforce of the company leaving in a close timeframe.
3.	Out of the 90,398 ready-for-retirement employees, only 1,549 could be considered for the mentorship program.
4.	The number of employees ready-for-retirement per department is as follow:
![](https://github.com/KatiuscaQ/Pewlett-Hackard-Analysis/blob/main/Resources/retiring_per_dept.PNG)
 
That table was obtained by running the following query:
```html
--Create a table combining departments and titles 
SELECT DISTINCT ON (emp_no) ut.emp_no,
              ut.first_name,
              ce.last_name,
              d.dept_name
INTO retirees
FROM unique_titles as ut
INNER JOIN dept_emp AS de
ON (ut.emp_no = de.emp_no)
INNER JOIN departments AS d
ON (de.dept_no = d.dept_no)
WHERE d.dept_name IN ('Marketing', 'Finance', 'Human Resources', 'Production', 'Development', 'Quality Management', 'Sales', 'Research', 'Customer Service');

--Count employees per departments
SELECT dept_name,
      COUNT (*)
FROM retirees
GROUP BY (dept_name)
ORDER BY count DESC;
```
## Summary: 
**How many roles will need to be filled as the "silver tsunami" begins to make an impact?**

The roles that will need to be filled are a total of: 90,398. This number was found with the help of the following query: 
```html
SELECT SUM (count) FROM retiring_titles;
```
The roles that will need to be filled are:

![]( https://github.com/KatiuscaQ/Pewlett-Hackard-Analysis/blob/main/Resources/retiring_titles.PNG)
 
**Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?**

There are 1,549 qualified employees that could be considered for the mentorship program. By running the following query, it is possible to see which titles and how many candidates per title could be consider:
```html
SELECT title,
	    COUNT (*) 
FROM mentorship_eligibilty
GROUP BY (title)
ORDER BY count DESC;
```
The following table is created from running said query: 
![](https://github.com/KatiuscaQ/Pewlett-Hackard-Analysis/blob/main/Resources/mentorship_elegibility.PNG)

Notice that in this table the title "Manager" is not fulfilled which means the mentor for the future generation in this position would have to be filled externally.
 
