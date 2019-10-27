# Challenge Set 9
## Part I: W3Schools SQL Lab 

*Introductory level SQL*

--

This challenge uses the [W3Schools SQL playground](http://www.w3schools.com/sql/trysql.asp?filename=trysql_select_all). Please add solutions to this markdown file and submit.

1. Which customers are from the UK?

   ```sql
   SELECT CustomerName FROM [Customers] WHERE country='UK';
   ```
   
   ```ContactName
   CustomerName
   Around the Horn
   B's Beverages
   Consolidated Holdings
   Eastern Connection
   Island Trading
   North/South
   Seven Seas Imports
   ```


2. What is the name of the customer who has the most orders?

   ```sql
   SELECT Customers.CustomerName, Orders.OrderID,
         COUNT(Orders.OrderID) AS OrdersCount
         FROM Customers 
        INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID 
   GROUP BY Customers.CustomerID, 
            Customers.CustomerName
   ORDER BY OrdersCount DESC
   LIMIT 1;
   
   CustomerName	OrderID	OrdersCount
   Ernst Handel	10258	10
   ```

   

3. Which supplier has the highest average product price?

   ```sql
   SELECT Suppliers.SupplierName, AVG(Products.Price) 
   FROM Products 
   INNER JOIN Suppliers ON Products.SupplierID=Suppliers.SupplierID
   GROUP BY SupplierName
   ORDER BY AVG(Products.Price) DESC LIMIT 5;
   
   SupplierName	AVG(Products.Price)
   Aux joyeux ecclésiastiques	140.75
   ```

   

4. How many different countries are all the customers from? (*Hint:* consider [DISTINCT](http://www.w3schools.com/sql/sql_distinct.asp).)

   ```sql
   SELECT COUNT (DISTINCT Country) AS NumberofCountries FROM [Customers];
   
   21
   ```

5. What category appears in the most orders?

   ```sql
   SELECT Categories.CategoryName, COUNT (Categories.CategoryName)
   FROM   [Categories]
   JOIN   [Products]     ON Categories.CategoryID = Products.CategoryID
   JOIN   [OrderDetails] ON Products.ProductID = OrderDetails.ProductID
   GROUP BY Categories.CategoryName
   ORDER BY COUNT (Categories.CategoryName) DESC;
   
   
   Dairy Products	100
   ```

6. What was the total cost for each order?

   ```sql
   SELECT OrderDetails.OrderID, SUM(OrderDetails.Quantity*Products.Price) AS TotalCostEachOrder
   FROM [OrderDetails]
   JOIN [Products] ON OrderDetails.ProductID=Products.ProductID
   GROUP BY OrderID;
   
   # Printing out first 5 only
   OrderID	TotalCostEachOrder
   10248	566
   10249	2329.25
   10250	2267.25
   10251	839.5
   10252	4662.5
   ```

7. Which employee made the most sales (by total price)?

   ```sql
   SELECT Employees.EmployeeID, FirstName, LastName, ROUND(SUM(OrderDetails.Quantity*Products.Price),0) AS TotalSales
   FROM [OrderDetails] 
   JOIN [Products]    ON OrderDetails.ProductID=Products.ProductID
   JOIN [Orders]      ON Orders.OrderID=OrderDetails.OrderID
   JOIN [Employees]   ON Employees.EmployeeID=Orders.EmployeeID
   GROUP BY Employees.EmployeeID
   ORDER BY TotalSales DESC
   
   
   EmployeeID	FirstName	LastName	TotalSales
   4	Margaret	Peacock	105696
   ```

   

8. Which employees have BS degrees? (*Hint:* look at the [LIKE](http://www.w3schools.com/sql/sql_like.asp) operator.)

   ```sql
   SELECT FirstName, LastName, Notes
   FROM [Employees]
   WHERE Notes LIKE '%BS%';
   
   
   FirstName	LastName	Notes
   Janet	Leverling	
   Janet has a BS degree in chemistry from Boston College). She has also completed a certificate program in food retailing management. Janet was hired as a sales associate and was promoted to sales representative.
   
   Steven	Buchanan	
   Steven Buchanan graduated from St. Andrews University, Scotland, with a BSC degree. Upon joining the company as a sales representative, he spent 6 months in an orientation program at the Seattle office and then returned to his permanent post in London, where he was promoted to sales manager. Mr. Buchanan has completed the courses 'Successful Telemarketing' and 'International Sales Management'. He is fluent in French.
   ```

   

9. Which supplier of three or more products has the highest average product price? (*Hint:* look at the [HAVING](http://www.w3schools.com/sql/sql_having.asp) operator.)

   ```sql
   SELECT Suppliers.SupplierName, ROUND(AVG(Products.Price),2) AS AvgPrice
   FROM [Suppliers]
   JOIN [Products] ON Suppliers.SupplierID=Products.SupplierID
   GROUP BY Suppliers.SupplierName
   HAVING COUNT(Products.ProductName) >= 3
   ORDER BY AvgPrice DESC
   
   
   SupplierName	AvgPrice
   Tokyo Traders	46
   ```

   

