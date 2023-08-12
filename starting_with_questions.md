Answer the following questions and provide the SQL queries used to find the answer.

**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**

SQL Queries:

            SELECT city, country, SUM(totalTransactionRevenue) AS total_revenue
            FROM all_sessions
            GROUP BY city, country
            ORDER BY total_revenue DESC;

Answer:

            "San Francisco"	"United States"	1564320000

**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:

            SELECT city, country, AVG(productQuantity) AS avg_products_ordered
            FROM all_sessions
            GROUP BY city, country;


Answer:

        "Seattle"	"United States"	1.00000000000000000000
        "Dublin"	"Ireland"	1.00000000000000000000
        "not available in demo dataset"	"Finland"	1.00000000000000000000
        "Sunnyvale"	"United States"	1.00000000000000000000
        "not available in demo dataset"	"Canada"	1.00000000000000000000
        "Bengaluru"	"India"	1.00000000000000000000
        "not available in demo dataset"	"France"	1.00000000000000000000
        "San Francisco"	"United States"	1.00000000000000000000
        "Chicago"	"United States"	1.00000000000000000000
        "Dallas"	"United States"	1.00000000000000000000
        "Palo Alto"	"United States"	1.00000000000000000000
        "San Jose"	"United States"	1.00000000000000000000
        "Ann Arbor"	"United States"	1.00000000000000000000
        "not available in demo dataset"	"Colombia"	1.00000000000000000000
        "not available in demo dataset"	"Mexico"	1.00000000000000000000
        "Columbus"	"United States"	1.00000000000000000000
        "Detroit"	"United States"	1.00000000000000000000
        "(not set)"	"United States"	1.00000000000000000000
        "not available in demo dataset"	"Argentina"	1.00000000000000000000
        "Los Angeles"	"United States"	1.00000000000000000000
        "Mountain View"	"United States"	1.00000000000000000000
        "New York"	"United States"	1.1666666666666667
        "Houston"	"United States"	2.0000000000000000
        "Atlanta"	"United States"	4.0000000000000000
        "Salem"	"United States"	8.0000000000000000
        "Madrid"	"Spain"	10.0000000000000000
        "not available in demo dataset"	"United States"	10.5833333333333333

**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**

SQL Queries:

            SELECT city, country, v2ProductCategory, COUNT(*) AS category_count
            FROM all_sessions
            GROUP BY city, country, v2ProductCategory
            ORDER BY category_count DESC;



Answer: first 10 lines

        "not available in demo dataset"	"United States"	"Home/Shop by Brand/YouTube/"	613
        "not available in demo dataset"	"United States"	"Home/Apparel/Men's/Men's-T-Shirts/"	435
        "not available in demo dataset"	"United States"	"Home/Apparel/"	288
        "not available in demo dataset"	"United States"	"Home/Electronics/"	280
        "not available in demo dataset"	"United States"	"Home/Shop by Brand/Google/"	223
        "not available in demo dataset"	"United States"	"(not set)"	217
        "not available in demo dataset"	"United Kingdom"	"Home/Shop by Brand/YouTube/"	189
        "not available in demo dataset"	"United States"	"Home/Office/"	188
        "not available in demo dataset"	"United States"	"Home/Apparel/Men's/Men's-Outerwear/"	184
        "not available in demo dataset"	"United States"	"Home/Drinkware/"	164





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

                WITH ranked_products AS (
                  SELECT city, country, v2ProductName, productQuantity,
                         ROW_NUMBER() OVER (PARTITION BY city, country ORDER BY productQuantity DESC) AS rank
                  FROM all_sessions
                )
                SELECT city, country, v2ProductName, productQuantity
                FROM ranked_products
                WHERE rank = 1
                ORDER BY country;

Answer: exmaples from the table

            "Buenos Aires"	"Argentina"	"Google Ballpoint Pen Black"
            "not available in demo dataset"	"Argentina"	"YouTube Hard Cover Journal"
            "Santa Fe"	"Argentina"	"Google Phone Sanitizer"
            "Rosario"	"Argentina"	"Google Men's Vintage Badge Tee Black"
            "not available in demo dataset"	"Armenia"	"Windup Android"
            "Brisbane"	"Australia"	"YouTube Wool Heather Cap Heather/Black"
            "Perth"	"Australia"	"YouTube Custom Decals"

**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

            SELECT city, country, SUM(totalTransactionRevenue) AS total_revenue,
                   AVG(totalTransactionRevenue) AS avg_revenue
            FROM all_sessions
            GROUP BY city, country
            ORDER BY avg_revenue;

Answer:

        "Zurich"	"Switzerland"	16990000	16990000.000000000000
        "Columbus"	"United States"	21990000	21990000.000000000000
        "Houston"	"United States"	38980000	38980000.000000000000
        "Mountain View"	"United States"	483360000	60420000.000000000000
        "New York"	"United States"	530360000	66295000.000000000000
        "New York"	"Canada"	67990000	67990000.000000000000
        "Austin"	"United States"	157780000	78890000.000000000000
        "Toronto"	"Canada"	82160000	82160000.000000000000
        "San Bruno"	"United States"	103770000	103770000.000000000000
        "San Francisco"	"United States"	1564320000	130360000.00000000
        "San Jose"	"United States"	262380000	131190000.000000000000
        "Chicago"	"United States"	449520000	149840000.00000000
        "Nashville"	"United States"	157000000	157000000.000000000000
        "Palo Alto"	"United States"	608000000	202666666.66666667
        "Los Angeles"	"United States"	479480000	239740000.00000000
        "not available in demo dataset"	"United States"	6092560000	243702400.00000000
        "Sunnyvale"	"United States"	992230000	248057500.00000000
        "Sydney"	"Australia"	358000000	358000000.00000000
        "Seattle"	"United States"	358000000	358000000.00000000
        "Atlanta"	"United States"	854440000	427220000.00000000
        "Tel Aviv-Yafo"	"Israel"	602000000	602000000.00000000
