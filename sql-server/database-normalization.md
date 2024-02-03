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

1. Meets **all conditions of 2NF**.
2. Remove **transitive dependencies**.

**Problems of Transitive Dependencies:**
1. Disk Space Wastage.
2. Data Inconsistency.
3. DML queries can become slow.

### Example - Not in 3NF

| EmpId | EmpName | Gender | Salary | AnnualSalary | DeptId |
|-------|---------|--------|--------|--------------|--------|
| 1     | Sam     | M      | 4500   | 54000        | 1      |
| 2     | Pam     | F      | 2000   | 24000        | 2      |
| 3     | Simon   | M      | 1300   | 15600        | 1      |
| 4     | Mary    | F      | 5000   | 60000        | 2      |
| 5     | Todd    | M      | 3000   | 36000        | 1      |

*In the above table, AnnualSalary is dependent on both Salary and DeptId. If Salary changes, AnnualSalary is affected.*

**Below tables meet all 3NF conditions:**

#### Employee Table

| EmpId | EmpName | Gender | Salary | DeptId |
|-------|---------|--------|--------|--------|
| 1     | Sam     | M      | 4500   | 1      |
| 2     | Pam     | F      | 2000   | 2      |
| 3     | Simon   | M      | 1300   | 1      |
| 4     | Mary    | F      | 5000   | 2      |
| 5     | Todd    | M      | 3000   | 1      |

#### Department Salary Table

| DeptId | AnnualSalary |
|--------|--------------|
| 1      | 54000        |
| 2      | 24000        |

## Conclusion

Normalization is a critical process in database design that helps organize data efficiently, reduce redundancy, and ensure data consistency. It involves progressively applying normal forms to achieve a well-structured database.

Understanding the principles of normalization and recognizing the types of dependencies within data are essential skills for designing robust and scalable databases. Regular normalization reviews and adjustments are crucial as data requirements evolve over time.

*Note: The provided examples and explanations are simplified for educational purposes. Real-world scenarios may involve additional complexities and considerations.*

## 4NF

1. Meets **all conditions of 3NF**.
2. Handle **multivalued dependencies**.

**Problems of Multivalued Dependencies:**
1. Disk Space Wastage.
2. Data Inconsistency.
3. DML queries can become slow.

### Example - Not in 4NF

| EmpId | Project  | Hours |
|-------|----------|-------|
| 1     | ProjectA | 20    |
| 1     | ProjectB | 30    |
| 2     | ProjectA | 25    |
| 3     | ProjectB | 40    |
| 4     | ProjectA | 15    |

*In the above table, Hours are dependent on both EmpId and Project. If the number of hours worked on a project changes, we need to update multiple records.*

**Below tables meet all 4NF conditions:**

#### Employee Table

| EmpId | EmpName | Gender | Salary | DeptId |
|-------|---------|--------|--------|--------|
| 1     | Sam     | M      | 4500   | 1      |
| 2     | Pam     | F      | 2000   | 2      |
| 3     | Simon   | M      | 1300   | 1      |
| 4     | Mary    | F      | 5000   | 2      |
| 5     | Todd    | M      | 3000   | 1      |

#### Project Hours Table

| EmpId | Project  | Hours |
|-------|----------|-------|
| 1     | ProjectA | 20    |
| 1     | ProjectB | 30    |
| 2     | ProjectA | 25    |
| 3     | ProjectB | 40    |
| 4     | ProjectA | 15    |

## Conclusion

Normalization is a critical process in database design that helps organize data efficiently, reduce redundancy, and ensure data consistency. It involves progressively applying normal forms to achieve a well-structured database.

Understanding the principles of normalization and recognizing the types of dependencies within data are essential skills for designing robust and scalable databases. Regular normalization reviews and adjustments are crucial as data requirements evolve over time.

*Note: The provided examples and explanations are simplified for educational purposes. Real-world scenarios may involve additional complexities and considerations.*

## 5NF

1. Meets **all conditions of 4NF**.
2. Handle **join dependencies**.

**Problems of Join Dependencies:**
1. Disk Space Wastage.
2. Data Inconsistency.
3. DML queries can become slow.

### Example - Not in 5NF

| Employee | Project  | Location |
|----------|----------|----------|
| Sam      | ProjectA | London   |
| Pam      | ProjectB | Sydney   |
| Sam      | ProjectB | London   |
| Mary     | ProjectA | Sydney   |
| Todd     | ProjectA | London   |

*In the above table, Location is dependent on both Employee and Project. If the location of a project changes, we need to update multiple records.*

**Below tables meet all 5NF conditions:**

#### Employee Table

| Employee |
|----------|
| Sam      |
| Pam      |
| Mary     |
| Todd     |

#### Project Table

| Project  |
|----------|
| ProjectA |
| ProjectB |

#### Location Table

| Employee | Project  | Location |
|----------|----------|----------|
| Sam      | ProjectA | London   |
| Pam      | ProjectB | Sydney   |
| Sam      | ProjectB | London   |
| Mary     | ProjectA | Sydney   |
| Todd     | ProjectA | London   |

## Conclusion

Normalization is a critical process in database design that helps organize data efficiently, reduce redundancy, and ensure data consistency. It involves progressively applying normal forms to achieve a well-structured database.

Understanding the principles of normalization and recognizing the types of dependencies within data are essential skills for designing robust and scalable databases. Regular normalization reviews and adjustments are crucial as data requirements evolve over time.

*Note: The provided examples and explanations are simplified for educational purposes. Real-world scenarios may involve additional complexities and considerations.*

## 6NF

1. Meets **all conditions of 5NF**.
2. Handles **certain types of temporal dependencies**.

**Example Scenario for 6NF:**

Consider a scenario where you want to track changes to a particular attribute over time, and you need to maintain a complete history of all changes. This could be relevant in scenarios involving historical data, versioning, or slowly changing dimensions.

## Example - Not in 6NF

| Employee | Salary | EffectiveDate |
|----------|--------|---------------|
| Sam      | 4500   | 2022-01-01    |
| Sam      | 5000   | 2022-03-15    |
| Sam      | 4800   | 2022-05-20    |
| Pam      | 2000   | 2022-01-01    |
| Pam      | 2200   | 2022-04-10    |

*In the above table, Salary is dependent on both Employee and EffectiveDate. Changes to an employee's salary require adding new records.*

**Below tables meet all 6NF conditions:**

#### Employee Table

| Employee |
|----------|
| Sam      |
| Pam      |

#### Salary Table

| Employee | Salary | EffectiveDate |
|----------|--------|---------------|
| Sam      | 4500   | 2022-01-01    |
| Sam      | 5000   | 2022-03-15    |
| Sam      | 4800   | 2022-05-20    |
| Pam      | 2000   | 2022-01-01    |
| Pam      | 2200   | 2022-04-10    |

## Conclusion

Theoretical forms like 6NF are designed to handle very specific and advanced scenarios, and their practical application depends on the nature of the data and the requirements of the system. Most real-world databases are designed up to 3NF or 4NF, and achieving higher normal forms like 5NF and 6NF is often unnecessary for typical applications.
