# Database Queries

## find all customers that live in London. Returns 6 records.

SELECT \* FROM customers WHERE city = 'London'; // returns 6 records

## find all customers with postal code 1010. Returns 3 customers.

SELECT \* FROM Customers WHERE PostalCode = 1010; // returns 3 records

## find the phone number for the supplier with the id 11. Should be (010) 9984510.

SELECT Phone FROM Suppliers WHERE SupplierID = 11; // returns correct number

## list orders descending by the order date. The order with date 1997-02-12 should be at the top.

SELECT \* FROM Orders ORDER BY OrderDate DESC; // returns correct date on top

## find all suppliers who have names longer than 20 characters. You can use `length(SupplierName)` to get the length of the name. Returns 11 records.

SELECT \* FROM Suppliers WHERE LENGTH(SupplierName) > 20; // returns 11 records

## find all customers that include the word "market" in the name. Should return 4 records.

SELECT \* FROM Customers WHERE CustomerName LIKE '%market%'; // returns 4 records

## add a customer record for _"The Shire"_, the contact name is _"Bilbo Baggins"_ the address is _"1 Hobbit-Hole"_ in _"Bag End"_, postal code _"111"_ and the country is _"Middle Earth"_.

INSERT INTO customers(customerName, contactName,address,city, postalCode,country ) VALUES ('The Shire', 'Bilbo Baggins', '1 Hobbit-Hole','Bag End','111','Middle Earth'); // works fine and inserts correctly

## update _Bilbo Baggins_ record so that the postal code changes to _"11122"_.

UPDATE customers set postalCode = 11122 WHERE postalCode = 111;

## list orders grouped by customer showing the number of orders per customer. _Rattlesnake Canyon Grocery_ should have 7 orders.

SELECT Customers.customerName, COUNT(Orders.customerid) FROM Orders INNER JOIN Customers ON Orders.customerid=customers.customerid GROUP BY customers.customerName; // lists correctly displays 7 orders

## list customers names and the number of orders per customer. Sort the list by number of orders in descending order. _Ernst Handel_ should be at the top with 10 orders followed by _QUICK-Stop_, _Rattlesnake Canyon Grocery_ and _Wartian Herkku_ with 7 orders each.

SELECT Customers.customername, COUNT(Orders.customerid) FROM Orders INNER JOIN Customers ON Orders.customerid=customers.customerid GROUP BY customername ORDER BY COUNT(Orders.customerid) desc; // sorts correctly with Ernst Handel at the top

## list orders grouped by customer's city showing number of orders per city. Returns 58 Records with _Aachen_ showing 2 orders and _Albuquerque_ showing 7 orders.

SELECT Customers.city, COUNT(Orders.customerid) FROM Orders INNER JOIN Customers ON Orders.customerid=customers.customerid GROUP BY city // sorts correctly

## delete all users that have no orders. Should delete 17 (or 18 if you haven't deleted the record added) records.

DELETE FROM customers WHERE NOT EXISTS (SELECT \* FROM orders WHERE orders.customerid = customers.customerid); // deletes the correct amount 18 in my case since I didn't delete the newly added record
