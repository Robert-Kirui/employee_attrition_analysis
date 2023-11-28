## Employee Attrition Analysis
---

### Table of Contents
- [Overview](#Overview)
- [Data Source](#Data-Source)
- [Tools](#Tools)
- [Data Analysis](#Data-Analysis)
- [Findings](#Findings)
- [Recommendations](#Recommendations)
- [Limitations](#Limitations)
- [References](#References)

### Overview 
To determine employee attrition for the company and the variation by gender, department, job roles, level of education, field of education, age band, frequency of business travel, and marital status. Also, to determine the correlation between attrition and stock option level, number of trainings in the last year, number of years since last promotion, number of companies previously worked, total working years, number of years in the current role, and number of years at the company.

![overview](https://github.com/Robert-Kirui/employee_attrition_analysis/assets/151769501/69421771-a789-414b-8858-72992ede2819)


### Data Source
The dataset was obtained from [Data Tutorials YouTube channel](https://www.youtube.com/watch?v=-sOHVl_iCHA&t=4s)

### Tools
- SQL
- Microsoft SQL Server
- Power BI
- Excel

### Data Analysis
- What is the total number of employees, current employees, and ex-employees?
- What is the age distribution of the workforce?
- What is the overall attrition rate for the company?
- What is the attrition rate by gender, department, job roles, level of education, field of education, age band, frequency of business travel, and marital status?
- Is there a correlation between attrition and stock option level, number of trainings in the last year, number of years since last promotion, number of companies previously worked, total working years, number of years in the current role, and number of years at the company?
  
### Findings 
```SQL
/* Total Employees*/
SELECT SUM(Employee_Count) AS Total_Employees
FROM HR_data;
```
```SQL
/* Current Employees*/
SELECT COUNT(*) AS Current_Employees
FROM HR_data
WHERE CF_current_Employee = 1;
```
```SQL
/* Ex-Employees*/
SELECT 
	SUM(CASE WHEN CF_current_Employee = 0 THEN 1 ELSE 0 END) AS Ex_Employees
FROM HR_data; 
```
```SQL
/* Overall attrition rate for the company */
SELECT 
	SUM(CASE WHEN CF_current_Employee = 0 THEN 1 ELSE 0 END) * 100.0/ (SELECT SUM(Employee_Count)) AS Overall_Attrition
FROM HR_data; 
```

```SQL
/* Age Distribution of Employees */
SELECT
	 Age, 
	 COUNT(*) AS Employee_Count
FROM HR_data
GROUP BY Age
ORDER BY Employee_Count DESC; 
```


```SQL
/* Attrition rate by gender, department, job roles, education level, education field, 
age band, frequency of business travel and marital status*/

/* Attrition rate by Gender */
SELECT 
	Gender, 
	COUNT(*) AS Number_of_Ex_Employees, 
	((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Gender
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Attrition rate by Department */
SELECT 
	Department, 
	COUNT(*) Number_of_Ex_Employees, 
	((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Department
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Attrition rate by Job Role */
SELECT 
	Job_Role, 
	COUNT(*) AS Number_of_Ex_Employees,
	((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Job_Role
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Attrition rate by Education Level */
SELECT 
	Education, 
	COUNT(*) AS Number_of_Ex_Employees,
	((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Education
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Attrition rate by Field of Education */
SELECT 
	Education_Field, 
	COUNT(*) AS Number_of_Ex_Employees, 
	((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Education_Field
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Attrition rate by Age Band */
SELECT 
	CF_age_band, 
	COUNT(*) AS Number_of_Ex_Employees, 
	((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY CF_age_band
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Attrition rate by Frequency of Business Travel */
SELECT 
	Business_Travel, 
	COUNT(*) AS Number_of_Ex_Employees, 
	((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Business_Travel
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Attrition rate by Marital Status */
SELECT 
	Marital_Status, 
	COUNT(*) AS Number_of_Ex_Employees, 
	((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Marital_Status
ORDER BY Number_of_Ex_Employees DESC; 
```


```SQL
/* Stock option Level VS attrition */
SELECT
	 Stock_Option_Level, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY  Stock_Option_Level
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Number of trainings in the last year VS attrition */
SELECT
	 Training_Times_Last_Year, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Training_Times_Last_Year
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Years since last promotion VS attrition */
SELECT
	 Years_Since_Last_Promotion, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Years_Since_Last_Promotion
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Number of companies previously worked VS attrition */
SELECT
	 Num_Companies_Worked, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Num_Companies_Worked
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Total working years VS attrition */
SELECT
	 Total_Working_Years, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Total_Working_Years
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Years in current role VS attrition */
SELECT
	 Years_In_Current_Role, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Years_In_Current_Role
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
/* Number of years at the company VS attrition */
SELECT
	 Years_At_Company, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Years_At_Company
ORDER BY Number_of_Ex_Employees DESC; 
```

```SQL
/* Patterns in attrition based on the number of years an employee has been under current manager */
SELECT
	 Years_With_Curr_Manager, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Years_With_Curr_Manager
ORDER BY Number_of_Ex_Employees DESC; 
```

```SQL
/* Correlation between attrition and job level and performance rating */
SELECT
	 Job_Level, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Job_Level
ORDER BY Number_of_Ex_Employees DESC;
```

```SQL
SELECT
	 Performance_Rating, 
	 COUNT(*) AS Number_of_Ex_Employees, 
	 ((COUNT(*) * 100.0) / (SELECT COUNT(*) FROM HR_data WHERE CF_current_Employee = 0)) AS Percentage_of_Total
FROM HR_data
WHERE CF_current_Employee = 0
GROUP BY Performance_Rating
ORDER BY Number_of_Ex_Employees DESC;
```

### Findings
- The overall attrition rate for the company is 16.12%.
- Research and Development (R&D) and Sales departments, as well as Lab Technician and Sales Executive roles have higher attrition rates compared to other departments and job roles.
- There is no correlation between the frequency of business travel and attrition. Employees who rarely travel have the highest attrition rates (65.82%) while those who do not travel at all have the least attrition (5.06%). Employees who travel frequently have moderate attrition rate (29.11%).
- Attrition is high among employees aged 25 – 44 years (68.76%), and lowest among those aged over 55 years (4.64%).
- There is high attrition among employees with Bachelor’s and Master’s Degrees (combined 66.24%) and lowest among employees with Doctoral Degrees. Additionally, employees in Life Sciences and Medical fields post the highest attrition (combined 64.13%), while those in Human Resources field have the lowest attrition.
- Employees aged 35 and 34 years are the most in the company. Those aged 18, 19, 57, and 60 years are the least.
- Attrition rate is high among male employees compared to female employees.
- Employees in stock options level 0 and 1 have the highest attrition rate (64.98% and 23.63% respectively), while those in level 2 and 3 have the least attrition rate (5.06% and 6.33% respectively).
- There is no correlation between the number of trainings an employee attended last year and attrition. Attrition rate is highest among employees who attended 2 and 3 trainings last year, and lowest among those who attended 1 and 6 trainings.
- There is a clear correlation between the number of years since the last promotion and attrition. Attrition rate is highest among employees who were promoted within the last year (46.41%), followed by those who were promoted in the last 1 and 2 years (20.68% and 11.39% respectively). On the other hand, attrition rate is the lowest among employees who were last promoted 10 and 14 years ago (0.42%), with those who received the last promotion 11 and 13 years ago following closely (0.84%).
- Attrition rate is very high among employees who have previously worked with one other company (41.35%) and those who haven’t worked with any other company before (9.70%). On the other hand, employees who have previously worked with 8 and 9 other companies post the lowest attrition rate (2.53% and 5.06% respectively).
- There is no correlation between the number of total working years and attrition rate. Employees who have worked for 1 year has the highest attrition, while those who have worked for 21, 25, 26, 28, 31, 33, and 34 years have the lowest attrition (0.42%). Those who have worked for 40 years have a relatively lower attrition rate (0.84%).
- There is a correlation between the number of years in current role and attrition rate. Employees with 0 and 2 years in current role have the highest attrition (30.80% and 28.69% respectively), while those with 12, 13, and 14 years in current role post the lowest attrition rate (0.42%). Employees with 16, 17, and 18 years in current role have no attrition at all (0.00%).
- Employees who have been in the company for 1 and 2 years have the highest attrition (24.89% and 11.39% respectively). Attrition rate is the lowest among employees who have been in the company for 15 years or more (0.42%).
- Employees who have been under the current manager for fewer years tend to leave the company more, compared to those who have been under the current manager for many years.
- Approximately 60% of all employees who left the company were in job level 1, 21.94% were in job level 2, and 13.5% were in job level 3. Only 4.20% (10 out of 237 employees) of all employees who left the company were in job levels 4 and 5. This shows that employees in lower job levels tend to leave the company more compared to those in higher levels. In terms of performance rating, a whopping 84.39% of all employees who left the company had a performance rating of 3, with only 15.61% being those with a performance rating of 4. This shows that employees with lower performance rating tend to leave the company more than those with higher rating.  

### Recommendations
1. Delay promotions among employees in Research and Development (R&D) and Sales departments, and among Lab Technicians and Sales Executives to minimize attrition.
2. When hiring, give priority to individuals who have worked for many other companies before because they are less likely to leave the company soon. 

### Limitations

### References 
- [Data Tutorials YouTube channel](https://www.youtube.com/watch?v=-sOHVl_iCHA&t=4s)
