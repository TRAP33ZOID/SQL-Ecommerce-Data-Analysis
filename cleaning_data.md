What issues will you address by cleaning the data?
1) all_sessions:
    A) There was a lot of missing values. some colummns were completely empty while others had 90%+ of the data missing. The columns that were 100% emetpy were removed using the SQL code below:
        ALTER TABLE all_sessions
        DROP COLUMN productRefundAmount, 
        DROP COLUMN searchKeyword, 
        DROP COLUMN itemRevenue, 
        DROP COLUMN itemQuantity;
   





Queries:
Below, provide the SQL queries you used to clean your data.
