\# Superstore Returns Analysis — Tableau



\*\*Objective\*\*  

Investigate rising return rates and quantify profit impact with drilldowns by geography, sub-category, and manufacturer.



\*\*Data / Tools\*\*  

Tableau Superstore (2025.1) · Tableau Desktop



\## Business Summary

\- KPI tiles: Sales, Profit, Quantity, Return Rate (returned units ÷ total units)

\- Point-in-time, YoY, and MoM trend views

\- Filters: Region, State, Sub-Category, Manufacturer

\- Top / Bottom spotlight to prioritise actions



\## Insights

\- Elevated return rates cluster in Technology and Office Supplies

\- High-volume states (e.g., CA, NY) show higher return ratios, lowering Profit Ratio

\- Manufacturers with negative return-to-profit patterns flagged for review



\## Impact

\- Quantifies profit erosion from returns  

\- Focuses vendor and SKU follow-ups  

\- Adds return KPIs to monthly business reviews  



\## Live Dashboard

\[View on Tableau Public]https://public.tableau.com/views/Superstore-ReturnTrendAnalysis/ReturnRateAnalysisTrendsRisksActions?:language=en-US\&:sid=\&:redirect=auth\&:display\_count=n\&:origin=viz\_share\_link



<div style="position: relative; height: 0; padding-bottom: 70%;">

&nbsp; <iframe src="https://public.tableau.com/views/your-dashboard-link?:showVizHome=no\&:embed=true"

&nbsp;         width="100%" height="100%"

&nbsp;         style="position:absolute; top:0; left:0; border:0;" allowfullscreen></iframe>

</div>



\## Technical Notes

\- Return Quantity: IF \[Returned] = "Yes" THEN \[Quantity] ELSE 0 END  

\- Return Rate: SUM(IF \[Returned] = "Yes" THEN \[Quantity] END) / SUM(\[Quantity])  

\- Profit Ratio: SUM(\[Profit]) / SUM(\[Sales])  

\- YoY/MoM: parameter-scoped YEAR(\[Order Date]); table calcs LOOKUP, ZN  

\- Dashboards: Overview, Trends, Rate Analysis, Risk Zones, Product Lookup  

\- Interactivity: Global filters (Region, State, Sub-Category, Manufacturer); highlight and drill-through  



