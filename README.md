# GrocerySQL
(Project dated April 2020)
This project was to learn how to set up and manage a grocery store database within MySQL and establish a connection to a text editor (Sublime).
The project then can be used with a virtual environment set up in Terminal to run a Flask server that displays the SQL database content.
It allows me to see and connect through a 3 tier application (UI, Backend, Database). This is to help understand how projects are executed in a corporate environment. 
Further personalization could be used to design a web app but would be too time consuming for a class project. Bootstrtap was unfortunately not able to be used as project took too long. This is why it only presents a basic HTML, CSS web page.


# Project Walk-through

# Idea:

3 Tier Application:

  1. UI (HTML, CSS, Bootsrtap) ---> Products Web Page
  2. Backend (Python, Flask) ---> Products Python API
  3. Database (mySQL Workbench) ---> Products Database Table


# Code Walk-Through:

## Database Creation:


- Set-Up and Open Local Host Instance in MySQL Workbench
    - this allows you to create new data base schemas, new tables, insert records, etc.

- Create a new schema and name it "GroceryInventory"
    - Can also run a query script in MySQL command prompt to create a schema
    - ``` 
      CREATE SCHEMA 'GroceryInventory';

- Right click on "GroceryInventory" under Schemas and create a table

- Name the table "products"
  - Add new columns and their data types
  - "product_id" --> Datatype: INT --> marked with PK (primary key), NN (not null), AI (auto increment) --> product reference ID
  - "name" --> Datatype: VARCHAR(100) --> marked with NN (not null) --> name of product
  - "uom_id" --> Datatype: INT --> marked with NN (not null) --> UOM = unit of measurement
  - "price_per_unit" --> Datatype: DOUBLE --> marked with NN (not null) --> DOUBLE doesn't have to be whole number ($2.5, $6.2) --> prce per item
  - SQL Script Query:
      ``` 
        CREATE TABLE 'GroceryInventory'.'products'(
           'product_id' INT NOT NULL AUTO_INCREMENT,
           'name' VARCHAR(100) NOT NULL,
           'uom_id' INT NOT NULL,
           'price_per_unit' DOUBLE NOT NULL,
         PRIMARY KEY('product_id'));
         
  - Apply and finish --> new table created

- Create another table named "uom" (stands for unit of measurement)
  - Add new columns and their data types
  - "uom_id" --> Datatype: INT --> marked with PK, NN, AI
  - "uom_name" --> Datatype: VARCHAR(45) --> marked with NN
  - SQL Query Script:
     ``` 
         CREATE TABLE 'GroceryInventory'.'uom'(
            'uom_id' INT NOT NULL AUTO_INCREMENT,
            'uom_name' VARCHAR(45) NOT NULL,
         PRIMARY_KEY('uom_id'));
  
  - Apply and finish --> new table created

- Under Scehmas click on the uom table created
  - Enter Values in the rows of the table
  - "uom_id" add values 1 and 2
  - "uom_name" add values "each" and "kg"
  - This means "uom_id" 1 is equal to "each" and "uom_id" 2 is equal to "kg"
  - SQL Query Script:
     ``` 
         INSERT INTO 'GroceryInventory'.'uom'('uom_id', 'uom_name') VALUES ('1', 'each');
         INSERT INTO 'GroceryInventory'.'uom'('uom_id', 'uom_name') VALUES ('2', 'kg'); 

  - Apply and finish


