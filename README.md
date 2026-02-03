# Data-Analyst---Dynamic-Dashboards
📋 Project Overview This project focuses on extracting actionable insights from [Automotive Industry/Dataset] to help stakeholders understand [Sales revenue drivers and operational ]. By combining the querying power of SQL with the visualization capabilities of Power BI, I transformed raw data into a strategic tool for decision-making.


##Dashboard 
<img width="1362" height="671" alt="Dashboard" src="https://github.com/user-attachments/assets/a861d21a-9fb8-4510-be49-c8e5ce3ca9fb" />

Metric	Business Value

ACH % (129.9%)	Measures efficiency and sales team effectiveness.

Volumetric ACH (755)	Provides the scale of operations (Wholesale units).

TGT Variance (29.9%)	Quantifies the surplus or deficit against the business plan

##Question

- What is the most important insight here?
The most important insight is the Aug-24 peak, where Achievement (139) was nearly triple the Target (47). This suggests either a highly successful marketing campaign or an under-estimation of demand during that period.

- How did you calculate the Achievement % (129.9%) in DAX?
Answer: I created a measure using the DIVIDE function to ensure safety against division by zero errors.
ACH % = DIVIDE([Total Achievement], [Total Target], 0)

- What does the green arrow next to the 29.9% signify, and how is it built?
Answer: It’s a conditional formatting icon. It signifies that the Achievement is above the Target. I used the "Icons" feature in the formatting pane, setting a rule where if the value is > 0, display a green up-arrow.
WS Icon = 
VAR PositiveIcon = UNICHAR(9650)
VAR NagativeIcon = UNICHAR(9660)
VAR Result = IF(APAC_DUMP[WS TGT-ACH]>0,
PositiveIcon,
NagativeIcon)
RETURN Result

- Why did you choose to display both the percentage (129.9%) and the absolute number (755)?
Answer: The percentage shows efficiency (how well we are doing against the plan), while the absolute number provides scale (the actual volume handled). For an executive, knowing we are at 130% is great, but knowing that 130% equals 755 units is vital for logistics planning.

= If the "Total Target" was missing for a specific month, how would your scorecard react?
Answer: Using the DIVIDE function with a 0 or Blank as the third argument ensures the card doesn't show an "Infinity" error. It would likely show 0% or Blank, which alerts the data team to a data quality issue in the source file.

- How do you ensure the scorecard values change when a user selects a specific "Model" from the slicer?
Answer: This is handled by Power BI’s native Filter Context. As long as the Model slicer and the Sales data are part of the same relationship in the Data Model, the scorecard will automatically filter to show values only for that selection.

- In your line chart, you compare CY (Current Year) vs LY (Last Year). How do you calculate LY Sales?
Answer: I use Time Intelligence functions.
LY Sales = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Calendar'[Date]))
This allows for a direct "Apple-to-Apple" comparison of the current month vs. the same month last year.

- Your bar chart shows "TGT vs ACH" by country. Which country is underperforming, and how can you tell?
Answer: Based on the chart, countries like Cambodia and Mongolia have very low Achievement bars compared to others. However, the PER% line (orange) helps identify if they are hitting their specific small targets.

- Why did you use a Pie Chart for "Colour Wise Wholesale" instead of a Bar Chart?
Answer: I used a Pie Chart because we are looking at a "Part-to-Whole" relationship with only 3-4 categories (Black Gold, Standard Black, etc.). It’s effective here to show that "Standard Black" dominates nearly half the total volume.

- The "Aug-24" tooltip shows detailed data. Why use a Tooltip instead of putting labels on the chart?
Answer: To avoid visual clutter. Adding data labels for TGT, ACH, and PER% on every single point makes the trend line unreadable. The tooltip provides "Information on Demand" when the user hovers over a specific month of interest.

- If a stakeholder says the "Growth" line is misleading, how would you troubleshoot the data?
Answer: I would first check the Calendar Table to ensure there are no gaps in dates. Then, I would verify if the "Growth" measure is calculating a percentage change or a raw difference, and ensure the filter context (like the Year slicer) isn't accidentally excluding the comparison period.







