# PT Seru Test Case

Performance Tracker-Dashboard

### Power BI File : https://drive.google.com/file/d/1v-6vZ8Nihy6KK9j23PWelrGQ5jX_sAjt/view?usp=drive_link
### Dashboard Link : https://drive.google.com/file/d/1qyJ8HZxo3r8ve6BgwY560d8mP4BLlDlB/view?usp=drive_link

## Problem Statement

To enable informed decision-making and strategic planning, there's a need for a comprehensive dashboard that visualizes key sales metrics, incorporating data segmentation by product categories (Female, Male, Unisex). The dashboard must effectively track and display:

1. **Sales by Segment:** Visualizing monthly sales distribution across different product categories to identify patterns and trends.
2. **Orders by Month:** Monitoring the volume of orders placed each month to gauge overall business activity and customer demand.
3. **Total Category Growth by Year:** Analyzing the year-over-year growth in sales for different product categories to understand market dynamics and category performance.
4. **Total Segment Growth by Year:** Evaluating the annual growth rates within each product segment to pinpoint opportunities and challenges.

However, the current dashboard indicates potential issues in growth rate calculations, showing -100% growth for both category and segment growth metrics, suggesting a need for review and correction of these calculations to ensure accurate reporting and analysis.

### Steps Followed 
- Step 1 : Load data into Power BI Desktop, dataset is a csv file.

- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.

- Step 3 : Also since by default, profile will be opened only for 1000 rows so we need to select "column profiling based on entire dataset".

- Step 4 : It was observed that in none of the columns errors & empty values were present except table named "Orders".
Removing Blank Rows:

        = Table.SelectRows(#"Filtered Rows", each not List.IsEmpty(List.RemoveMatchingItems(Record.FieldValues(_), {"", null})))

![image](https://github.com/Biancaazk/Testcase_PTSeru/assets/148216513/5cc46a53-9731-489a-9117-df3190d4b34b)

- Step 5 : Create a new table named "Calendar" to focusing on time period

        Calendar = CALENDAR(DATE(2022, 1, 1), DATE(2023, 12, 31))

![image](https://github.com/Biancaazk/Testcase_PTSeru/assets/148216513/bc0a1651-1427-49bd-9fbe-924cead83152)

- Step 6 : Make relationship between the tables

![image](https://github.com/Biancaazk/Testcase_PTSeru/assets/148216513/ba555db4-347f-4c4b-84f0-a1a78ad7e980)


- Step 7 : To proceed with the dashboard visualization requirements:
    1. **Sales by Segment** will likely use data from **Detail.xlsx**, categorizing sales by month and possibly by 'Category'.
    2. **Orders by Month** might leverage **Orders.xlsx** to count orders over time, requiring a monthly aggregation of the data.
    3. **Total Category Growth by Year** and **Total Segment Growth by Year** might also primarily use **Detail.xlsx** and **Orders.xlsx**, focusing on growth metrics within categories and segments across years.
.

- Step 8 : Create **Sales by Segment** Bar Chart:
We need "Month" from **Calendar** or we can use "Order Date" from **Orders.xlsx** if we don't create Calendar table.
From **Detail.xlsx**, we need the amount and category as we treat it as Segment.

![image](https://github.com/Biancaazk/Testcase_PTSeru/assets/148216513/76dbab12-62ed-4d61-978d-9585407dc47a)

- Step 9 : Create **Orders by Month** Line Chart:
We need "Month" from **Calendar**, same as the previous one.
From **Detail.xlsx** or **Orders.xlsx**, we need OrderID to see the number of orders.

![image](https://github.com/Biancaazk/Testcase_PTSeru/assets/148216513/5207d6a6-1323-47f4-90ab-d04d3d179dde)

- Step 10 : Create **Total Category Growth by Year** Percentage:
First step to do, we calculate the Previous Year Category:

    Previous Year Category = 
    CALCULATE(
    SUM('Details_1'[Amount]),
    DATEADD('Calendar'[Date], -1, YEAR),
    ALLEXCEPT('Details_1', 'Details_1'[Sub-Category])
    )

2nd step we calculate the Total Category Sales (This will be usefull for both Category Growth and Segment Growth):

    Total Category Sales = 
    CALCULATE(
    SUM('Details_1'[Amount]),
    'Calendar'[Year] = YEAR(TODAY())  // or a specific year if needed
    )

and the last step is calculate the YoY% Category Growth:

    YoY % Category Growth = 
    DIVIDE(
    [Total Category Sales] - [Previous Year Category],
    [Previous Year Category]
    )

- Step 11 : Create **Total Segment Growth by Year** Percentage:
(To create this key, we do similiar steps to Category Growth)
First step to do, we calculate the Previous Year Segment:

    Previous Year Segment = 
    CALCULATE(
    SUM('Details_1'[Amount]),
    DATEADD('Calendar'[Date], -1, YEAR),
    ALLEXCEPT('Details_1', 'Details_1'[Category])
    )

2nd step we use the calculation of Total Category Sales that we have created, and the last step is calculate the YoY% Segment Growth: 

    YoY % Segment Growth = 
    DIVIDE(
    [Total Category Sales] - [Previous Year Segment],
    [Previous Year Segment]
    )

- Step 11 : Create another metrics if needed
- Step 12 : Customize the dashboard
- Step 13 : Identify the insight from the dashboard result





