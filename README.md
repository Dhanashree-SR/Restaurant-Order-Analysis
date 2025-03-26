# 🍽️ Restaurant Order Analysis Using SQL  

## 📌 Project Overview  
In this project, **I was appointed as a Data Analyst** for **Taste of the World Café**, a restaurant that recently launched a **new menu**. My goal was to analyze customer data to provide insights into:  

✅ **Which menu items are performing well or underperforming?**  
✅ **What are the most frequently ordered dishes?**  
✅ **Who are the top customers, and what do they love the most?**  

Using **SQL**, I extracted insights from restaurant transactions to help the management make **data-driven decisions** on menu optimization and customer engagement.  

---

## 📂 Dataset Information  
This project is built on **two main tables**:  
📌 **`menu_items`** – Stores details about each menu item (name, category, price). 

📌 **`order_details`** – Contains all customer transactions (order ID, item ID, order date).  

📥 **[Click to View Guided Project](https://app.mavenanalytics.io/guided-projects/d7167b45-6317-49c9-b2bb-42e2a9e9c0bc)**

---

## 🎯 My Approach  
To achieve my objectives, I performed:  

📊 **Menu Analysis** – Understanding menu pricing, categories, and dish performance.  
📋 **Order Analysis** – Examining customer transactions, spending habits, and order frequency.  
🔗 **Table Joins & Customer Insights** – Combining both tables to analyze customer preferences.  

---

## 🛠️ SQL Queries & Analysis  

### 🍽️ Menu Analysis  
- **View all menu items**  
  ```sql
  SELECT * FROM menu_items;
  ```
- **Total number of menu items**  
  ```sql
  SELECT COUNT(item_name) AS Item_Count FROM menu_items;
  ```
- **Most & least expensive items**  
  ```sql
  SELECT * FROM menu_items ORDER BY price DESC;  -- Most expensive  
  SELECT * FROM menu_items ORDER BY price;       -- Least expensive  
  ```
- **Category-wise item count**  
  ```sql
  SELECT category, COUNT(menu_item_id) AS num_items  
  FROM menu_items  
  GROUP BY category;
  ```
- **Average price per category**  
  ```sql
  SELECT category, AVG(price) AS Avg_Price  
  FROM menu_items  
  GROUP BY category;
  ```
- **Total Italian dishes on the menu**  
  ```sql
  SELECT COUNT(*) FROM menu_items WHERE category='Italian';
  ```

---

### 📋 Order Analysis  
- **Explore the orders dataset**  
  ```sql
  SELECT * FROM order_details;
  ```
- **Date range of transactions**  
  ```sql
  SELECT MIN(order_date), MAX(order_date) FROM order_details;
  ```
- **Total number of orders & items ordered**  
  ```sql
  SELECT COUNT(DISTINCT order_id) FROM order_details;  
  SELECT COUNT(*) FROM order_details;
  ```
- **Orders with the most items**  
  ```sql
  SELECT order_id, COUNT(item_id) AS num_items  
  FROM order_details  
  GROUP BY order_id  
  ORDER BY num_items DESC;
  ```
- **Orders with more than 12 items**  
  ```sql
  SELECT COUNT(*) AS More_than_12_items FROM (  
    SELECT order_id, COUNT(item_id) AS num_items  
    FROM order_details  
    GROUP BY order_id  
    HAVING num_items > 12  
  ) AS num_orders;
  ```

---

### 🛍️ Customer Behavior Insights  
To understand customer preferences, I **joined both tables** and analyzed purchasing behavior:  

- **Join `menu_items` and `order_details` tables**  
  ```sql
  SELECT *  
  FROM order_details od  
  LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id;
  ```
- **Most & least ordered items**  
  ```sql
  SELECT item_name, COUNT(order_details_id) AS num_purchases  
  FROM order_details od  
  LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id  
  GROUP BY item_name  
  ORDER BY num_purchases DESC;  -- Most ordered  
  ```
  ```sql
  SELECT item_name, COUNT(order_details_id) AS num_purchases  
  FROM order_details od  
  LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id  
  GROUP BY item_name  
  ORDER BY num_purchases;  -- Least ordered  
  ```
- **Top 5 highest spending orders**  
  ```sql
  SELECT order_id, SUM(price) AS total_spend  
  FROM order_details od  
  LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id  
  GROUP BY order_id  
  ORDER BY total_spend DESC  
  LIMIT 5;
  ```
- **Details of the highest spending order (Order ID: 440)**  
  ```sql
  SELECT order_id, category, COUNT(item_id) AS num_items  
  FROM order_details od  
  LEFT JOIN menu_items mi ON od.item_id = mi.menu_item_id  
  WHERE order_id = 440  
  GROUP BY category;
  ```
- **Most expensive order in the dataset**  
  ```sql
  SELECT od.order_id, SUM(mi.price) AS Total_Order_Amount  
  FROM order_details od  
  JOIN menu_items mi ON od.item_id = mi.menu_item_id  
  GROUP BY od.order_id  
  ORDER BY Total_Order_Amount DESC  
  LIMIT 1;
  ```

---

## 🔥 Key Insights from My Analysis  
🔹 **Best-Selling Items:** Some menu items were significantly more popular than others.  
🔹 **Customer Preferences:** Top-spending customers preferred specific dish categories.  
🔹 **Expensive Orders:** Some customers placed orders that were much higher than average.  
🔹 **Menu Pricing:** Identified high-value and low-value menu items.  

These insights can help the restaurant **optimize its menu**, adjust pricing, and **improve customer experience**!  

---

## 📊 Tools I Used  
🔹 **MySQL** – Querying and analyzing structured data.  
🔹 **MySQL Workbench** – Running queries and visualizing database tables.  
🔹 **Maven Analytics** – A guided learning platform that structured my approach.  

---

## 🙌 Special Acknowledgment  
This project was **successfully completed** as part of a guided project from **Maven Analytics**, mentored by **Alice Zhao**. 🎉  
A huge thanks to the **Maven Analytics team** for their structured resources and expert guidance.  

---

## 🚀 How to Run My Project  
If you’d like to **replicate my analysis**, follow these steps:  

1️⃣ Clone this repository:  
   ```sh
   git clone https://github.com/yourusername/restaurant-order-analysis.git
   ```
2️⃣ Click here to view the guided project: **[🔗 Click to View Guided Project](https://app.mavenanalytics.io/guided-projects/d7167b45-6317-49c9-b2bb-42e2a9e9c0bc)**  
3️⃣ Import the dataset into **MySQL Workbench**.  
4️⃣ Run the SQL queries provided in this README.  
5️⃣ Analyze the results and generate insights.  

---

## 💬 Connect With Me  
📌 **LinkedIn:** https://www.linkedin.com/in/dhanashree-sr/ <br/>
📧 **Portfolio:** https://dhanashreesr.vercel.app/

Feel free to reach out if you have any **questions, feedback, or want to discuss SQL projects!** 😊  

---
