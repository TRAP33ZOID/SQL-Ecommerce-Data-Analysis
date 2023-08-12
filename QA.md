What are your risk areas? Identify and describe them.

    Duplicate Records: There might be duplicate entries in our datasets, leading to inflated numbers during analysis. e.g duplicate visitID in all_sessions
    Inconsistent Data:
    There might be discrepancies between datasets, such as SKUs present in one dataset but missing in another. (products, sales by sku)
    Invalid Data:
    Negative values in columns where only positive values make sense (e.g., stockLevel, total_ordered).
    Missing Data: Some datasets might have crucial missing data, leading to incomplete or misleading analyses.


QA Process:
Describe your QA process and include the SQL queries used to execute it.

1)Check for Duplicate Records:

      -- Check duplicates in all_sessions based on visitId
      SELECT visitId, COUNT(*)
      FROM all_sessions
      GROUP BY visitId
      HAVING COUNT(*) > 1;

2)Check for Invalid Data:

      -- Check for negative stockLevel in products
      SELECT COUNT(*)
      FROM products
      WHERE stockLevel < 0;
      
      -- Check for negative total_ordered in sales_by_sku
      SELECT COUNT(*)
      FROM sales_by_sku
      WHERE total_ordered < 0;
      
3)Handle Missing Data:

      -- Check for missing values in products' sentimentScore
      SELECT COUNT(*)
      FROM products
      WHERE sentimentScore IS NULL;
