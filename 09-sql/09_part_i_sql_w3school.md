# Challenge Set 9
## Part I: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?
```sql
SELECT * FROM Customers WHERE Country='UK';
```
2. What is the name of the customer who has the most orders?
```sql
SELECT CustomerName, COUNT(*) AS OrderCount FROM Customers
JOIN Orders ON Customers.CustomerID = Orders.CustomerID
GROUP BY CustomerName
ORDER BY OrderCount DESC
LIMIT 1;
```
3. Which supplier has the highest average product price?
```sql
SELECT Suppliers.SupplierName,AVG(Products.Price) as AvgPrice   
FROM Suppliers
JOIN Products on Suppliers.SupplierID = Products.SupplierID  
GROUP BY Products.SupplierID  
ORDER BY AvgPrice DESC
LIMIT 1;
```
4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)
```sql
SELECT COUNT(DISTINCT Country) FROM Customers;
```
5. What category appears in the most orders?
```sql
SELECT Products.CategoryID, COUNT(OrderDetails.OrderID) FROM Products
JOIN OrderDetails On Products.ProductID=OrderDetails.ProductID
GROUP BY CategoryID
ORDER BY COUNT(OrderDetails.OrderID) DESC
LIMIT 1;
```
6. What was the total cost for each order?
```sql
SELECT OrderDetails.OrderID, SUM(OrderDetails.OrderID*Products.Price) AS TotalCost FROM OrderDetails
JOIN Products On OrderDetails.ProductID=Products.ProductID
GROUP BY OrderID;
```
7. Which employee made the most sales (by total price)?
```sql
SELECT EmployeeID, TotalCost FROM
(SELECT OrderDetails.OrderID, SUM(OrderDetails.OrderID*Products.Price) AS TotalCost FROM OrderDetails
JOIN Products On OrderDetails.ProductID=Products.ProductID
GROUP BY OrderID) AS S
JOIN (SELECT Orders.OrderID, Employees.EmployeeID FROM Orders
JOIN Employees on Orders.EmployeeID=Employees.EmployeeID) AS E
WHERE S.OrderID=E.OrderID
GROUP BY EmployeeID
ORDER BY TotalCost DESC
LIMIT 1;
```
8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)
```sql
SELECT * FROM Employees
WHERE Notes LIKE '%BS%';
```
9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)
```sql
SELECT SupplierID, AVG(Price) AS AvgPrice
FROM Products
GROUP BY SupplierID
HAVING COUNT(ProductID) > 2
ORDER BY AvgPrice DESC
LIMIT 1;
```
