# GrocerySQL
(Project dated April 2020)
This project was to learn how to set up and manage a grocery store database within MySQL and establish a connection to a text editor (Sublime).
The project then can be used with a virtual environment set up in Terminal to run a Flask server that displays the SQL database content.
It allows me to see and connect through a 3 tier application (UI, Backend, Database). This is to help understand how projects are executed in a corporate environment. 
Further personalization could be used to design a web app but would be too time consuming for a class project. Bootstrtap was unfortunately not able to be used as project took too long. This is why it only presents a basic HTML, CSS web page.


# Project Walk-through

## Idea:

3 Tier Application:

  1. UI (HTML, CSS, Bootsrtap) ---> Products Web Page
  2. Backend (Python, Flask) ---> Products Python API
  3. Database (mySQL Workbench) ---> Products Database Table


## Code Walk-Through:


- Set-Up and Open Local Host Instance in MySQL Workbench
    - this allows you to create new data base schemas, new tables, insert records, etc.

- Create a new schema and name it "GroceryInventory"
    - Can also run a query script in MySQL command prompt to create a schema
    - ``` 
      CREATE SCHEMA 'GroceryInventory'; ```

- Right click on "GroceryInventory" under Schemas and create a table

- Name the table "products"
  - Add new columns and their data types
  - "product_id" --> Datatype: INT --> marked with PK (primary key), NN (not null), AI (auto increment)
  - "name" --> Datatype: VARCHAR(100) --> marked with NN (not null)
  - "uom_id" --> Datatype: INT --> marked with NN (not null) --> UOM = unit of measurement
  - "price_per_unit" --> Datatype: DOUBLE --> marked with NN (not null) --> DOUBLE doesn't haveto be whole number ($2.5, $6.2)
  - SQL Script Query:
      ``` 
        CREATE TABLE 'GroceryInventory'.'products'(
           'product_id' INT NOT NULL AUTO_INCREMENT,
           'name' VARCHAR(100) NOT NULL,
           'uom_id' INT NOT NULL,
           'price_per_unit' DOUBLE NOT NULL,
         PRIMARY KEY('product_id')); ```
         
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



- 
