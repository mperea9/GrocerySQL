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
    - ``` CREATE SCHEMA 'GroceryInventory'; ```
