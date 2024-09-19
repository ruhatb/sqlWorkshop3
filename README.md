# sqlWorkshop3
--Customers ve Orders tablolarını kullanarak, Customers tablosundaki müşterileri ve onların verdikleri siparişleri birleştirerek listeleyin. Müşteri adı, sipariş ID'si ve sipariş tarihini gösterin.--
SELECT Customers.CustomerName, Orders.OrderID, Orders.OrderDate
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;

-- Suppliers ve Products tablolarını kullanarak tüm tedarikçileri ve onların sağladıkları ürünleri listeleyin. Eğer bir tedarikçinin ürünü yoksa, NULL olarak gösterilsin.--

SELECT Suppliers.Suppliername ,Products.Productname 
FROM Suppliers
LEFT JOİN Products ON Suppliers.Suppliersid =Products.Productsid;

--Employees ve Orders tablolarını kullanarak tüm siparişleri ve bu siparişleri işleyen çalışanları listeleyin. Eğer bir sipariş bir çalışan tarafından işlenmediyse, çalışan bilgileri NULL olarak gösterilsin--

SELECT Orders.OrdersId, Employees.EpmloyeesName 
FROM Orders 
LEFT JOİN Employees ON Orders.OrdersID = Employees.EmpployesId;

--Customers ve Orders tablolarını kullanarak tüm müşterileri ve tüm siparişleri listeleyin. Sipariş vermeyen müşteriler ve müşterisi olmayan siparişler için NULL döndürün--

SELECT Custemers.CustemersName , Orders.OrdersName FROM Orders JOİN Custemers ON Custemers.CustemersID = Orders.OrderID ;

--Verilen Products ve Categories tablolarını kullanarak tüm ürünler ve tüm kategoriler için olası tüm kombinasyonları listeleyin. Sonuç kümesindeki her satır bir ürün ve bir kategori kombinasyonunu göstermelidir--

SELECT Products.ProductName, Categories.CategoryName
FROM Products
CROSS JOIN Categories;

--Orders, Customers, Employees tablolarını kullanarak bu tabloları birleştirin ve 1998 yılında verilen siparişleri listeleyin. Müşteri adı, sipariş ID'si, sipariş tarihi ve ilgili çalışan adı gösterilsin--

SELECT Orders.OrdersId, Custemers.CustemersName, Orders.OrdersDate, Employees.EmployeesName, 
FROM Orders 
LEFT JOİN Custemers ON Orders.CustumerID=Custemers.CustemersID 
LEFT JOİN Employees ON Orders.EmployeesId=Employees.EmployeesID
WHERE (Orders.OrdersDate = 1998) ;

--Orders ve Customers tablolarını kullanarak müşterileri, verdikleri sipariş sayısına göre gruplandırın. Sadece 5’ten fazla sipariş veren müşterileri listeleyin--

SELECT COUNT(Orders.OrdersID) AS Count, Customer.CustomerNAme FROM Orders
LEFT JOİN Customer ON Customers.CustomersID = Orders.CustomersID
GROUP BY Customers.CustomerName 
HAVING Count > 5;

--OrderDetails ve Products tablolarını kullanarak her ürün için kaç adet satıldığını ve toplam satış miktarını listeleyin. Ürün adı, satılan toplam adet ve toplam kazancı (Quantity * UnitPrice) gösterin--

SELECT Products.ProductName, SUM(OrderDetails.Quantity) AS Quantity, sUM(OrderDetails.Quantity * OrderDetails.UnitPrice) AS Total
FROM OrderDetails
JOIN  Products ON OrderDetails.ProductID = Products.ProductID
GROUP BY Products.ProductName;



--Customers ve Orders tablolarını kullanarak, müşteri adı "B" harfiyle başlayan müşterilerin siparişlerini listeleyin--
SELECT Customers.CustomerName, Orders.OrderID
FROM Customers
JOIN Orders ON Customers.CustomerID = Orders.CustomerID
WHERE Customers.CustomerName LIKE 'B%';