- Under Scehmas click on the products table created
  - Enter Values in the rows of the table
  - For rows "product_id", "name", "uom_id", and "price_per_unit"
  - Add these values respectively, "1", "toothpaste", "1", "30"
  - SQL Query Script:
     ``` 
         INSERT INTO 'GroceryInventory'.'products'('product_id', 'name', 'uom_id', price_per_unit) VALUES ('1', 'toothpaste', '1', '30');

  - Apply and finish



- Set up table relationships with foreign keys
  - Foreign Key definiton: A foreign key column in a table points to a column with unique values in another table (often the primary key column) to create a way of cross-referencing the two tables. If a column is assigned a foreign key, each row of that column must contain a value that exists in the 'foreign' column it references.
  - Simple: Links columns from different tables and runs validations
  - Under Schemas and under GroceryInventory tables, click the gear icon when you hover over products table
  - At the bottom, click on "Foreign Keys"
  - We define the foreign key under "Foreign Key Name"
  - Create a foreign key "fk_uom_id"
  - Under "Referenced Table" drop down select 'GroceryInventory'.'uom'
  - Next, on the right side, select "uom_id" under "Column" and "uom_id" under "Referenced Column"
  - Again to the right under "Foreign Key Optons"
  - Set "On Update: " to "RESTRICT"
  - Leave "On Delete: " on NO ACTION
  - This allows for the restrictions and prevents wrong alues being associated
  - SQL Query Script:
    ```
      ALTER TABLE 'GroceryInventory'.'products'
      ADD INDEX 'fk_uom_id_idx' ('uom_id' ASC) VISIBLE;
      ;
      ALTER TABLE 'GroceryInventory'.'products'
      ADD CONSTRAINT 'fk_uom_id'
        FOREIGN KEY('uom_id')
        REFERENCES 'GroceryInventory'.'uom'('uom_id')
        ON DELETE NO ACTION
        ON UPDATE RESTRICT);
        
   - Apply and finish

- Create another table "orders"
  - Add new columns and their data types
  - "order_id" --> Datatype: INT --> marked with PK (primary key), NN (not null), AI (auto increment)
  - "customer_name" --> Datatype: VARCHAR(100) --> marked with NN (not null) --> customer's name
  - "total" --> Datatype: DOUBLE --> marked with NN (not null) --> for the total price of order
  - "datetime" --> Datatype: DATETIME --> marked with NN (not null) --> For day and time order was made
  - SQL Script Query:
      ``` 
        CREATE TABLE 'GroceryInventory'.'orders'(
           'order_id' INT NOT NULL AUTO_INCREMENT,
           'customer_name' VARCHAR(100) NOT NULL,
           'total' DOUBLE NOT NULL,
           'datetime' DATETIME NOT NULL,
         PRIMARY KEY('order_id'));
         
  - Apply and finish --> new table created

- Create another table "order_details"
  - Add new columns and their data types
  - "order_id" --> Datatype: INT --> marked with PK (primary key), NN (not null)
  - "product_id" --> Datatype: INT --> marked with NN (not null)
  - "quantity" --> Datatype: DOUBLE --> marked with NN (not null) --> quantity of order
  - "total_price" --> Datatype: DOUBLE --> marked with NN (not null) --> total price of the order
  - SQL Script Query:
      ``` 
        CREATE TABLE 'GroceryInventory'.'order_details'(
           'order_id' INT NOT NULL,
           'product_id' INT NOT NULL,
           'quantity' DOUBLE NOT NULL,
           'total_price' DOUBLE NOT NULL,
         PRIMARY KEY('order_id'));
         
  - Apply and finish --> new table created

- Apply Foreign Keys to new tables
  - Create foreign key "fk_order_id" in the order_details table
  - Reference to 'GroceryInventory'.'orders' table
  - Select "order_id" from column
  - Select "order_id" from reference column
  - Select RESTRICT for "On Update: "
  - Create another foreign key "fk_product_id" in the order_details table
  - Reference to 'GroceryInventory'.'products' table
  - Select "product_id" from column
  - Select "product_id" from reference column
  - Select RESTRICT for "On Update: "
  - SQL Query Script:
    ```
      ALTER TABLE 'GroceryInventory'.'order_details'
      ADD INDEX 'fk_product_id_idx' ('product_id' ASC) VISIBLE;
      CONSTRAINT 'fk_order_id'
        FOREIGN KEY('order_id')
        REFERENCES 'GroceryInventory'.'orders'('order_id')
        ON DELETE NO ACTION
        ON UPDATE RESTRICT
      CONSTRAINT 'fk_product_id'
        FOREIGN KEY('product_id')
        REFERENCES 'GroceryInventory'.'products'('product_id')
        ON DELETE NO ACTION
        ON UPDATE RESTRICT);
        
  - Apply and finsh


- Create a Diagram of the Database and all its connections
  - In the top bar menu select "Database"
  - Select "Reverse Engineer"
  - Press Next
  - Press Next
  - Check "GroceryInventory"
  - Press Next
  - Press Next
  - Press Execute
  - Press Next
  - Press Finish
  - You should be able to see the diagram of the database model and relationships


## Python Code and Flask Setup:

