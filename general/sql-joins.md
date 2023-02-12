# SQL basic joins

### 1. INNER JOIN

- An inner join returns only the rows that have matching values in both tables.

- For example, consider two tables `Customers` and `Orders`.

- An inner join between these two tables on the `CustomerID` column would return only the rows where the **`CustomerID` values match in both tables**

- In this example, the output shows only those customers who have placed an order.

  ```sql
  SELECT Customers.CustomerName, Orders.OrderID
  FROM Customers
  INNER JOIN Orders
  ON Customers.CustomerID = Orders.CustomerID;
  ```

  | CustomerName  | OrderID |
  | ------------- | ------- |
  | John Doe      | 1       |
  | Jane Doe      | 2       |
  | John Smith    | 3       |
  | Sarah Johnson | 4       |

&nbsp;

### LEFT OUTER JOIN

- A left outer join returns all the rows from the left table (the first table in the join clause) and the matching rows from the right table (the second table in the join clause).

- If there is no match, NULL values will be returned for the right table's columns.

- For example, a left outer join between the "Customers" and "Orders" tables on the "CustomerID" column would return **all of the customers, with NULL values for the right table's columns for the customers who haven't made an order**.

  ```sql
  SELECT Customers.CustomerName, Orders.OrderID
  FROM Customers
  LEFT JOIN Orders
  ON Customers.CustomerID = Orders.CustomerID;

  ```

  output:

  | CustomerName  | OrderID |
  | ------------- | ------- |
  | John Doe      | 1       |
  | Jane Doe      | 2       |
  | John Smith    | 3       |
  | Sarah Johnson | 4       |
  | Jane Watson   | NULL    |

&nbsp;

### RIGHT OUTER JOIN

- similar to `LEFT OUTER JOIN`, just the other way side

&nbsp;

### SELF JOIN

- A self join is a regular join, but the table is joined with itself.

- For example, consider the "Employees" table. A self join on the "Employees" table could be used to **find all pairs of employees who work in the same department**.

  ```sql
  SELECT A.EmployeeName AS Employee1, B.EmployeeName AS Employee2
  FROM Employees A
  JOIN Employees B
  ON A.Department = B.Department
  WHERE A.EmployeeID <> B.EmployeeID;
  ```

  output:

  | Employee1     | Employee2     |
  | ------------- | ------------- |
  | John Doe      | Jane Doe      |
  | Jane Doe      | John Smith    |
  | John Smith    | Sarah Johnson |
  | Sarah Johnson | Jane Watson   |

&nbsp;

### CROSS JOIN

- A cross join returns the Cartesian product of the two tables, which means it returns all possible combinations of rows from the two tables.
- For example, a cross join between the "Customers" and "Orders" tables would return a table with all **possible combinations** of customers and orders.

  ```sql
  SELECT Customers.CustomerName, Orders.OrderID
  FROM Customers
  CROSS JOIN Orders;
  ```

  | CustomerName  | OrderID |
  | ------------- | ------- |
  | John Doe      | 1       |
  | John Doe      | 2       |
  | John Doe      | 3       |
  | Jane Doe      | 1       |
  | Jane Doe      | 2       |
  | Jane Doe      | 3       |
  | John Smith    | 1       |
  | John Smith    | 2       |
  | John Smith    | 3       |
  | Sarah Johnson | 1       |
  | Sarah Johnson | 2       |
  | Sarah Johnson | 3       |
