ALTER SESSION SET NLS_DATE_FORMAT='DD/MM/YYYY'; 

DROP TABLE item CASCADE CONSTRAINTS; 
DROP TABLE orders CASCADE CONSTRAINTS; 
DROP TABLE order_line CASCADE CONSTRAINTS; 
DROP TABLE outlet CASCADE CONSTRAINTS; 
DROP TABLE staff CASCADE CONSTRAINTS; 
DROP TABLE staff_list CASCADE CONSTRAINTS; 
DROP TABLE customer CASCADE CONSTRAINTS; 
DROP TABLE vehicle CASCADE CONSTRAINTS; 
DROP TABLE transactions CASCADE CONSTRAINTS; 
DROP TABLE training_plan CASCADE CONSTRAINTS; 
DROP TABLE stock CASCADE CONSTRAINTS; 
DROP TABLE stock_list CASCADE CONSTRAINTS; 

CREATE TABLE item ( 
    item_num NUMBER(3) PRIMARY KEY, 
    item_description NVARCHAR2(50) NOT NULL,  
    item_type VARCHAR2(20) NOT NULL,  
    item_price NUMBER(5,2) NOT NULL,  
    CONSTRAINT check_item_type CHECK (item_type IN ('Pizza', 'Sides', 'Beverages', 'Soup', 'Pasta', 'Desserts', 'Breads')), 
    CONSTRAINT check_item_price CHECK (item_price > 0),
    CONSTRAINT AK_item UNIQUE (item_description)
);

INSERT INTO item VALUES (1, 'Hawaiian Pizza ' || UNISTR('\D83C\DF55\D83C\DF55'), 'Pizza', 24.99);
INSERT INTO item VALUES (2, 'Aloha Chicken ' || UNISTR('\D83C\DF55\D83C\DF57'), 'Pizza', 24.99);
INSERT INTO item VALUES (3, 'Chicken Delight ' || UNISTR('\D83C\DF57\D83C\DF55'), 'Pizza', 24.99);
INSERT INTO item VALUES (4, 'Beef Pepperoni ' || UNISTR('\D83C\DF56\D83C\DF55'), 'Pizza', 24.99);
INSERT INTO item VALUES (5, 'Beef Sensation ' || UNISTR('\D83C\DF56\D83C\DF55'), 'Pizza', 24.99);
INSERT INTO item VALUES (6, 'Seafood Sensation ' || UNISTR('\D83E\DD53\D83C\DF55'), 'Pizza', 24.99);
INSERT INTO item VALUES (7, 'Island Tuna ' || UNISTR('\D83C\DF63\D83C\DF55'), 'Pizza', 24.99);
INSERT INTO item VALUES (8, 'Vege Heaven ' || UNISTR('\D83C\DF3F\D83C\DF55'), 'Pizza', 24.99);
INSERT INTO item VALUES (9, 'Mushroom Supreme ' || UNISTR('\D83C\DF44\D83C\DF55'), 'Pizza', 24.99);
INSERT INTO item VALUES (10, 'Onion Rings' || UNISTR('\D83E\DDC5'), 'Sides', 7.20);
INSERT INTO item VALUES (11, 'Potato Wedges' || UNISTR('\D83E\DD54'), 'Sides', 7.20);
INSERT INTO item VALUES (12, 'Coke' || UNISTR('\D83C\DF7A'), 'Beverages', 5.90);
INSERT INTO item VALUES (13, 'Sprite' || UNISTR('\D83E\DDCA'), 'Beverages', 5.90);
INSERT INTO item VALUES (14, 'Fanta' || UNISTR('\D83C\DF4A'), 'Beverages', 5.90);
INSERT INTO item VALUES (15, '100 Plus' || UNISTR('\D83D\DCAF'), 'Beverages', 5.90);
INSERT INTO item VALUES (16, 'Creamy Carbonara Pasta' || UNISTR('\D83C\DF5D\D83E\DDC0'), 'Pasta', 15.90);
INSERT INTO item VALUES (17, 'Chicken Bolognaise Pasta' || UNISTR('\D83C\DF5D\D83C\DF57'), 'Pasta', 15.90);
INSERT INTO item VALUES (18, 'Mushroom Soup' || UNISTR('\D83C\DF44\D83C\DF5B'), 'Soup', 6.50);
INSERT INTO item VALUES (19, 'Pumpkin Soup' || UNISTR('\D83C\DF83\D83C\DF5B'), 'Soup', 6.50);
INSERT INTO item VALUES (20, 'Seafood Soup' || UNISTR('\D83C\DF64\D83C\DF5B'), 'Soup', 6.50);
INSERT INTO item VALUES (21, 'Chocolate Ice Cream' || UNISTR('\D83C\DF6B\D83C\DF66'), 'Desserts', 4.90);
INSERT INTO item VALUES (22, 'Vanilla Ice Cream' || UNISTR('\D83C\DF66\D83C\DF3C'), 'Desserts', 4.90);
INSERT INTO item VALUES (23, 'Chocolate Fudge Cake' || UNISTR('\D83C\DF6B\D83C\DF70'), 'Desserts', 4.90);
INSERT INTO item VALUES (24, 'Bread Stix' || UNISTR('\D83C\DF5E'), 'Breads', 4.99);
INSERT INTO item VALUES (25, 'Cheesy Stix' || UNISTR('\D83E\DDC0\D83C\DF5E'), 'Breads', 4.99);

CREATE TABLE outlet ( 
    outlet_num NUMBER(2) PRIMARY KEY, 
    outlet_tel CHAR(10) NOT NULL, 
    outlet_street VARCHAR2(100) NOT NULL, 
    outlet_suburb VARCHAR2(50) NOT NULL, 
    outlet_postcode NUMBER(5) NOT NULL, 
    CONSTRAINT check_outlet_postcode CHECK (outlet_postcode BETWEEN 10000 AND 99999),
    CONSTRAINT AK_outlet UNIQUE (outlet_tel)
); 

INSERT INTO outlet VALUES (01, '0322013974', 'No. 26, Jalan Bangsar', 'Bangsa Baru', 59100);
INSERT INTO outlet VALUES (02, '0355240155', ' No.3 Jalan Aerobik 13/43', 'Shah Alam', 40100);
INSERT INTO outlet VALUES (03, '0377325710', 'No. 5 Jalan SS 22/19', 'Damansara Utama', 47400);
INSERT INTO outlet VALUES (04, '0366180751', 'No. 15 Jalan SS5B', 'Kelana Jaya', 47301);
INSERT INTO outlet VALUES (05, '0311809218', 'No. 7 Jalan Setia Indah', 'Setia Alam', 40170);
INSERT INTO outlet VALUES (06, '0399152830', 'No. 20 Jalan Sri Damak', 'Klang', 41200);
INSERT INTO outlet VALUES (07, '0388102638', 'No. 5 Jalan USJ 10', 'Subang Jaya', 47610);

CREATE TABLE customer ( 
    cust_num NUMBER(6) PRIMARY KEY, 
    cust_tel CHAR(11) NOT NULL, 
    cust_title CHAR(2) NOT NULL, 
    cust_fname VARCHAR2(50) NOT NULL, 
    cust_lname VARCHAR2(50) NOT NULL, 
    cust_street VARCHAR2(100) NOT NULL, 
    cust_suburb VARCHAR2(50) NOT NULL, 
    cust_postcode NUMBER(5) NOT NULL, 
    CONSTRAINT check_cust_title CHECK (cust_title IN ('Ms', 'Mr')), 
    CONSTRAINT check_cust_postcode CHECK (cust_postcode BETWEEN 10000 AND 99999), 
    CONSTRAINT AK_customer UNIQUE (cust_tel) 
); 

INSERT INTO customer VALUES (123456, '01123456782', 'Mr', 'John', 'Smith', '1, Jalan Raya', 'Subang Jaya', 47500);
INSERT INTO customer VALUES (234567, '0123456789', 'Ms', 'Emily', 'Johnson', '2, Jalan Bahagia', 'Shah Alam', 40000);
INSERT INTO customer VALUES (345678, '0134567890', 'Mr', 'Daniel', 'Brown', '3, Jalan Ceria', 'Klang', 41000);
INSERT INTO customer VALUES (456789, '0145678901', 'Ms', 'Olivia', 'Taylor', '4, Jalan Damai', 'Petaling Jaya', 47400);
INSERT INTO customer VALUES (567890, '0156789012', 'Mr', 'William', 'Davis', '5, Jalan Sejahtera', 'Subang Jaya', 47500);
INSERT INTO customer VALUES (678901, '0167890123', 'Ms', 'Sophia', 'Wilson', '6, Jalan Indah', 'Shah Alam', 40000);
INSERT INTO customer VALUES (789012, '0178901234', 'Mr', 'Michael', 'Thomas', '7, Jalan Ceria', 'Klang', 41000);
INSERT INTO customer VALUES (890123, '0189012345', 'Ms', 'Emma', 'Clark', '8, Jalan Bahagia', 'Petaling Jaya', 47400);
INSERT INTO customer VALUES (901234, '0190123456', 'Mr', 'Jacob', 'Anderson', '9, Jalan Raya', 'Subang Jaya', 47500);
INSERT INTO customer VALUES (012345, '0101234567', 'Ms', 'Isabella', 'Lee', '10, Jalan Damai', 'Shah Alam', 40000);
INSERT INTO customer VALUES (129456, '0112345679', 'Mr', 'David', 'Martin', '11, Jalan Sejahtera', 'Klang', 41000);
INSERT INTO customer VALUES (294567, '0123456788', 'Ms', 'Ava', 'Harris', '12, Jalan Indah', 'Petaling Jaya', 47400);
INSERT INTO customer VALUES (340678, '0134567897', 'Mr', 'Daniel', 'Walker', '13, Jalan Bahagia', 'Subang Jaya', 47500);
INSERT INTO customer VALUES (421789, '0145678906', 'Ms', 'Sophia', 'Lewis', '14, Jalan Ceria', 'Shah Alam', 40000);
INSERT INTO customer VALUES (534890, '0156789015', 'Mr', 'Matthew', 'Brown', '15, Jalan Damai', 'Klang', 41000);
INSERT INTO customer VALUES (623901, '0167890124', 'Ms', 'Emily', 'Johnson', '16, Jalan Sejahtera', 'Petaling Jaya', 47400);
INSERT INTO customer VALUES (776012, '0178901233', 'Mr', 'David', 'Taylor', '17, Jalan Indah', 'Subang Jaya', 47500);
INSERT INTO customer VALUES (834123, '0189012342', 'Ms', 'Olivia', 'Davis', '18, Jalan Raya', 'Shah Alam', 40000);
INSERT INTO customer VALUES (905634, '0190123451', 'Mr', 'James', 'Clark', '19, Jalan Bahagia', 'Klang', 41000);
INSERT INTO customer VALUES (013445, '0101234565', 'Ms', 'Sophia', 'Anderson', '20, Jalan Ceria', 'Petaling Jaya', 47400);

CREATE TABLE transactions ( 
    trans_num NUMBER(6) PRIMARY KEY, 
    trans_type VARCHAR2(20) NOT NULL, 
    trans_time TIMESTAMP(2) NOT NULL, 
    trans_amount NUMBER(6, 2) NOT NULL, 
    trans_discount NUMBER(3,2) DEFAULT NULL, 
    CONSTRAINT check_trans_amount CHECK (trans_amount >0), 
    CONSTRAINT check_discount CHECK (trans_discount BETWEEN 0 AND 1),
    CONSTRAINT AK_transactions UNIQUE (trans_time)
); 

/*
Due to the high volume of transactions in the pizza restaurant, an index on trans_type is created to enhance
the performance of filtering data. This improvement aids in generating daily sales reports based on transaction types, 
facilitating financial analysis and performance evaluation.
*/
CREATE INDEX idx_trans_type ON transactions(trans_type);

INSERT INTO transactions 
VALUES (000001, 'Cash', TO_TIMESTAMP('02-05-2022 18:23:11.02', 'DD-MM-YYYY HH24:MI:SS.FF'), 112.46, 0.20);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000002, 'Credit Card', TO_TIMESTAMP('05-06-2022 10:45:30.00', 'DD-MM-YYYY HH24:MI:SS.FF'), 69.48);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000003, 'E-wallet', TO_TIMESTAMP('10-07-2022 15:12:40.57', 'DD-MM-YYYY HH24:MI:SS.FF'), 17.70);
INSERT INTO transactions 
VALUES (000004, 'Cash', TO_TIMESTAMP('21-07-2022 09:30:15.82', 'DD-MM-YYYY HH24:MI:SS.FF'), 90.87, 0.10);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000005, 'Credit Card', TO_TIMESTAMP('04-08-2022 12:55:21.19', 'DD-MM-YYYY HH24:MI:SS.FF'), 24.99);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount)
VALUES (000006, 'E-wallet', TO_TIMESTAMP('12-08-2022 17:40:05.63', 'DD-MM-YYYY HH24:MI:SS.FF'), 24.99);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000007, 'Cash', TO_TIMESTAMP('20-09-2022 14:20:30.42', 'DD-MM-YYYY HH24:MI:SS.FF'), 16.70);
INSERT INTO transactions 
VALUES (000008, 'Credit Card', TO_TIMESTAMP('07-10-2022 09:15:55.88', 'DD-MM-YYYY HH24:MI:SS.FF'), 74.97, 0.10);
INSERT INTO transactions 
VALUES (000009, 'E-wallet', TO_TIMESTAMP('28-10-2022 13:05:41.72', 'DD-MM-YYYY HH24:MI:SS.FF'), 99.96, 0.10);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000010, 'Cash', TO_TIMESTAMP('17-11-2022 19:48:23.11', 'DD-MM-YYYY HH24:MI:SS.FF'), 57.18);
INSERT INTO transactions 
VALUES (000011, 'Credit Card', TO_TIMESTAMP('09-12-2022 11:30:55.03', 'DD-MM-YYYY HH24:MI:SS.FF'), 74.97, 0.10);
INSERT INTO transactions 
VALUES (000012, 'E-wallet', TO_TIMESTAMP('01-01-2023 14:55:20.69', 'DD-MM-YYYY HH24:MI:SS.FF'), 74.97, 0.10);
INSERT INTO transactions 
VALUES (000013, 'Cash', TO_TIMESTAMP('23-01-2023 17:10:45.40', 'DD-MM-YYYY HH24:MI:SS.FF'), 74.97, 0.10);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000014, 'Credit Card', TO_TIMESTAMP('16-02-2023 09:25:30.92', 'DD-MM-YYYY HH24:MI:SS.FF'), 25.88);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000015, 'E-wallet', TO_TIMESTAMP('14-03-2023 12:40:15.21', 'DD-MM-YYYY HH24:MI:SS.FF'), 49.98);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000016, 'Cash', TO_TIMESTAMP('26-03-2023 15:55:50.63', 'DD-MM-YYYY HH24:MI:SS.FF'), 24.99);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000017, 'Credit Card', TO_TIMESTAMP('09-04-2023 18:30:40.49', 'DD-MM-YYYY HH24:MI:SS.FF'), 59.78);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000018, 'E-wallet', TO_TIMESTAMP('17-05-2023 10:45:55.74', 'DD-MM-YYYY HH24:MI:SS.FF'), 67.20);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000019, 'Cash', TO_TIMESTAMP('14-06-2023 13:20:10.31', 'DD-MM-YYYY HH24:MI:SS.FF'), 55.88);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000020, 'Credit Card', TO_TIMESTAMP('03-07-2023 16:45:25.16', 'DD-MM-YYYY HH24:MI:SS.FF'), 56.39);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000021, 'Credit Card', TO_TIMESTAMP('09-07-2023 12:32:40.49', 'DD-MM-YYYY HH24:MI:SS.FF'), 29.98);
INSERT INTO transactions (trans_num, trans_type, trans_time, trans_amount) 
VALUES (000022, 'E-wallet', TO_TIMESTAMP('15-07-2023 19:55:50.63', 'DD-MM-YYYY HH24:MI:SS.FF'), 49.98);

CREATE TABLE orders (
    order_num NUMBER(6) PRIMARY KEY,
    cust_num NUMBER(6) NOT NULL,
    outlet_num NUMBER(2) NOT NULL,
    trans_num NUMBER(6) NOT NULL,
    order_time TIMESTAMP(0) NOT NULL,
    FOREIGN KEY (cust_num) REFERENCES customer(cust_num), 
    FOREIGN KEY (outlet_num) REFERENCES outlet(outlet_num), 
    FOREIGN KEY (trans_num) REFERENCES transactions(trans_num), 
    CONSTRAINT check_outlet_num CHECK (outlet_num BETWEEN 1 AND 7),
    CONSTRAINT AK_orders UNIQUE (cust_num, order_time) 
);

INSERT INTO orders VALUES (000001, 123456, 01, 000001, TO_TIMESTAMP('02-05-2022 18:23:11', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000002, 234567, 02, 000002, TO_TIMESTAMP('05-06-2022 10:45:30', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000003, 345678, 03, 000003, TO_TIMESTAMP('10-07-2022 15:12:40', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000004, 456789, 04, 000004, TO_TIMESTAMP('21-07-2022 09:30:15', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000005, 567890, 05, 000005, TO_TIMESTAMP('04-08-2022 12:55:21', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000006, 678901, 06, 000006, TO_TIMESTAMP('12-08-2022 17:40:05', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000007, 789012, 07, 000007, TO_TIMESTAMP('20-09-2022 14:20:30', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000008, 890123, 02, 000008, TO_TIMESTAMP('07-10-2022 09:15:55', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000009, 901234, 03, 000009, TO_TIMESTAMP('28-10-2022 13:05:41', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000010, 012345, 01, 000010, TO_TIMESTAMP('17-11-2022 19:48:23', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000011, 129456, 04, 000011, TO_TIMESTAMP('09-12-2022 11:30:55', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000012, 294567, 05, 000012, TO_TIMESTAMP('01-01-2023 14:55:20', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000013, 340678, 06, 000013, TO_TIMESTAMP('23-01-2023 17:10:45', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000014, 421789, 07, 000014, TO_TIMESTAMP('16-02-2023 09:25:30', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000015, 534890, 03, 000015, TO_TIMESTAMP('14-03-2023 12:40:15', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000016, 623901, 01, 000016, TO_TIMESTAMP('26-03-2023 15:55:50', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000017, 776012, 02, 000017, TO_TIMESTAMP('09-04-2023 18:30:40', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000018, 834123, 04, 000018, TO_TIMESTAMP('17-05-2023 10:40:15', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000019, 834123, 04, 000018, TO_TIMESTAMP('17-05-2023 10:43:34', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000020, 834123, 04, 000018, TO_TIMESTAMP('17-05-2023 10:45:55', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000021, 905634, 05, 000019, TO_TIMESTAMP('14-06-2023 12:50:50', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000022, 905634, 05, 000019, TO_TIMESTAMP('14-06-2023 13:20:10', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000023, 013445, 06, 000020, TO_TIMESTAMP('03-07-2023 16:30:15', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000024, 013445, 06, 000020, TO_TIMESTAMP('03-07-2023 16:45:25', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000025, 776012, 07, 000021, TO_TIMESTAMP('09-07-2023 12:32:40', 'DD-MM-YYYY HH24:MI:SS'));
INSERT INTO orders VALUES (000026, 623901, 07, 000022, TO_TIMESTAMP('15-07-2023 19:55:50', 'DD-MM-YYYY HH24:MI:SS'));

CREATE TABLE order_line ( 
    CONSTRAINT PK_order_line PRIMARY KEY (order_num, item_num), 
    order_num NUMBER(6) NOT NULL,  
    item_num NUMBER(3) NOT NULL,   
    order_quantity NUMBER(3) NOT NULL, 
    FOREIGN KEY (order_num) REFERENCES orders(order_num), 
    FOREIGN KEY (item_num) REFERENCES item(item_num), 
    CONSTRAINT check_order_quantity CHECK (order_quantity > 0) 
);  

INSERT INTO order_line VALUES (000001, 17, 3);
INSERT INTO order_line VALUES (000001, 18, 2);
INSERT INTO order_line VALUES (000002, 3, 2);
INSERT INTO order_line VALUES (000002, 19, 3);
INSERT INTO order_line VALUES (000003, 12, 3);
INSERT INTO order_line VALUES (000004, 6, 1);
INSERT INTO order_line VALUES (000004, 7, 2);
INSERT INTO order_line VALUES (000004, 16, 1);
INSERT INTO order_line VALUES (000005, 3, 1);
INSERT INTO order_line VALUES (000006, 8, 1);
INSERT INTO order_line VALUES (000007, 22, 1);
INSERT INTO order_line VALUES (000007, 12, 2);
INSERT INTO order_line VALUES (000008, 3, 3);
INSERT INTO order_line VALUES (000009, 2, 2);
INSERT INTO order_line VALUES (000009, 4, 2);
INSERT INTO order_line VALUES (000010, 18, 2);
INSERT INTO order_line VALUES (000010, 11, 1);
INSERT INTO order_line VALUES (000011, 1, 3);
INSERT INTO order_line VALUES (000012, 18, 1);
INSERT INTO order_line VALUES (000012, 8, 2);
INSERT INTO order_line VALUES (000013, 4, 3);
INSERT INTO order_line VALUES (000014, 24, 2);
INSERT INTO order_line VALUES (000014, 16, 1);
INSERT INTO order_line VALUES (000015, 9, 2);
INSERT INTO order_line VALUES (000016, 3, 1);
INSERT INTO order_line VALUES (000017, 4, 2);
INSERT INTO order_line VALUES (000018, 10, 2);
INSERT INTO order_line VALUES (000019, 18, 1);
INSERT INTO order_line VALUES (000020, 16, 3);
INSERT INTO order_line VALUES (000021, 6, 2);
INSERT INTO order_line VALUES (000022, 15, 1);
INSERT INTO order_line VALUES (000023, 22, 2);
INSERT INTO order_line VALUES (000024, 12, 1);
INSERT INTO order_line VALUES (000024, 11, 2);
INSERT INTO order_line VALUES (000024, 10, 1);
INSERT INTO order_line VALUES (000025, 9, 1);
INSERT INTO order_line VALUES (000025, 25, 1);
INSERT INTO order_line VALUES (000026, 7, 2);

CREATE TABLE training_plan ( 
    train_id NUMBER(3) PRIMARY KEY, 
    tutor_id NUMBER(4) NOT NULL, 
    train_description VARCHAR2(60) NOT NULL, 
    train_level VARCHAR2(20) NOT NULL, 
    CONSTRAINT AK_training_plan UNIQUE (tutor_id) 
); 

INSERT INTO training_plan VALUES (1, 1, 'Leadership and Management Skills', 'Manager');
INSERT INTO training_plan VALUES (2, 17, 'Strategic Planning and Decision Making', 'Manager');
INSERT INTO training_plan VALUES (3, 25, 'Effective Communication and Interpersonal Skills', 'Supervisor');
INSERT INTO training_plan VALUES (4, 15, 'Teamwork and Collaboration', 'Waiter');
INSERT INTO training_plan VALUES (5, 19, 'Customer Service Excellence', 'Waiter');
INSERT INTO training_plan VALUES (6, 28, 'Conflict Resolution and Problem-Solving', 'Waiter');
INSERT INTO training_plan VALUES (7, 35, 'Time Management and Productivity', 'Waiter');
INSERT INTO training_plan VALUES (8, 18, 'Food Safety and Hygiene', 'Waiter');
INSERT INTO training_plan VALUES (9, 27, 'Menu Planning and Recipe Development', 'Chef');
INSERT INTO training_plan VALUES (10, 21, 'Culinary Techniques and Food Preparation', 'Chef');
INSERT INTO training_plan VALUES (11, 4, 'Effective Service Recovery and Handling Difficult Customers', 'Waiter');
INSERT INTO training_plan VALUES (12, 3, 'Creative Plating and Presentation', 'Chef');
INSERT INTO training_plan VALUES (13, 7, 'Upselling Techniques and Sales Skills', 'Waiter');
INSERT INTO training_plan VALUES (14, 52, 'Effective Customer Communication', 'Rider');
INSERT INTO training_plan VALUES (15, 42, 'Route and Navigation Training', 'Rider');

CREATE TABLE staff ( 
    staff_num NUMBER(4) PRIMARY KEY, 
    outlet_num NUMBER(2) NOT NULL, 
    train_id NUMBER(3), 
    staff_title CHAR(2) NOT NULL, 
    staff_fname VARCHAR2(50) NOT NULL, 
    staff_lname VARCHAR2(50) NOT NULL, 
    staff_tel CHAR(11) NOT NULL, 
    staff_street VARCHAR2(100) NOT NULL, 
    staff_suburb VARCHAR2(50) NOT NULL, 
    staff_postcode NUMBER(5) NOT NULL, 
    staff_position VARCHAR2(25) NOT NULL, 
    staff_doe DATE NOT NULL, 
    staff_dspln VARCHAR2(50) DEFAULT NULL, 
    manager_id NUMBER(4), 
    FOREIGN KEY (outlet_num) REFERENCES outlet(outlet_num), 
    FOREIGN KEY (train_id) REFERENCES training_plan(train_id), 
    CONSTRAINT check_staff_title CHECK (staff_title IN ('Ms', 'Mr')), 
    CONSTRAINT check_staff_postcode CHECK (staff_postcode BETWEEN 10000 AND 99999), 
    CONSTRAINT AK_staff UNIQUE (staff_tel) 

); 


INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (1, 01, NULL, 'Mr', 'James', 'Bonne', '0123434789', '21, Jalan Merdeka', 'Petaling Jaya', 47400, 'Manager', TO_DATE('01-02-2022', 'DD-MM-YYYY'),NULL);
INSERT INTO staff 
VALUES (2, 01, 6, 'Ms', 'Emily', 'Charles', '0134564590', '22, Jalan Bahagia', 'Shah Alam', 40000, 'Senior Employee', TO_DATE('03-04-2022', 'DD-MM-YYYY'), 'Suspension without pay',1);
INSERT INTO staff  
VALUES (3, 01, 9, 'Mr', 'Daniel', 'Chad', '0156678901', '23, Jalan Ceria', 'Klang', 41000, 'Senior Employee', TO_DATE('05-04-2022', 'DD-MM-YYYY'), 'Suspension without pay',1);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (4, 01, 3, 'Ms', 'Olivia', 'Taylor', '0156789012', '24, Jalan Damai', 'Petaling Jaya', 47400, 'Supervisor', TO_DATE('07-08-2022', 'DD-MM-YYYY'),1);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (5, 01, 6, 'Mr', 'William', 'Davis', '0132789012', '25, Jalan Sejahtera', 'Subang Jaya', 47500, 'Part Time Employee', TO_DATE('09-10-2022', 'DD-MM-YYYY'),1);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (6, 01, 9, 'Ms', 'Sophia', 'Wilson', '0178976234', '26, Jalan Indah', 'Shah Alam', 40000, 'Junior Employee', TO_DATE('11-11-2022', 'DD-MM-YYYY'),1);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (7, 04, 3, 'Mr', 'Michael', 'Thomas', '0189872345', '27, Jalan Ceria', 'Klang', 41000, 'Supervisor', TO_DATE('13-02-2023', 'DD-MM-YYYY'),28);
INSERT INTO staff 
VALUES (8, 04, 4, 'Ms', 'Emma', 'Clark', '0190165456', '28, Jalan Bahagia', 'Petaling Jaya', 47400, 'Senior Employee', TO_DATE('15-04-2022', 'DD-MM-YYYY'), 'Written Warning',28);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (9, 02, 9, 'Mr', 'Jacob', 'Anderson', '0101984567', '29, Jalan Raya', 'Subang Jaya', 47500, 'Senior Employee', TO_DATE('01-06-2022', 'DD-MM-YYYY'),17);
INSERT INTO staff 
VALUES (10, 02, 8, 'Ms', 'Isabella', 'Lee', '0112325678', '30, Jalan Damai', 'Shah Alam', 40000, 'Senior Employee', TO_DATE('19-05-2022', 'DD-MM-YYYY'), 'Demotion',17);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (11, 02, NULL, 'Mr', 'David', 'Martin', '0125456789', '31, Jalan Sejahtera', 'Klang', 41000, 'Junior Employee', TO_DATE('01-10-2022', 'DD-MM-YYYY'),17);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (12, 02, 7, 'Ms', 'Ava', 'Harris', '0134560990', '32, Jalan Indah', 'Petaling Jaya', 47400, 'Junior Employee', TO_DATE('23-12-2022', 'DD-MM-YYYY'),17);
INSERT INTO staff 
VALUES (13, 02, 11, 'Mr', 'Daniel', 'Walker', '0140978901', '33, Jalan Bahagia', 'Subang Jaya', 47500, 'Part Time Employee', TO_DATE('25-09-2022', 'DD-MM-YYYY'), 'Verbal Warning',17);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (14, 04, 10, 'Ms', 'Sophia', 'Lewis', '0156784312', '34, Jalan Ceria', 'Shah Alam', 40000, 'Part Time Employee', TO_DATE('27-04-2022', 'DD-MM-YYYY'),28);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (15, 05, 1, 'Mr', 'Matthew', 'Brown', '0167843123', '35, Jalan Damai', 'Klang', 41000, 'Manager', TO_DATE('29-06-2022', 'DD-MM-YYYY'),NULL);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (16, 04, 13, 'Ms', 'Emily', 'Johnson', '0178921234', '36, Jalan Sejahtera', 'Petaling Jaya', 47400, 'Senior Employee', TO_DATE('31-08-2022', 'DD-MM-YYYY'),28);
INSERT INTO staff
VALUES (17, 02, 1, 'Mr', 'David', 'Taylor', '0182112345', '37, Jalan Indah', 'Subang Jaya', 47500, 'Manager', TO_DATE('02-11-2022', 'DD-MM-YYYY'), 'Suspension without pay',NULL);
INSERT INTO staff 
VALUES (18, 06, 3, 'Ms', 'Olivia', 'Davis', '0190123256', '38, Jalan Raya', 'Shah Alam', 40000, 'Supervisor', TO_DATE('04-01-2023', 'DD-MM-YYYY'), 'Verbal Warning',35);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (19, 03, 2, 'Mr', 'James', 'Clark', '0101214567', '39, Jalan Bahagia', 'Klang', 41000, 'Manager', TO_DATE('06-03-2022', 'DD-MM-YYYY'),NULL);
INSERT INTO staff 
VALUES (20, 03, 13, 'Ms', 'Sophia', 'Anderson', '0112376678', '40, Jalan Ceria', 'Petaling Jaya', 47400, 'Part Time Employee', TO_DATE('08-05-2022', 'DD-MM-YYYY'), 'Verbal Warning',19);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (21, 03, 9, 'Mr', 'William', 'Martin', '0123546789', '41, Jalan Damai', 'Subang Jaya', 47500, 'Senior Employee', TO_DATE('10-07-2022', 'DD-MM-YYYY'),19);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (22, 03, 3,'Ms', 'Emma', 'Harris', '0134565890', '42, Jalan Sejahtera', 'Shah Alam', 40000, 'Supervisor', TO_DATE('12-09-2022', 'DD-MM-YYYY'),19);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (23, 03, NULL, 'Mr', 'Jacob', 'Lewis', '0145768901', '43, Jalan Indah', 'Klang', 41000, 'Junior Employee', TO_DATE('14-10-2022', 'DD-MM-YYYY'),19);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (24, 03, 12, 'Ms', 'Isabella', 'Brown', '0156439012', '44, Jalan Bahagia', 'Petaling Jaya', 47400, 'Junior Employee', TO_DATE('16-10-2022', 'DD-MM-YYYY'),19);
INSERT INTO staff VALUES (25, 07, 2, 'Mr', 'Daniel', 'Taylor', '0167893223', '45, Jalan Ceria', 'Subang Jaya', 47500, 'Manager', TO_DATE('18-03-2022', 'DD-MM-YYYY'), 'Verbal Warning',NULL);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id) 
VALUES (26, 05, 11, 'Ms', 'Olivia', 'Johnson', '0178761234', '46, Jalan Raya', 'Shah Alam', 40000, 'Senior Employee', TO_DATE('20-05-2022', 'DD-MM-YYYY'),15);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (27, 04, NULL, 'Mr', 'Patrick', 'Bonne', '0189032345', '47, Jalan Merdeka', 'Klang', 41000, 'Senior Employee', TO_DATE('22-07-2022', 'DD-MM-YYYY'),28);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (28, 04, 2, 'Ms', 'Lexi', 'Green', '0175442288', '52, Jalan Kenari', 'Puchong Jaya', 63000, 'Manager', TO_DATE('22-07-2022', 'DD-MM-YYYY'),NULL);
INSERT INTO staff 
VALUES (29, 05, 7, 'Mr', 'Adam', 'Smith', '0163226789', '1, Jalan Raya', 'Subang Jaya', 47500, 'Part Time Employee', TO_DATE('01-12-2022', 'DD-MM-YYYY'), 'Written Warning',15);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (30, 05, 12, 'Ms', 'Sophie', 'Johnson', '0174511890', '2, Jalan Bahagia', 'Shah Alam', 40000, 'Senior Employee', TO_DATE('03-04-2022', 'DD-MM-YYYY'),15);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (31, 05, 10, 'Mr', 'Ethan', 'Brown', '0185675501', '3, Jalan Ceria', 'Klang', 41000, 'Senior Employee', TO_DATE('05-06-2022', 'DD-MM-YYYY'),15);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (32, 06, 7, 'Ms', 'Aria', 'Taylor', '0196783312', '4, Jalan Damai', 'Petaling Jaya', 47400, 'Senior Employee', TO_DATE('07-06-2022', 'DD-MM-YYYY'),35);
INSERT INTO staff 
VALUES (33, 06, 9, 'Mr', 'Noah', 'Davis', '0107866123', '5, Jalan Sejahtera', 'Subang Jaya', 47500, 'Part Time Employee', TO_DATE('09-08-2022', 'DD-MM-YYYY'), 'Written Warning',35);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (34, 06, NULL, 'Ms', 'Mia', 'Wilson', '0118881234', '6, Jalan Indah', 'Shah Alam', 40000, 'Junior Employee', TO_DATE('11-12-2022', 'DD-MM-YYYY'),35);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (35, 06, 1, 'Mr', 'Liam', 'Thomas', '0129099345', '7, Jalan Ceria', 'Klang', 41000, 'Manager', TO_DATE('13-01-2023', 'DD-MM-YYYY'),NULL);
INSERT INTO staff 
VALUES (36, 07, NULL, 'Ms', 'Zoe', 'Chester', '0130123356', '8, Jalan Bahagia', 'Petaling Jaya', 47400, 'Senior Employee', TO_DATE('15-04-2022', 'DD-MM-YYYY'), 'Written Warning',25);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (37, 07, 12, 'Mr', 'Elijah', 'Anderson', '0141234447', '9, Jalan Raya', 'Subang Jaya', 47500, 'Junior Employee', TO_DATE('17-01-2023', 'DD-MM-YYYY'),25);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (38, 07, 11, 'Ms', 'Ava', 'Lee', '0152665678', '10, Jalan Damai', 'Shah Alam', 40000, 'Senior Employee', TO_DATE('19-07-2022', 'DD-MM-YYYY'),25);
INSERT INTO staff 
VALUES (39, 07, 5, 'Mr', 'James', 'Martin', '0163776789', '11, Jalan Sejahtera', 'Klang', 41000, 'Junior Employee', TO_DATE('21-10-2022', 'DD-MM-YYYY'),'Demotion',25);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (40, 01, 14, 'Mr', 'Oliver', 'Smith', '0174534890', '12, Jalan Raya', 'Subang Jaya', 47500, 'Senior Employee', TO_DATE('02-03-2022', 'DD-MM-YYYY'),1);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (41, 01, 15, 'Ms', 'Ava', 'Johnson', '0155678901', '13, Jalan Bahagia', 'Shah Alam', 40000, 'Part Time Employee', TO_DATE('04-03-2023', 'DD-MM-YYYY'),1);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (42, 02, 14, 'Mr', 'Elijah', 'Brown', '0196780912', '14, Jalan Ceria', 'Klang', 41000, 'Senior Employee', TO_DATE('06-07-2022', 'DD-MM-YYYY'),17);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (43, 02, 14, 'Ms', 'Scarlett', 'Taylor', '0107832123', '15, Jalan Damai', 'Petaling Jaya', 47400, 'Part Time Employee', TO_DATE('08-09-2022', 'DD-MM-YYYY'),17);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (44, 03, NULL, 'Mr', 'Lucas', 'Davis', '0118908734', '16, Jalan Sejahtera', 'Subang Jaya', 47500, 'Senior Employee', TO_DATE('09-07-2022', 'DD-MM-YYYY'),19);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (45, 03, 14, 'Ms', 'Chloe', 'Wilson', '0129019845', '17, Jalan Indah', 'Shah Alam', 40000, 'Junior Employee', TO_DATE('12-01-2023', 'DD-MM-YYYY'),19);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (46, 04, 15, 'Mr', 'Muhammad', 'Thomas', '0130083456', '18, Jalan Ceria', 'Klang', 41000, 'Senior Employee', TO_DATE('14-02-2022', 'DD-MM-YYYY'),28);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (47, 04, 15, 'Ms', 'Amelia', 'Clark', '0141044567', '19, Jalan Bahagia', 'Petaling Jaya', 47400, 'Part Time Employee', TO_DATE('16-03-2022', 'DD-MM-YYYY'),28);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (48, 05, NULL, 'Mr', 'Mason', 'Anderson', '0152343578', '20, Jalan Raya', 'Subang Jaya', 47500, 'Junior Employee', TO_DATE('18-10-2022', 'DD-MM-YYYY'),15);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (49, 05, 15, 'Ms', 'Harper', 'Lee', '0163452589', '21, Jalan Damai', 'Shah Alam', 40000, 'Part Time Employee', TO_DATE('20-05-2023', 'DD-MM-YYYY'),15);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (50, 06, 14, 'Mr', 'Ethan', 'Martin', '0174537890', '22, Jalan Sejahtera', 'Klang', 41000, 'Senior Employee', TO_DATE('22-06-2022', 'DD-MM-YYYY'),35);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (51, 06, NULL, 'Ms', 'Lily', 'Harris', '0185629901', '23, Jalan Indah', 'Petaling Jaya', 47400, 'Senior Employee', TO_DATE('24-07-2022', 'DD-MM-YYYY'),35);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (52, 07, 15, 'Mr', 'Owen', 'Lewis', '0196209012', '24, Jalan Ceria', 'Subang Jaya', 47500, 'Senior Employee', TO_DATE('26-08-2022', 'DD-MM-YYYY'),25);
INSERT INTO staff (staff_num, outlet_num, train_id, staff_title, staff_fname, staff_lname, staff_tel, staff_street, staff_suburb, staff_postcode, staff_position, staff_doe, manager_id)
VALUES (53, 07, NULL, 'Ms', 'Zoe', 'Brown', '0107839123', '25, Jalan Bahagia', 'Shah Alam', 40000, 'Part Time Employee', TO_DATE('28-01-2023', 'DD-MM-YYYY'),25);


alter table training_plan add 
foreign key(tutor_id) references staff(staff_num);

CREATE TABLE staff_list ( 
    CONSTRAINT PK_staff_list PRIMARY KEY (order_num, staff_num), 
    order_num NUMBER(6) NOT NULL, 
    staff_num NUMBER(4) NOT NULL, 
    job VARCHAR2(20) NOT NULL, 
    FOREIGN KEY (order_num) REFERENCES orders(order_num), 
    FOREIGN KEY (staff_num) REFERENCES staff(staff_num) 
); 

INSERT INTO staff_list VALUES (000001, 2, 'Waiter');
INSERT INTO staff_list VALUES (000001, 3, 'Chef');
INSERT INTO staff_list VALUES (000002, 10, 'Waiter');
INSERT INTO staff_list VALUES (000002, 9, 'Chef');
INSERT INTO staff_list VALUES (000003, 20, 'Telephone Operator');
INSERT INTO staff_list VALUES (000003, 44, 'Rider');
INSERT INTO staff_list VALUES (000003, 21, 'Chef');
INSERT INTO staff_list VALUES (000004, 8, 'Telephone Operator');
INSERT INTO staff_list VALUES (000004, 46, 'Rider');
INSERT INTO staff_list VALUES (000004, 14, 'Chef');
INSERT INTO staff_list VALUES (000005, 26, 'Waiter');
INSERT INTO staff_list VALUES (000005, 30, 'Chef');
INSERT INTO staff_list VALUES (000006, 32, 'Waiter');
INSERT INTO staff_list VALUES (000006, 33, 'Chef');
INSERT INTO staff_list VALUES (000007, 38, 'Telephone Operator');
INSERT INTO staff_list VALUES (000007, 52, 'Rider');
INSERT INTO staff_list VALUES (000007, 36, 'Chef');
INSERT INTO staff_list VALUES (000008, 13, 'Telephone Operator');
INSERT INTO staff_list VALUES (000008, 42, 'Rider');
INSERT INTO staff_list VALUES (000008, 11, 'Chef');
INSERT INTO staff_list VALUES (000009, 23, 'Waiter');
INSERT INTO staff_list VALUES (000009, 24, 'Chef');
INSERT INTO staff_list VALUES (000010, 5, 'Telephone Operator');
INSERT INTO staff_list VALUES (000010, 40, 'Rider');
INSERT INTO staff_list VALUES (000010, 6, 'Chef');
INSERT INTO staff_list VALUES (000011, 16, 'Waiter');
INSERT INTO staff_list VALUES (000011, 27, 'Chef');
INSERT INTO staff_list VALUES (000012, 29, 'Telephone Operator');
INSERT INTO staff_list VALUES (000012, 48, 'Rider');
INSERT INTO staff_list VALUES (000012, 31, 'Chef');
INSERT INTO staff_list VALUES (000013, 35, 'Telephone Operator');
INSERT INTO staff_list VALUES (000013, 50, 'Rider');
INSERT INTO staff_list VALUES (000013, 34, 'Chef');
INSERT INTO staff_list VALUES (000014, 39, 'Telephone Operator');
INSERT INTO staff_list VALUES (000014, 53, 'Rider');
INSERT INTO staff_list VALUES (000014, 37, 'Chef');
INSERT INTO staff_list VALUES (000015, 22, 'Telephone Operator');
INSERT INTO staff_list VALUES (000015, 45, 'Rider');
INSERT INTO staff_list VALUES (000015, 21, 'Chef');
INSERT INTO staff_list VALUES (000016, 1, 'Telephone Operator');
INSERT INTO staff_list VALUES (000016, 41, 'Rider');
INSERT INTO staff_list VALUES (000016, 6, 'Chef');
INSERT INTO staff_list VALUES (000017, 12, 'Telephone Operator');
INSERT INTO staff_list VALUES (000017, 43, 'Rider');
INSERT INTO staff_list VALUES (000017, 11, 'Chef');
INSERT INTO staff_list VALUES (000018, 16, 'Waiter');
INSERT INTO staff_list VALUES (000018, 14, 'Chef');
INSERT INTO staff_list VALUES (000019, 8, 'Waiter');
INSERT INTO staff_list VALUES (000019, 14, 'Chef');
INSERT INTO staff_list VALUES (000020, 28, 'Telephone Operator');
INSERT INTO staff_list VALUES (000020, 47, 'Rider');
INSERT INTO staff_list VALUES (000020, 27, 'Chef');
INSERT INTO staff_list VALUES (000021, 26, 'Telephone Operator');
INSERT INTO staff_list VALUES (000021, 49, 'Rider');
INSERT INTO staff_list VALUES (000021, 30, 'Chef');
INSERT INTO staff_list VALUES (000022, 29, 'Waiter');
INSERT INTO staff_list VALUES (000022, 31, 'Chef');
INSERT INTO staff_list VALUES (000023, 32, 'Telephone Operator');
INSERT INTO staff_list VALUES (000023, 51, 'Rider');
INSERT INTO staff_list VALUES (000023, 34, 'Chef');
INSERT INTO staff_list VALUES (000024, 35, 'Waiter');
INSERT INTO staff_list VALUES (000024, 34, 'Chef');
INSERT INTO staff_list VALUES (000025, 39, 'Waiter');
INSERT INTO staff_list VALUES (000025, 36, 'Chef');
INSERT INTO staff_list VALUES (000026, 39, 'Waiter');
INSERT INTO staff_list VALUES (000026, 37, 'Chef');

CREATE TABLE vehicle ( 
    veh_num VARCHAR2(15) PRIMARY KEY, 
    outlet_num NUMBER(2) NOT NULL, 
    veh_product VARCHAR2(50) NOT NULL, 
    veh_type VARCHAR2(10) NOT NULL, 
    veh_dop DATE NOT NULL, 
    veh_lchecked DATE, 
    veh_mileage NUMBER(6) NOT NULL, 
    FOREIGN KEY (outlet_num) REFERENCES outlet(outlet_num), 
    CONSTRAINT check_veh_mileage CHECK (veh_mileage > 0), 
    CONSTRAINT AK_vehicle UNIQUE (veh_mileage) 
); 

INSERT INTO vehicle VALUES ('WAB123', 01, 'Honda Jazz', 'Car', TO_DATE('01/01/2023', 'DD/MM/YYYY'), TO_DATE('01/07/2023', 'DD/MM/YYYY'), 51023);
INSERT INTO vehicle VALUES ('XYZ456', 02, 'Toyota Vios', 'Car', TO_DATE('15/03/2023', 'DD/MM/YYYY'), TO_DATE('02/07/2023', 'DD/MM/YYYY'), 75410);
INSERT INTO vehicle VALUES ('DEF789', 03, 'Perodua Myvi', 'Car', TO_DATE('10/06/2022', 'DD/MM/YYYY'), TO_DATE('05/06/2023', 'DD/MM/YYYY'), 25521);
INSERT INTO vehicle VALUES ('GHI012', 04, 'Proton Saga', 'Car', TO_DATE('25/09/2022', 'DD/MM/YYYY'), TO_DATE('15/05/2023', 'DD/MM/YYYY'), 35238);
INSERT INTO vehicle VALUES ('JKL345', 05, 'Nissan Almera', 'Car', TO_DATE('03/04/2023', 'DD/MM/YYYY'), TO_DATE('21/06/2023', 'DD/MM/YYYY'), 85193);
INSERT INTO vehicle VALUES ('MNO678', 06, 'Kia Picanto', 'Car', TO_DATE('19/08/2022', 'DD/MM/YYYY'), TO_DATE('16/05/2023', 'DD/MM/YYYY'), 15580);
INSERT INTO vehicle VALUES ('PQR901', 07, 'Hyundai i10', 'Car', TO_DATE('07/11/2022', 'DD/MM/YYYY'), TO_DATE('27/04/2023', 'DD/MM/YYYY'), 95435);
INSERT INTO vehicle VALUES ('STU234', 02, 'Mazda2', 'Car', TO_DATE('12/02/2023', 'DD/MM/YYYY'), TO_DATE('14/07/2023', 'DD/MM/YYYY'), 60765);
INSERT INTO vehicle VALUES ('VWX567', 03, 'Suzuki Swift', 'Car', TO_DATE('30/10/2022', 'DD/MM/YYYY'), TO_DATE('29/04/2023', 'DD/MM/YYYY'), 20507);
INSERT INTO vehicle VALUES ('YZA890', 01, 'Renault Kwid', 'Car', TO_DATE('22/07/2022', 'DD/MM/YYYY'), TO_DATE('11/02/2023', 'DD/MM/YYYY'), 72753);
INSERT INTO vehicle VALUES ('BCD123', 04, 'Honda CBR150R', 'Motor', TO_DATE('14/05/2022', 'DD/MM/YYYY'), TO_DATE('06/05/2023', 'DD/MM/YYYY'), 44444);
INSERT INTO vehicle VALUES ('EFG456', 05, 'Yamaha MT-15', 'Motor', TO_DATE('28/02/2022', 'DD/MM/YYYY'), TO_DATE('12/04/2023', 'DD/MM/YYYY'), 55016);
INSERT INTO vehicle VALUES ('HIJ789', 06, 'Kawasaki Ninja 250', 'Motor', TO_DATE('06/09/2022', 'DD/MM/YYYY'), TO_DATE('18/03/2023', 'DD/MM/YYYY'), 30735);
INSERT INTO vehicle VALUES ('KLM012', 07, 'Suzuki GSX-S150', 'Motor', TO_DATE('11/11/2022', 'DD/MM/YYYY'), TO_DATE('23/01/2023', 'DD/MM/YYYY'), 70634);
INSERT INTO vehicle VALUES ('NOP345', 03, 'KTM RC 200', 'Motor', TO_DATE('19/04/2022', 'DD/MM/YYYY'), TO_DATE('02/02/2023', 'DD/MM/YYYY'), 67535);
INSERT INTO vehicle VALUES ('QRS678', 01, 'SYM VF3i', 'Motor', TO_DATE('09/03/2023', 'DD/MM/YYYY'), TO_DATE('28/03/2023', 'DD/MM/YYYY'), 15265);
INSERT INTO vehicle VALUES ('TUV901', 02, 'Honda RS150R', 'Motor', TO_DATE('15/08/2022', 'DD/MM/YYYY'), TO_DATE('07/06/2023', 'DD/MM/YYYY'), 82667);
INSERT INTO vehicle VALUES ('WXY234', 04, 'Yamaha NMax', 'Motor', TO_DATE('02/05/2022', 'DD/MM/YYYY'), TO_DATE('18/03/2023', 'DD/MM/YYYY'), 102039);
INSERT INTO vehicle VALUES ('ZAB567', 05, 'Perodua Alza', 'Van', TO_DATE('18/03/2023', 'DD/MM/YYYY'), TO_DATE('03/05/2023', 'DD/MM/YYYY'), 40242);
INSERT INTO vehicle VALUES ('BCD890', 06, 'Toyota Avanza', 'Van', TO_DATE('25/06/2022', 'DD/MM/YYYY'), TO_DATE('21/02/2023', 'DD/MM/YYYY'), 91544);
INSERT INTO vehicle VALUES ('EFG123', 07, 'Nissan NV200', 'Van', TO_DATE('09/03/2023', 'DD/MM/YYYY'), TO_DATE('06/04/2023', 'DD/MM/YYYY'), 60923);
 
CREATE TABLE stock ( 
    stock_num NUMBER(6) PRIMARY KEY, 
    stock_name VARCHAR2(50) NOT NULL, 
    stock_category VARCHAR2(25) NOT NULL, 
    CONSTRAINT AK_stock UNIQUE (stock_name)
); 

INSERT INTO stock VALUES (1, 'Garlic', 'Vegetables');
INSERT INTO stock VALUES (2, 'Mozzarella Cheese', 'Dairy');
INSERT INTO stock VALUES (3, 'Pepperoni', 'Meat');
INSERT INTO stock VALUES (4, 'Tomato Sauce', 'Sauces');
INSERT INTO stock VALUES (5, 'Green Peppers', 'Vegetables');
INSERT INTO stock VALUES (6, 'Sausage', 'Meat');
INSERT INTO stock VALUES (7, 'Mushrooms', 'Vegetables');
INSERT INTO stock VALUES (8, 'Black Olives', 'Vegetables');
INSERT INTO stock VALUES (9, 'Anchovies', 'Seafood');
INSERT INTO stock VALUES (10, 'Onions', 'Vegetables');
INSERT INTO stock VALUES (11, 'Basil', 'Herbs');
INSERT INTO stock VALUES (12, 'Cheddar Cheese', 'Dairy');
INSERT INTO stock VALUES (13, 'Pineapple', 'Fruits');
INSERT INTO stock VALUES (14, 'Ham', 'Meat');
INSERT INTO stock VALUES (15, 'Spinach', 'Vegetables');
INSERT INTO stock VALUES (16, 'Oregano', 'Herbs');
INSERT INTO stock VALUES (17, 'Artichoke Hearts', 'Vegetables');
INSERT INTO stock VALUES (18, 'Parmesan Cheese', 'Dairy');
INSERT INTO stock VALUES (19, 'Red Pepper Flakes', 'Spices');
INSERT INTO stock VALUES (20, 'Fresh Basil Leaves', 'Herbs');

CREATE TABLE stock_list (
    CONSTRAINT PK_stock_list PRIMARY KEY (stock_num, outlet_num),  
    stock_num NUMBER(6) NOT NULL, 
    outlet_num NUMBER(2) NOT NULL, 
    stock_quantity NUMBER(4) NOT NULL, 
    stock_manfdate DATE, 
    stock_expdate DATE NOT NULL, 
    FOREIGN KEY (stock_num) REFERENCES stock(stock_num), 
    FOREIGN KEY (outlet_num) REFERENCES outlet(outlet_num), 
    CONSTRAINT check_stock_quantity CHECK (stock_quantity >=0) 
);  

/*
In a pizza restaurant, efficient management of stock condition and expiration dates is crucial. To optimise the
daily stock checking process and promptly remove expired items from inventory, an index is implemented. This index 
enhances the retrieval of stock information based on expiration dates, allowing the restaurant to maintain accurate stock
records and promptly take actions to ensure the freshness and quality of stocks.
*/
CREATE INDEX idx_stock_expdate ON stock_list(stock_expdate);

INSERT INTO stock_list VALUES (1, 01, 13, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (1, 02, 23, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (1, 03, 25, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (1, 04, 13, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (1, 05, 22, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (1, 06, 21, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (1, 07, 25, TO_DATE('15-07-2023', 'DD-MM-YYYY'), TO_DATE('21-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (2, 01, 17, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (2, 02, 12, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('22-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (2, 03, 27, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('24-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (2, 04, 17, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (2, 05, 13, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('23-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (2, 06, 24, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('24-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (2, 07, 28, TO_DATE('15-07-2023', 'DD-MM-YYYY'), TO_DATE('25-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (3, 01, 25, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('25-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (3, 02, 15, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('27-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (3, 03, 19, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('29-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (3, 04, 25, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('26-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (3, 05, 15, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('28-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (3, 06, 19, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('29-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (3, 07, 18, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('29-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (4, 01, 20, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (4, 02, 29, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('22-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (4, 03, 10, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('24-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (4, 04, 21, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (4, 05, 27, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('24-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (4, 06, 13, TO_DATE('17-07-2023', 'DD-MM-YYYY'), TO_DATE('27-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (4, 07, 22, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (5, 01, 24, TO_DATE('09-07-2023', 'DD-MM-YYYY'), TO_DATE('22-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (5, 02, 25, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('25-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (5, 03, 22, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('27-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (5, 04, 24, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('23-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (5, 05, 21, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('25-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (5, 06, 25, TO_DATE('15-07-2023', 'DD-MM-YYYY'), TO_DATE('28-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (5, 07, 20, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('23-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (6, 01, 19, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (6, 02, 19, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (6, 03, 23, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('22-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (6, 04, 17, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (6, 05, 16, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (6, 06, 23, TO_DATE('15-07-2023', 'DD-MM-YYYY'), TO_DATE('23-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (6, 07, 15, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (7, 01, 16, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (7, 02, 11, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (7, 03, 24, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (7, 04, 16, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (7, 05, 12, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (7, 06, 23, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (7, 07, 16, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (8, 01, 23, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (8, 02, 20, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (8, 03, 23, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (8, 04, 23, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (8, 05, 19, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (8, 06, 24, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (8, 07, 23, TO_DATE('15-07-2023', 'DD-MM-YYYY'), TO_DATE('21-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (9, 01, 18, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (9, 02, 17, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (9, 03, 13, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (9, 04, 18, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (9, 05, 15, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (9, 06, 14, TO_DATE('15-07-2023', 'DD-MM-YYYY'), TO_DATE('21-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (9, 07, 19, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (10, 01, 16, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (10, 02, 15, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (10, 03, 14, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (10, 04, 17, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (10, 05, 12, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (10, 06, 14, TO_DATE('16-07-2023', 'DD-MM-YYYY'), TO_DATE('22-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (10, 07, 15, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (11, 01, 31, TO_DATE('09-07-2023', 'DD-MM-YYYY'), TO_DATE('15-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (11, 02, 20, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (11, 03, 28, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (11, 04, 31, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (11, 05, 21, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (11, 06, 27, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (11, 07, 32, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (12, 01, 21, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (12, 02, 20, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (12, 03, 21, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (12, 04, 20, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (12, 05, 19, TO_DATE('15-07-2023', 'DD-MM-YYYY'), TO_DATE('21-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (12, 06, 22, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (12, 07, 21, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (13, 01, 19, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (13, 02, 11, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (13, 03, 12, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (13, 04, 17, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (13, 05, 14, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (13, 06, 16, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (13, 07, 19, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (14, 01, 24, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (14, 02, 23, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (14, 03, 21, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (14, 04, 25, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (14, 05, 23, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (14, 06, 22, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (14, 07, 24, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (15, 01, 19, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (15, 02, 18, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (15, 03, 17, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (15, 04, 19, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (15, 05, 18, TO_DATE('15-07-2023', 'DD-MM-YYYY'), TO_DATE('21-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (15, 06, 16, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (15, 07, 20, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (16, 01, 27, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (16, 02, 29, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (16, 03, 28, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (16, 04, 25, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (16, 05, 24, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (16, 06, 22, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (16, 07, 26, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (17, 01, 20, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (17, 02, 22, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (17, 03, 24, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (17, 04, 18, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (17, 05, 19, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (17, 06, 21, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (17, 07, 23, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (18, 01, 29, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (18, 02, 28, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (18, 03, 27, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (18, 04, 26, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (18, 05, 25, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (18, 06, 22, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (18, 07, 20, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (19, 01, 18, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (19, 02, 19, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (19, 03, 21, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (19, 04, 17, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (19, 05, 16, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (19, 06, 20, TO_DATE('13-07-2023', 'DD-MM-YYYY'), TO_DATE('19-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (19, 07, 19, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (20, 01, 25, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (20, 02, 28, TO_DATE('12-07-2023', 'DD-MM-YYYY'), TO_DATE('18-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (20, 03, 30, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (20, 04, 24, TO_DATE('10-07-2023', 'DD-MM-YYYY'), TO_DATE('16-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (20, 05, 23, TO_DATE('11-07-2023', 'DD-MM-YYYY'), TO_DATE('17-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (20, 06, 22, TO_DATE('14-07-2023', 'DD-MM-YYYY'), TO_DATE('20-07-2023', 'DD-MM-YYYY'));
INSERT INTO stock_list VALUES (20, 07, 23, TO_DATE('09-07-2023', 'DD-MM-YYYY'), TO_DATE('15-07-2023', 'DD-MM-YYYY'));

--create views
CREATE OR REPLACE VIEW staff_cust_view AS  
SELECT s.staff_num, s.staff_fname, s.staff_lname, o.order_num, sl.job,  cu.cust_num, cu.cust_fname || ' ' || cu.cust_lname AS cust_name
FROM staff s, staff_list sl, orders o, customer cu
WHERE s.staff_num = sl.staff_num
AND sl.order_num = o.order_num
AND o.cust_num = cu.cust_num ORDER BY staff_num;

CREATE OR REPLACE VIEW outlet_trans_view AS 
SELECT UNIQUE o.outlet_num, t.trans_num, od.cust_num, t.trans_time, t.trans_amount 
FROM outlet o, orders od, transactions t 
WHERE o.outlet_num = od.outlet_num 
AND od.trans_num = t.trans_num
ORDER BY o.outlet_num;
