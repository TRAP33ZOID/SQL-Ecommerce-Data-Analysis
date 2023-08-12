Question 1: Which country has the highest number of visitors?

SQL Queries:

          SELECT country, COUNT(DISTINCT fullVisitorId) as total_visitors
          FROM all_sessions
          GROUP BY country
          ORDER BY total_visitors DESC
           
Answer: "United States"
  
Question 2: What is the average time spent on the site by visitors from different channels?

SQL Queries:

          SELECT channelGrouping, AVG(timeOnSite) as average_time_on_site
          FROM all_sessions
          GROUP BY channelGrouping
          ORDER BY average_time_on_site DESC;
          
Answer:

        "(Other)"	417.3333333333333333
        "Affiliates"	296.9714285714285714
        "Direct"	245.3272027373823781
        "Paid Search"	245.1742919389978214
        "Organic Search"	220.8337314859053989
        "Referral"	205.2125000000000000
        "Display"	181.7818181818181818

Question 3: How many products, on average, does a visitor view during their session?

SQL Queries:
  
          SELECT AVG(products) as average_products_viewed
          FROM (
              SELECT fullVisitorId, COUNT(DISTINCT productSKU) as products
              FROM all_sessions
              GROUP BY fullVisitorId
          ) as ProductCounts;

Answer: 1.06271532025592350418
