# What is Database normalization

it is the process of organizing data to minimize data redundancy (data duplication), which in turn ensures data consistency.

**Problems of Data Redundancy** 

1. Disk Space Wastage
2. Data Inconsistency
3. DML queries can become slow(insert, update, delete)

#### There are 6 normal forms 1NF to 6NF

<mark>*Most Databases are in Third NF(3NF)*</mark>

## 1NF

1. data in a each column should be <u>atomic</u>. No <u>multiple values</u>, separated by comma.
2. table does not contain any mark.
3. identify record uniquely using <u>Primary Key</u>.

**Problems**
1. not possible to select, insert, delete and update just one employee.
2. table structure change required every time and waste disk space.

| DeptName | Emp              |
|----------|------------------|
| IT       | Sam, Mike, Shan  |
| HR       | Pam              |

**Below table meets all 1NF conditions**

*Department Table*

| DeptId | DeptName |
|--------|----------|
| 1      | IT       |
| 2      | HR       |

*Employee Table*

| DeptId | EmpName |
|--------|---------|
| 1      | Sam     |
| 1      | Mike    |
| 1      | Shan    |
| 2      | Pam     |


## 2NF

1. meets <u>all condition of 1NF</u>.
2. move <u>Redundant data</u> to separate the table.
3. create <u>Relationship</u> between tables using <u>foreign keys</u>.

**Problems of Redundancy**

1. Disk Space Wastage.
2. Data Inconsistency.
3. DML queries can become slow.

| EmpId | EmpName | Gen | Sal | DeptName | DeptHead | DeptLoc |
|-------|---------|-----|-----|----------|----------|---------|
| 1     | Sam     | M   | 4500| IT       | John     | London  |
| 2     | Pam     | F   | 2000| HR       | Mike     | Sydney  |
| 3     | Simon   | M   | 1300| IT       | John     | London  |
| 4     | Mary    | F   | 5000| HR       | Mike     | Sydney  |
| 5     | Todd    | M   | 3000| IT       | John     | London  |


*In above table what if IT department head is changed to jane?*
*we need to update all records in Emp table*

**Below table meets all 2NF conditions**

*Employee Table*

| EmpId | EmpName | Gender | Salary | DeptId |
|-------|---------|--------|--------|--------|
| 1     | Sam     | M      | 4500   | 1      |
| 2     | Pam     | F      | 2000   | 2      |
| 3     | Simon   | M      | 1300   | 1      |
| 4     | Mary    | F      | 5000   | 2      |
| 5     | Todd    | M      | 3000   | 1      |

*Department Table*

| DeptId | DeptName | DeptHead | DeptLoc  |
|--------|----------|----------|----------|
| 1      | IT       | John     | London   |
| 2      | HR       | Mike     | Sydney   |

## 3NF

1. meets <u>all condition of 1NF and 2NF</u>.
2. does not contain cols(attributes) they are not <u>fully dependent</u> upon the <u>Primary Key</u>. 

| EmpId | EmpName | Gender | Salary | AnnualSalary | DeptId |
|-------|---------|--------|--------|--------------|--------|
| 1     | Sam     | M      | 4500   | 45000        | 1      |
| 2     | Pam     | F      | 2000   | 20000        | 2      |
| 3     | Simon   | M      | 1300   | 13000        | 1      |
| 4     | Mary    | F      | 5000   | 50000        | 2      |
| 5     | Todd    | M      | 3000   | 30000        | 1      |

