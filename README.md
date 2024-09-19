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


