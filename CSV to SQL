import pandas as pd
import psycopg2 as pg
import psycopg2.extras as extras
import os
from pathlib import Path


base_dir = Path('C:/Users/mini/Desktop/vscode_python/Python-Project/e-Commerce Dataset')
csv_files = (
    base_dir / 'customers.csv',
    base_dir / 'orders.csv',
    base_dir / 'sellers.csv',
    base_dir / 'products.csv',
    base_dir / 'geolocation.csv',
    base_dir / 'payments.csv',
    base_dir / 'order_items.csv',
    )


conn = pg.connect(
    host='localhost',
    database='postgres',
    user='postgres',
    password='anwar103',
    port='5432'
)


cursor = conn.cursor()


#function that checks true or false if a table exists in the database
def table_exists_psycopg2(conn, table_name):
    # establish a cursor to execute the query
    # query checks if the table exists in the information_schema.tables
    # the query will return either true if the subqurery finds at lease one matching row and false otherwise
    # then we return the results of the query by extratcing the row of the first column which is just the boolean result
    try:
        cur = conn.cursor()
        cur.execute("SELECT EXISTS (SELECT FROM information_schema.tables WHERE table_name = %s)", (table_name,))
        return cur.fetchone()[0]
    # error handling method. If the query fails then it will print the error message and return false
    except pg.Error as e:
        print(f"Error checking table existence: {e}")
        return False
    # closes cursor object cur
    finally:
        if cur:
            cur.close()


# function that inserts every row of dataframe into an already existing table in postgresql
def execute_values(conn, df, table):
    # first converts each row of the dataframe into a tuple by using to_numpy() and then make a list of all of the tuples
    # this is done to make a list of each row of data
    # this is important becasue the list is in the correct format for the execute_values function to insert the data into the table in postgresql
    tuples = [tuple(x) for x in df.to_numpy()]
   
    # df.columns returns the column names of the dataframe which is then turned into a list
    # "','.join" joins the list into a string connected by commas
    cols = ','.join(list(df.columns))
    # parameterized SQL query to execute. we will insert into the table the columns from the cols varaible
    query = "INSERT INTO %s(%s) VALUES %%s" % (table, cols)
    # created a cursor object which is used to execute sql commands and interact with the databse
    cursor = conn.cursor()
    try:
        extras.execute_values(cursor, query, tuples)
        conn.commit()
    # error handling method. If the query fails then it will rollback the changes made to the database and close the cursor
    # except (Exception) as error: Catches any error that occurs during the insert or commit process.
    # print("Error: %s" % error): Displays the error message to help with debugging.
    # onn.rollback(): Undoes any part of the transaction that may have executed before the error.
    # cursor.close(): Closes the cursor to clean up resources.
    # return 1: Returns an error indicator (value 1) to the calling code.
    except (Exception) as error:
        print("Error: %s" % error)
        conn.rollback()
        cursor.close()
        return 1
    # success message
    print("the dataframe is inserted")
    cursor.close()


#uses the table_exists_psycopg2 function to see if the df_orders table exists in the database
# if it does it is truncated if not then it is created with the specified columns and datatypes
for file in csv_files:
    csv_location = file


    df = pd.read_csv(csv_location)
    table_name = file.stem


    #sets each column to lowercase
    df.columns = df.columns.str.lower()
    #replaces the spaces in each column with underscores
    df.columns = df.columns.str.replace(' ', '_')
   
    if table_exists_psycopg2(conn, table_name) == True:
        cursor.execute(f'truncate table {table_name}')
    elif table_exists_psycopg2(conn, table_name) == False:
    # Map pandas dtypes to PostgreSQL data types
        dtype_mapping = {
            'int64': 'INT',
            'float64': 'FLOAT',
            'datetime64[ns]': 'DATE',
            'object': 'VARCHAR(255)', # Default for strings, adjust as needed
            'bool': 'BOOLEAN'
        }


    # Generate column definitions for the CREATE TABLE statement
        columns_with_types = []
        for col, dtype in df.dtypes.items():
            pg_type = dtype_mapping.get(str(dtype), 'VARCHAR(255)') # Default to VARCHAR if no specific mapping
            columns_with_types.append(f"{col} {pg_type}")


        create_table_query = f"CREATE TABLE {table_name} ({', '.join(columns_with_types)})"
        cursor.execute(create_table_query)
        conn.commit()
        print(f"Table '{table_name}' created successfully.")


    #uses the execute_values function to insert the dataframe into the df_orders table
    execute_values(conn, df, table_name)


cursor.close()
conn.close()
