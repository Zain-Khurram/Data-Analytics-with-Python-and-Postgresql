# Data-Analytics-with-Python-and-Postgresql

E-commerce Data Analysis with PostgreSQL and Python
This project focuses on analyzing e-commerce data using PostgreSQL for data storage and querying, and Python with libraries like Pandas, Psycopg2, Matplotlib, and Seaborn for data manipulation, analysis, and visualization.

Table of Contents
Project Overview

Features

Getting Started

Prerequisites

Installation

Environment Variables

Usage

Data Source

Analysis Performed

Contributing

License

Project Overview
This repository contains scripts to load e-commerce CSV data into a PostgreSQL database and perform various analytical queries to gain insights into customer behavior, sales trends, and product performance. The project demonstrates a common workflow for data analysis, from data ingestion to generating visualizations.

Features
Automated Data Loading: Python script to read CSV files and automatically create/truncate tables in PostgreSQL, then insert data.

Dynamic Table Creation: Automatically infers PostgreSQL data types from Pandas DataFrames for table creation.

Robust Error Handling: Includes error handling for database operations to ensure data integrity.

Comprehensive Data Analysis: Executes a series of SQL queries to extract meaningful insights from the e-commerce dataset.

Data Visualization: Utilizes Matplotlib and Seaborn to visualize key findings, such as customer distribution by state and monthly order trends.

Getting Started
Follow these steps to set up and run the project locally.

Prerequisites
Before you begin, ensure you have the following installed:

Python 3.x

PostgreSQL

pip (Python package installer)

Installation
Clone the repository:

Bash

git clone https://github.com/yourusername/your-repo-name.git
cd your-repo-name
Install Python dependencies:

Bash

pip install pandas psycopg2-binary matplotlib seaborn numpy
Set up your PostgreSQL database:
Make sure your PostgreSQL server is running and you have a database configured.

Environment Variables
This project uses environment variables for sensitive information like database credentials and file paths. Create a .env file in the root directory of your project and add the following variables:

DB_HOST=localhost
DB_NAME=postgres
DB_USER=postgres
DB_PASSWORD=your_db_password
DB_PORT=5432
CSV_FOLDER_PATH=/path/to/your/csv/files
Replace the placeholder values with your actual database credentials and the absolute path to your CSV files.

Usage
Place your CSV files: Ensure your e-commerce CSV files (e.g., customers.csv, orders.csv, sellers.csv, products.csv, geolocation.csv, payments.csv, order_items.csv) are located in the directory specified by CSV_FOLDER_PATH in your .env file.

Run the data loading script: This script will connect to your PostgreSQL database, create/truncate tables, and insert the data from your CSV files.

Bash

python data_loader.py # Assuming your data loading script is named data_loader.py
Run the analysis script: This script will execute the SQL queries and generate visualizations.

Bash

python analysis.py # Assuming your analysis script is named analysis.py
Data Source
The project uses a simulated or real-world e-commerce dataset, typically consisting of the following CSV files:

customers.csv: Information about customers.

orders.csv: Details about orders placed.

sellers.csv: Information about sellers.

products.csv: Product details.

geolocation.csv: Geolocation data.

payments.csv: Payment information for orders.

order_items.csv: Details of items within each order.

Analysis Performed
The analysis.py script performs the following key analyses:

Unique Customer Cities: Lists all distinct cities where customers are located.

Order Count in 2017: Counts the total number of orders placed in the year 2017.

Total Sales Per Category: Calculates the sum of sales for each product category.

Percentage of Installment Orders: Determines the percentage of orders paid for in installments.

Customer Count by State: Visualizes the distribution of customers across different states.

Orders Per Month (2018): Shows the number of orders placed each month in 2018.

Average Products Per Order by City: Calculates the average number of products in an order, grouped by customer city.

Revenue Contribution by Product Category: Determines the percentage of total revenue contributed by each product category, ranked by sales.

Price-Purchase Correlation: Identifies the correlation between product price and the number of times a product has been purchased.

Seller Revenue Ranking: Ranks sellers based on their total revenue generated.

Cumulative Sales Per Month: Calculates the running total of sales each month for every year.

Year-over-Year Sales Growth: Computes the year-over-year growth rate of total sales.

Top 3 Customers by Spending (Yearly): Identifies and visualizes the top 3 customers who spent the most money each year.
