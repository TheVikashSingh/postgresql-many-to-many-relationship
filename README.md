# postgresql-many-to-many-relationship

I have created 4 tables
<img width="1021" height="595" alt="image" src="https://github.com/user-attachments/assets/f50bf38e-7bac-4c19-b7d7-f159e7c766aa" />


The final result is

<img width="1108" height="441" alt="image" src="https://github.com/user-attachments/assets/5ccec465-ebd9-4364-ac46-d999236edac5" />


------------------------Table creation-------------------------


projectdb=# CREATE TABLE customers(
projectdb(# cust_id INT GENERATED ALWAYS AS IDENTITY (START WITH 3333 INCREMENT BY 7) PRIMARY KEY,
projectdb(# cust_name TEXT NOT NULL);
CREATE TABLE

projectdb=# CREATE TABLE orders(
projectdb(# ord_id INT GENERATED ALWAYS AS IDENTITY (START WITH 98625 INCREMENT BY 9) PRIMARY KEY,
projectdb(# ord_date DATE DEFAULT CURRENT_DATE,
projectdb(# cust_id INT NOT NULL,
projectdb(# FOREIGN KEY (cust_id) REFERENCES customers (cust_id));

projectdb=# CREATE TABLE products(
projectdb(# p_id INT GENERATED ALWAYS AS IDENTITY (START WITH 29874 INCREMENT BY 11) PRIMARY KEY,
projectdb(# p_name VARCHAR(100) NOT NULL,
projectdb(# p_price NUMERIC(10,3) NOT NULL);

projectdb=# CREATE TABLE order_items(
projectdb(# item_id BIGINT GENERATED ALWAYS AS IDENTITY (START WITH 921457 INCREMENT BY 23) PRIMARY KEY,
projectdb(# quantity INT NOT NULL,
projectdb(# ord_id INT NOT NULL,
projectdb(# p_id INT NOT NULL,
projectdb(# FOREIGN KEY (ord_id) REFERENCES orders (ord_id),
projectdb(# FOREIGN KEY (p_id) REFERENCES products (p_id));

--------------------------ADD SOME DATA--------------
projectdb=# INSERT INTO customers (cust_name) VALUES
projectdb-# ('Tony Stark'),
projectdb-# ('Steve Rogers'),
projectdb-# ('Bruce Wayne'),
projectdb-# ('Clark Kent'),
projectdb-# ('Diana Prince'),
projectdb-# ('Peter Parker'),
projectdb-# ('Natasha Romanoff'),
projectdb-# ('Barry Allen'),
projectdb-# ('Arthur Curry'),
projectdb-# ('Thor Odinson'),
projectdb-# ('Loki Laufeyson'),
projectdb-# ('Wanda Maximoff'),
projectdb-# ('Bruce Banner'),
projectdb-# ('Selina Kyle'),
projectdb-# ('Hal Jordan');
INSERT 0 15
projectdb=# INSERT INTO products (p_name, p_price) VALUES
projectdb-# ('Iron Man Suit Mark 50', 999999.999),
projectdb-# ('Captain America Shield', 250000.000),
projectdb-# ('Mjolnir', 500000.000),
projectdb-# ('Web Shooters', 75000.000),
projectdb-# ('Batmobile', 850000.000),
projectdb-# ('Batarang Set', 15000.000),
projectdb-# ('Lasso of Truth', 120000.000),
projectdb-# ('Infinity Gauntlet Replica', 999999.000),
projectdb-# ('Arc Reactor', 300000.000),
projectdb-# ('Doctor Strange Cloak', 180000.000),
projectdb-# ('Flash Speed Boots', 95000.000),
projectdb-# ('Aquaman Trident', 210000.000),
projectdb-# ('Hulkbuster Armor', 1250000.000),
projectdb-# ('Green Lantern Ring', 500000.000),
projectdb-# ('Scarlet Witch Tome', 275000.000);
INSERT 0 15
projectdb=# INSERT INTO orders (cust_id) VALUES
projectdb-# (3333),  -- Tony Stark
projectdb-# (3340),  -- Steve Rogers
projectdb-# (3347),  -- Bruce Wayne
projectdb-# (3354),  -- Clark Kent
projectdb-# (3361),  -- Diana Prince
projectdb-# (3368),  -- Peter Parker
projectdb-# (3375),  -- Natasha Romanoff
projectdb-# (3382),  -- Barry Allen
projectdb-# (3389),  -- Arthur Curry
projectdb-# (3396),  -- Thor Odinson
projectdb-# (3403),  -- Loki
projectdb-# (3410),  -- Wanda
projectdb-# (3417),  -- Bruce Banner
projectdb-# (3424),  -- Selina Kyle
projectdb-# (3431);  -- Hal Jordan

projectdb=# INSERT INTO order_items (ord_id, p_id, quantity) VALUES
projectdb-# -- Tony Stark
projectdb-# (98625, 29874, 1),  -- Iron Man Suit
projectdb-# (98625, 29962, 1),  -- Arc Reactor
projectdb-#
projectdb-# -- Steve Rogers
projectdb-# (98634, 29885, 1),  -- Captain America Shield
projectdb-#
projectdb-# -- Bruce Wayne
projectdb-# (98643, 29918, 1),  -- Batmobile
projectdb-# (98643, 29929, 3),  -- Batarang Set
projectdb-#
projectdb-# -- Clark Kent
projectdb-# (98652, 29929, 2),  -- Batarang Set (gift)
projectdb-#
projectdb-# -- Diana Prince
projectdb-# (98661, 29940, 1),  -- Lasso of Truth
projectdb-#
projectdb-# -- Peter Parker
projectdb-# (98670, 29907, 2),  -- Web Shooters
projectdb-#
projectdb-# -- Natasha Romanoff
projectdb-# (98679, 29929, 2),  -- Batarang Set
projectdb-#
projectdb-# -- Barry Allen
projectdb-# (98688, 29984, 1),  -- Flash Speed Boots
projectdb-#
projectdb-# -- Arthur Curry
projectdb-# (98697, 29995, 1),  -- Aquaman Trident
projectdb-#
projectdb-# -- Thor
projectdb-# (98706, 29896, 1),  -- Mjolnir
projectdb-#
projectdb-# -- Loki
projectdb-# (98715, 29973, 1),  -- Doctor Strange Cloak
projectdb-#
projectdb-# -- Wanda Maximoff
projectdb-# (98724, 30028, 1),  -- Scarlet Witch Tome
projectdb-#
projectdb-# -- Bruce Banner
projectdb-# (98733, 30006, 1),  -- Hulkbuster Armor
projectdb-#
projectdb-# -- Selina Kyle
projectdb-# (98742, 29929, 1),  -- Batarang Set
projectdb-#
projectdb-# -- Hal Jordan
projectdb-# (98751, 30017, 1);  -- Green Lantern Ring
--------------------------------------------------------

SHOWING ALL DATA 

projectdb=# SELECT c.cust_id, c.cust_name, o.ord_id, o.ord_date, p.p_id, p.p_name, p.p_price, oi.item_id, oi.quantity FROM order_items oi INNER JOIN orders o ON o.ord_id = oi.ord_id INNER JOIN products p ON p.p_id = oi.p_id INNER JOIN customers c ON c.cust_id = o.cust_id ORDER BY p.p_price DESC;

<img width="1075" height="382" alt="image" src="https://github.com/user-attachments/assets/c3c27bbe-7515-4d2d-a9ff-38d6722b719d" />
