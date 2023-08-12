What issues will you address by cleaning the data?
1) all_sessions:
    A) There was a lot of missing values. some colummns were completely empty while others had 90%+ of the data missing. The columns that were 100% emetpy were removed using the SQL code below:
   B) There are columns that have multiple placeholders with the same meaning. For example city & country have place holders as (not set or not available). unified them to unkown
   C) updated columns with missing values.
   

2) Products:
       A) Set columns such as sentiment score and sentiment magnitude that have missing data to 0. it can also be set to the mean of the data column but my personal choice was to put a 0.

3) sales_by_sku:
       A)deleted SKU's that were present in sales_by_sku but not in products.
4) sales_report:
       A) filled in missing values in the ratio column with 0. similary to previous numerical columns, this coulve been set to the mean of the column but i choose 0.

   
Queries:
1)A)
  
    ALTER TABLE all_sessions
    DROP COLUMN productRefundAmount, 
    DROP COLUMN searchKeyword, 
    DROP COLUMN itemRevenue, 
    DROP COLUMN itemQuantity;
  
B)
      
    UPDATE all_sessions
    SET city = NULL
    WHERE city = '(not set)' OR city = 'not available in demo dataset';
    
    UPDATE all_sessions
    SET country = NULL
    WHERE country = '(not set)' OR country = 'not available in demo dataset';
    
    -- Repeated for other columns with placeholder values
C)
  
    UPDATE all_sessions
    SET city = 'Unknown'
    WHERE city IS NULL;
    
    UPDATE all_sessions
    SET v2ProductCategory = 'Not Specified'
    WHERE v2ProductCategory IS NULL;
    
3)    B)
          
    UPDATE products
    SET sentimentScore = 0
    WHERE sentimentScore IS NULL;
    
    UPDATE products
    SET sentimentMagnitude = 0
    WHERE sentimentMagnitude IS NULL;

4) A)
   
        DELETE FROM sales_by_sku
        WHERE productSKU NOT IN (SELECT SKU FROM products);
   
6)    A)
  
    UPDATE sales_report
    SET ratio = 0
    WHERE ratio IS NULL;
  


        
