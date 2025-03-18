1. creating new databases- create schema ecommercenew;
2. creating table with inserting columns-
       1.CREATE TABLE customers ( id INT AUTO_INCREMENT PRIMARY KEY,
            name VARCHAR(100) NOT NULL,email VARCHAR(100) UNIQUE NOT NULL, address VARCHAR(255));
       2. CREATE TABLE orders (
           id INT AUTO_INCREMENT PRIMARY KEY, customer_id INT,
            order_date DATE NOT NULL,total_amount DECIMAL(10,2) NOT NULL, FOREIGN KEY (customer_id) REFERENCES customers(id) ON DELETE CASCADE);
       3. CREATE TABLE products (
            id INT AUTO_INCREMENT PRIMARY KEY,
            name VARCHAR(100) NOT NULL, price DECIMAL(10,2) NOT NULL, description TEXT);

   
--Insertting values into the table;   
  1. table customers --  INSERT INTO customers (name, email, address) VALUES ('Alice Johnson', 'alice@example.com', '123 Elm Street'),('Bob Smith', 'bob@example.com', '456 Oak Avenue'),
                         ('Charlie Brown', 'charlie@example.com', '789 Pine Road');
  2.table products   --    INSERT INTO products (name, price, description) VALUES ('Product A', 30.00, 'Description of Product A'),('Product B', 25.00, 'Description of Product B'),('Product C', 50.00, 'Description of Product C'),
                         ('Product D', 75.00, 'Description of Product D');
  3. table orders    --   INSERT INTO orders (customer_id, order_date, total_amount) VALUES (1, CURDATE() - INTERVAL 10 DAY, 120.00),  (2, CURDATE() - INTERVAL 5 DAY, 200.00),  (3, CURDATE() - INTERVAL 35 DAY, 90.00);


Queries to Write:

    1.  Retrieve all customers who have placed an order in the last 30 days.
         code:-
              SELECT DISTINCT c.*
              FROM customers c JOIN orders o ON c.id = o.customer_id WHERE o.order_date >= CURDATE() - INTERVAL 30 DAY;

    ![image](https://github.com/user-attachments/assets/4e733339-6d34-4a51-a06c-dd09a88ac132)
    
    2.  Get the total amount of all orders placed by each customer.
         code:-
              SELECT c.name, SUM(o.total_amount) AS total_spent FROM customers c JOIN orders o ON c.id = o.customer_id GROUP BY c.id;

      ![image](https://github.com/user-attachments/assets/857ce1e3-44a0-4f2b-9de7-d46567fea5c4)

    3.Update the price of Product C to 45.00.
       code:-
           UPDATE products SET price = 45.00  WHERE id = '3';
           ![image](https://github.com/user-attachments/assets/8797eee9-9200-47a0-a4f3-8a5deeda6614)

    4.Add a new column discount to the products table.
    code:-
    ALTER TABLE products ADD COLUMN discount DECIMAL(5,2) DEFAULT 0.00;

         ![image](https://github.com/user-attachments/assets/86323757-7511-4323-a649-747a3834af24)

    5. Retrieve the top 3 products with the highest price.
    code:-
    SELECT * FROM products  ORDER BY price DESC LIMIT 3;
    ![image](https://github.com/user-attachments/assets/c6e5d425-1537-49d9-8a66-7c4761844406)

    6.Get the names of customers who have ordered Product A.
     code:-
          SELECT DISTINCT c.name FROM customers c JOIN orders o ON c.id = o.customer_id JOIN order_items oi ON o.id = oi.order_id
           JOIN products p ON oi.product_id = p.id WHERE p.name = 'Product A';

     ![image](https://github.com/user-attachments/assets/51ce02ab-651e-4555-9ede-63f38ba46328)



    7.Join the orders and customers tables to retrieve the customer's name and order date for each order. 
    code:-SELECT c.name, o.order_date FROM orders o JOIN customers c ON o.customer_id = c.id;
    ![image](https://github.com/user-attachments/assets/193594b5-22cd-4e15-b274-a14c9a1daa32)

    8.Retrieve the orders with a total amount greater than 150.00.
    code:-
        SELECT * FROM orders  WHERE total_amount > 150.00;
        ![image](https://github.com/user-attachments/assets/c705bb77-10c5-4408-917d-6185115e3ca2)

    9.Normalize the database by creating a separate table for order items and updating the orders table to reference the order_items table.
       code:-CREATE TABLE order_items (
    id INT AUTO_INCREMENT PRIMARY KEY, order_id INT, product_id INT,
    quantity INT NOT NULL, price DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (order_id) REFERENCES orders(id) ON DELETE CASCADE,FOREIGN KEY (product_id) REFERENCES products(id) ON DELETE CASCADE);

    ![image](https://github.com/user-attachments/assets/4715e500-a257-428c-91e3-0f179523da41)

    10.Retrieve the average total of all orders.
    code:-
    SELECT AVG(total_amount) AS average_order_total  FROM orders;

    ![image](https://github.com/user-attachments/assets/33afff99-5eed-4508-94a7-05a530bc38ea)







 




    