--Products ve Categories tablolarını kullanarak tüm kategorileri listeleyin ve ürünleri olmayan kategorileri bulun. Ürün adı NULL olan satırları gösterin--
SELECT Categories.CategoryName, Products.ProductName
FROM Categories
LEFT JOIN Products ON Categories.CategoryID = Products.CategoryID
WHERE Products.ProductName IS NULL;

--Employees tablosunu kullanarak her çalışanın yöneticisiyle birlikte bir liste oluşturun--
SELECT e1.EmployeeID, e1.EmployeeName AS EmployeeName, e2.EmployeeName AS ManagerName
FROM Employees e1
LEFT JOIN  Employees e2 ON e1.ManagerID = e2.EmployeeID;

--Products tablosunu kullanarak her kategorideki en pahalı ürünleri ve bu ürünlerin farklı fiyatlara sahip olup olmadığını sorgulayın--

SELECT  CategoryID,  ProductName, Price
FROM Products p1
WHERE  Price = (SELECT MAX(Price) FROM Products p2 WHERE p1.CategoryID = p2.CategoryID);


--Orders ve OrderDetails tablolarını kullanarak bu tabloları birleştirin ve her siparişin detaylarını sipariş ID'sine göre artan sırada listeleyin--

SELECT  Orders.OrderID,  OrderDetails.ProductID,  OrderDetails.Quantity, OrderDetails.UnitPrice
FROM  Orders
JOIN  OrderDetails ON Orders.OrderID = OrderDetails.OrderID
ORDER BY  Orders.OrderID ASC;

--Employees ve Orders tablolarını kullanarak her çalışanın kaç tane sipariş işlediğini listeleyin. Sipariş işlemeyen çalışanlar da gösterilsin--

SELECT Employees.EmployeeID, Employees.EmployeeName, COUNT(Orders.OrderID) AS OrderCount
FROM Employees
LEFT JOIN  Orders ON Employees.EmployeeID = Orders.EmployeeID
GROUP BY  Employees.EmployeeID, Employees.EmployeeName;

--roducts tablosunu kullanarak bir kategorideki ürünleri kendi arasında fiyatlarına göre karşılaştırın ve fiyatı düşük olan ürünleri listeleyin--
SELECT  p1.ProductID,  p1.ProductName, p1.Price
FROM  Products p1
JOIN Products p2 ON p1.CategoryID = p2.CategoryID AND p1.Price < p2.Price;


*--Products ve Suppliers tablolarını kullanarak tedarikçiden alınan en pahalı ürünleri listeleyin--

SELECT  Suppliers.SupplierName,  Products.ProductName,  Products.Price
FROM  Products
JOIN Suppliers ON Products.SupplierID = Suppliers.SupplierID
WHERE Products.Price = (SELECT MAX(Price) FROM Products WHERE SupplierID = Suppliers.SupplierID);
    
--Employees ve Orders tablolarını kullanarak her çalışanın işlediği en son siparişi bulun--


SELECT  Employees.EmployeeName, AX(Orders.Orderdate) AS LastOrderdate
FROM Employees
LEFT JOIN  Orders ON Employees.EmployeeId = Orders.EmployeeId
GROUP BY Employees.EmployeeName;

--Products tablosunu kullanarak ürünleri fiyatlarına göre gruplandırın ve fiyatı 20 birimden fazla olan ürünlerin sayısını listeleyin--
SELECT COUNT(*) AS Count
FROM Products
WHERE Price > 20;



--Orders ve Customers tablolarını kullanarak 1997 ile 1998 yılları arasında verilen siparişleri müşteri adıyla birlikte listeleyin--
SELECT  Customers.CustomerName,  Orders.OrderID, Orders.OrderDate
FROM  Orders
JOIN  Customers ON Orders.CustomerID = Customers.CustomerID
WHERE  Orders.OrderDate BETWEEN '1997-01-01' AND '1998-12-31';


-- Customers ve Orders tablolarını kullanarak hiç sipariş vermeyen müşterileri listeleyin.
SELECT Customers.CustomerName
FROM Customers
LEFT JOIN Orders ON Customers.CustomerId = Orders.CustomerId
WHERE Orders.OrderId IS NULL;
