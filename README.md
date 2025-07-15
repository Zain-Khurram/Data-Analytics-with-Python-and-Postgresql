# Data-Analytics-with-Python-and-Postgresql

This project focuses on analyzing e-commerce data using PostgreSQL for data storage and querying, and Python with libraries like Pandas, Psycopg2, Matplotlib, and Seaborn for data manipulation, analysis, and visualization.

This repository contains scripts to load e-commerce CSV data into a PostgreSQL database and perform various analytical queries to gain insights into customer behavior, sales trends, and product performance. The project demonstrates a common workflow for data analysis, from data ingestion to generating visualizations.

## Features

- Automated Data Loading: Python script to read CSV files and automatically create/truncate tables in PostgreSQL, then insert data.
- Dynamic Table Creation: Automatically infers PostgreSQL data types from Pandas DataFrames for table creation.
- Robust Error Handling: Includes error handling for database operations to ensure data integrity.
- Comprehensive Data Analysis: Executes a series of SQL queries to extract meaningful insights from the e-commerce dataset.
- Data Visualization: Utilizes Matplotlib and Seaborn to visualize key findings, such as customer distribution by state and monthly order trends.

Getting Started
Follow these steps to set up and run the project locally.

## Dependencies
Before you begin, ensure you have the following dependencies installed:

- pandas
- psycopg2
- matplotlib
- seaborn
- numpy

pip (Python package installer)

You can install these dependencies using pip:
```Bash
pip install pandas psycopg2-binary matplotlib seaborn numpy
```
Also make sure your PostgreSQL server is running and you have a database configured.

## Configuration

This project uses environment variables for sensitive information like database credentials and file paths. Create a .env file in the root directory of your project and add the following variables:

```env
CSV_FILE_PATH='path/to/your/folder'   # Default: n/a
DB_HOST='your_db_host'                # Default: 'localhost'
DB_NAME='your_db_name'                # Default: 'postgres'
DB_USER='your_db_user'                # Default: 'postgres'
DB_PASSWORD='your_db_password'        # Default: n/a
DB_PORT='your_db_port'                # Default: '5432'
```

Replace the placeholder values with your actual database credentials and the absolute path to your CSV files. 

If these environment variables are not set, the script will use the default values specified in the code. Some default values are not present and environnment variables for these must be set

## Usage
Place your CSV files: Ensure your e-commerce CSV files (e.g., customers.csv, orders.csv, sellers.csv, products.csv, geolocation.csv, payments.csv, order_items.csv) are located a folder and the folder is in the directory specified by CSV_FOLDER_PATH in your .env file.

- First Script 
1.  **Set up your PostgreSQL database:** Ensure you have a PostgreSQL server running and accessible.
2.  **Create a `.env` file** (as described in the Configuration section) or ensure the default values in the script are correct for your setup.
3.  **Place your CSV file** at the location specified by `CSV_FILE_PATH`. The CSV file is expected is to be `orders.csv`
4.  **Run the the first script:**
    ```bash
    python "csv to sql"
    ```
The script will connect to the database, process the CSV data, and load it onto postgresql

- Second Script
5. 

## Analysis Performed
The 'sql quieries' script performs the following key analyses:

1. Unique Customer Cities: Lists all distinct cities where customers are located.

2. Order Count in 2017: Counts the total number of orders placed in the year 2017.

3. Total Sales Per Category: Calculates the sum of sales for each product category.

4. Percentage of Installment Orders: Determines the percentage of orders paid for in installments.

5. Customer Count by State: Visualizes the distribution of customers across different states.

6. Orders Per Month (2018): Shows the number of orders placed each month in 2018.

7. Average Products Per Order by City: Calculates the average number of products in an order, grouped by customer city.

8. Revenue Contribution by Product Category: Determines the percentage of total revenue contributed by each product category, ranked by sales.

9. Price-Purchase Correlation: Identifies the correlation between product price and the number of times a product has been purchased.

10. Seller Revenue Ranking: Ranks sellers based on their total revenue generated.

11. Cumulative Sales Per Month: Calculates the running total of sales each month for every year.

12. Year-over-Year Sales Growth: Computes the year-over-year growth rate of total sales.

13. Top 3 Customers by Spending (Yearly): Identifies and visualizes the top 3 customers who spent the most money each year.
