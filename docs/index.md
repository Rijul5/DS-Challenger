# Welcome to my Mini Data Science Lab
This page provides the details of my experiment that I performed to solve the Summer 2022 Data Science Intern Challenge.

## Question 1
My experiment (program) is available in the [Jupyter Notebook file](https://github.com/Rijul5/DS-Challenger/blob/main/Challenger%20Notebook.ipynb) as well as in the [PDF file](https://github.com/Rijul5/DS-Challenger/blob/main/Challenger%20Notebook.pdf).

### Summary of Analysis Results
**a.  Think about what could be going wrong with our calculation. Think about a better way to evaluate this data.**

After analyzing the data, I found that the data distribution is right-skewed. Due to the presence of some large order values, data distribution is no longer normal. This results in a significant difference in mean, median, and mode values. In addition, the mean value is not a true representative of the central tendency of data. Therefore, the metric of average order value (AOV) is misleading as it uses the mean value to measure the average dollar amount spent each time a customer places an order.

**b. What metric would you report for this dataset?**

I would use the median metric for this dataset.

**c.  What is its value?**

284.0

### My thought process during this investigation

#### I followed the below steps programmatically to analyze the data.

1. Reading data from the given CSV file and calculating the preliminary AOV value.
2. Understanding the data structure by observing features (columns) and corresponding data types.
3. Evaluating if the data has some missing or invalid data points.
4. Understanding the quartiles of data distribution and observing mean, median, minimum, and maximum values.
5. Visualizing the data distribution using histogram and violin plots.
6. As I observe that the data distribution is right-skewed from step 3, I performed a log transformation of the orders data for better visualization of data distribution and the values of mean, median, and mode.
7. After performing step 4, it is clearly evident that the median is a better metric than the mean (AOV) value. Therefore, I decide to use the median metric for the given dataset and compute its value.

## Question 2
**a. How many orders were shipped by Speedy Express in total?**

__Query__
```SQL
SELECT COUNT(*) AS TotalOrders
FROM Orders AS ord 
JOIN 
SHIPPERS AS shp 
ON ord.ShipperID = shp.ShipperID
WHERE ShipperName = "Speedy Express"
```

__Result__
54


**b. What is the last name of the employee with the most orders?**

__Query__
```SQL
SELECT LastName, COUNT (*) AS NumberOfOrders
FROM Orders AS ord
JOIN
Employees AS emp
ON ord.EmployeeID = emp.EmployeeID
GROUP BY (ord.EmployeeID)
ORDER BY NumberOfOrders DESC
LIMIT 1
```

__Result__
Peacock with 40 Orders

**c. What product was ordered the most by customers in Germany?**

__Query__
```SQL
SELECT prod.ProductID, prod.ProductName, SUM(Quantity) AS TotalQuantity
FROM Orders AS ord, OrderDetails AS ordd, Customers AS cust, Products AS prod
WHERE cust.Country = "Germany" AND ord.OrderID = ordd.OrderID AND prod.ProductID = ordd.ProductID AND ord.CustomerID = cust.CustomerID
GROUP BY prod.ProductID
ORDER BY TotalQuantity DESC
```

__Result__
Product Name: Boston Crab Meat
Total Quantity: 160
ProductID: 40

