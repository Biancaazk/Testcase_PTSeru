# PT Seru Test Case

Performance Tracker-Dashboard

### Folder Link : https://drive.google.com/drive/u/3/folders/1Rx2XOkQT7jCggo3cu1ZynJl-NhC-zZQV

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
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4 : It was observed that in none of the columns errors & empty values were present except table named "Orders".
Removing Blank Rows:

        = Table.SelectRows(#"Filtered Rows", each not List.IsEmpty(List.RemoveMatchingItems(Record.FieldValues(_), {"", null})))

![image](https://github.com/Biancaazk/Testcase_PTSeru/assets/148216513/5cc46a53-9731-489a-9117-df3190d4b34b)

- Step 5 :