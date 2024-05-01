# Balance-Sheet_Financial-Report

<h2>Description</h2>
The project is regarding creating a Balance sheet of a company 

<br />

<h2>Interactive Balance Sheets</h2>
Power BI transforms static balance sheets into interactive dashboards. This allows users to drill down into specific assets, liabilities, or equity accounts to understand their composition and trends over time.

<br />

<h2>Real-Time Updates</h2> 
With Power BI, balance sheets can be updated in real-time as data flows in from connected sources. This ensures that decision-makers always have the most current snapshot of the company's financial position.

<br />

<h2>Predictive Capabilities</h2>
Power BI's integration with AI tools can be used to forecast future balance sheet positions based on historical trends and patterns. This can help businesses anticipate future financial needs and make proactive decisions.

<br />

<h2>GUI Used</h2>

- <b>DAX</b>
- <b>DAX</b>

<h2>Program walk-through:</h2>

A)	Creating a new measure group for balance sheet: Balance sheet Analysis 

<br />

<p align="center">
Creating a table: <br/>
<img src="https://i.imgur.com/mcikis6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />

B)	Add all below Measures in the Table:

<br />
<p align="center">
Adding all Below Measures: <br/>
<img src="https://i.imgur.com/vwrA4fm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

B.1) Calculating Balance Sheet Values:
<br />
<br />
BS values =CALCULATE( SUM('Balance Sheet Data'[balance Sheet Values]),TREATAS(VALUES(Dates[Year]),'Balance Sheet Data'[Year])
<br /> -- TREATAS used to avoid connecting date table with Balance sheet table
<br /> -- Values function used create a table with required dates
<br />-- Calculate function used for removing the filter level context
<br />- Treat As functions: YouTube Links: https://www.youtube.com/watch?v=YALX5cDMSfc
<br />
<br />
B.2)	Current Assets : Current Assets = CALCULATE([BS values],'Balance Sheet Data'[Category]= "Current assets")
<br />
<br />
B.3)	Current Liabilities : Current Liabilities = CALCULATE([BS values],'Balance Sheet Data'[Category]= "Current liabilities")
<br />
<br />
B.4)	Fixed Assets: Fixed Assets = CALCULATE([BS values],'Balance Sheet Data'[Category]= "Fixed (Long-Term) Assets")
<br />
<br />
B.5)	Liabilities and owners equity: Liabilities and owners Equity = [Current Liabilities]+[Long-Term Liabilities]+[Owner's Equity]
<br />
<br />
B.6)	Long term Liabilities: Long-Term Liabilities = CALCULATE([BS values],'Balance Sheet Data'[Category]= "Long-Term Liabilities")
<br />
<br />
B.7)	Other Assets: Other Assets = CALCULATE([BS values],'Balance Sheet Data'[Category]= "Other Assets")
<br />
<br />
B.8)	Owners’ Equity: Owner's Equity = CALCULATE([BS values],'Balance Sheet Data'[Category]= "Owner's Equity")
<br />
<br />
B.9)	Total Assets: Total Assets = [Current Assets]+[Fixed Assets]+[Other Assets]
<br />
<br />
B.10)	Total Liabilities: Total Liabilities = [Current Liabilities]+[Long-Term Liabilities]
<br />
<br />
B.11)	Balance sheet all Roll-up values: 
<br />
B/S values = 
Var currentitem = SELECTEDVALUE('Balance Sheet Template'[Balance Sheet Normalized])
<br />
Return
<br />
Switch( True(),
<br />
currentitem= "Total current assets",[Current Assets],
<br />
currentitem= "Total fixed assets",[Fixed Assets],
<br />
currentitem= "Total Other Assets",[other Assets],
<br />
currentitem= "Total Assets",[Total Assets],
<br />
currentitem= "Total current liabilities",[Current Liabilities],
<br />
currentitem= "Total long-term liabilities",[Long-Term Liabilities],
<br />
currentitem= "Total owner's equity",[Owner's Equity],
<br />
currentitem= "Total Liabilities and Owner's Equity",[Liabilities and owners Equity],
<br />
currentitem= "Debt Ratio (Total Liabilities / Total Assets)",FORMAT(DIVIDE([Total Liabilities],[Total Assets],0),"0.00"),
<br />
currentitem= "Current Ratio (Current Assets / Current Liabilities)",FORMAT(DIVIDE([Current Assets],[Current Liabilities],0),"0.00"),
<br />
currentitem= "Working Capital (Current Assets - Current Liabilities)",FORMAT([Current Assets]-[Current Liabilities],"0"),
<br />
currentitem= "Assets-to-Equity Ratio (Total Assets / Owner's Equity)",FORMAT(DIVIDE([Total Assets],[Owner's Equity],0),"0.00"),
<br />
currentitem= "Debt-to-Equity Ratio (Total Liabilities / Owner's Equity)",FORMAT(DIVIDE([Total Liabilities],[Owner's Equity],0),"0.00"),
<br />
currentitem= BLANK(),"",currentitem= "Assets","",currentitem= "Current Assets","",
<br />
currentitem= "Fixed (Long-Term) Assets","",currentitem= "Other Assets","",
<br />
currentitem= "Liabilities and Owner's Equity","",currentitem= "Long-Term Liabilities","",
<br />
currentitem= "Owner's Equity","",currentitem= "Common Financial Ratios","",  
CALCULATE([BS values],FILTER('Balance Sheet Data', 'Balance Sheet Data'[Sub Category]= currentitem)))


<br />
C)	Creating a Table for Balance Sheet 

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
