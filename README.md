# Healthcare - Dashboard

###Questions(KPIs)

	- What is the total sales since 2019?
	- What is the total profit?
	- What is the total total orders?
	- What are the difference between the previous year orders and current year orders, has it increased or decreased?
	- What is the sales by segment? 
 	- What is the sales by category?
	- What is the total sales ,profit and order quantity by shipment method? 
 	- How are the sales trend for months and quaters doing?
	- By which months the sales goes higher as expected ?
	- What are the top 10 products sold by each year ? 
	- Which regiona has done good at sales?
  	- What is the highest discounts provided?
  	- How many customers are present totally  and state wise?
	- List the top 5 customers
	- Most targetted products by Segments.


## Problem Statement

	Sales dashboard describes the sales perfomance for period of 4 years.It gives complete information  on category and sub category associated with the shipment mode,
	gain understading on the customer purchasing trend ,various customer demographics, customers interest on category. Offers a good idealogy and way to build strategy on how to increase the sales in future.

### Steps followed 

 - Step 1 : Loaded data into Power BI Desktop, dataset as a excel file.
 - Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
 - Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
 - Step 4 : It was observed that couple columns which appeared irrelevant and added no values to the data set were removed.
 - Step 5 : Columns were formatted properly.
 - Step 6 : Created a date table , and created years,month and quaters.
 - Step 7 : Created a seperate measures table to organize the measures effeciently and neatly.
 - Step 8 : Renamed columns accordingly and changed the data type.
 - Step 9 : Sorted the data set based on order date column.
 - Step 10 : From the visualization pane, visuals were added to derive the insights.
 - Step 11 : Since the data contains various aspects displaying the different dynamics hence in order to represent the data different visual were added using the three ellipses in the visualizations pane in report view. 
 - Step 12 : Visual filters (Slicers) were added for four fields named state and city.

	# Snapshot of Dashboard
![Image](https://github.com/user-attachments/assets/20710f93-3e60-4064-b34c-8e723f781746)

![Image](https://github.com/user-attachments/assets/aecce73e-b738-4990-88d1-fa7ae022b9b8)

 - Step 13 : Created a measure table and further sub divisioned to folders namely sales,customers,profit, sales and placed appropriately.
	
	Snap of the measure tables created.

![Image](https://github.com/user-attachments/assets/dd8b958f-bcdf-4ba5-b2e0-e9dc6f42404c)

 - Step 14 : Created date table seperately for maximizing the efficeiecny on time and date calculations. 
	Method : 	Assigned start and enddate as vairable and created the range and with the help of table tool further expanded with month name , quaters, quater number.
		Under the modeling tab created a relationship with the main table orderdate.
	snap of date table  & modeling

![Image](https://github.com/user-attachments/assets/0d5e61ba-b59c-423e-b1e9-589e73a6b1eb)

![Image](https://github.com/user-attachments/assets/1f861aa2-c940-4b00-bada-b59cf6994d66)

![Image](https://github.com/user-attachments/assets/fce63891-fa2c-40e4-ac06-ffe9f82ca8c7)

	 - Step 15 :	From the visualization pane placed new card visuals to display the Sales[by default the sales shown in for the current year]
	Added reference variables to visualize the comparison of the Sales
	Added arrow marks and formatted to show the difference with green and blue.
 # Snapshot 
 
 ![Image](https://github.com/user-attachments/assets/d455266a-8876-4a6f-b105-f317937bf2a5)

	Following dax used 
		TotalSales = SUM(Sales[Sales]) 

		salesDrop = [CySales]-[PySales]

		salesDiff % = DIVIDE([CySales],[PySales],0)*100 
		
		PySales = 
			VAR Latestyear = MAX(DateTable[Dates])
			VAR previousYearSales = CALCULATE(([TotalSales]),
				REMOVEFILTERS(DateTable[Dates]),
					DATESBETWEEN(DateTable[Dates],
						EOMONTH(Latestyear,-24)+1,
						EOMONTH(Latestyear,-12)
					)
				)
	
		RETURN previousYearSales

		CySales = 
		VAR latestYear = MAX(DateTable[Dates])

		VAR CurrentYearSales = CALCULATE(([TotalSales]),
			REMOVEFILTERS(DateTable[Dates]),
				DATESBETWEEN(DateTable[Dates],
					EOMONTH(latestYear,-12)+1,
					EOMONTH(latestYear,0)
		)			)

		RETURN CurrentYearSales
		
		Arrows = 
		 VAR upArrow = UNICHAR(9206) //uparrow
		 VAR downArrow = UNICHAR(9207) //DownArrow

		VAR Arrows1 =  SWITCH(
			    TRUE(),
       				[CySales]>[PySales], upArrow,
      				 [CySales]<[PySales],downArrow,
				" "
			 )

		 RETURN Arrows1

		Formatted Color = 
		SWITCH(
		TRUE(),
		[CySales] > [PySales], "#00CC00",   
		[CySales] < [PySales], "#FF0000", 
		"#000000" 
		)
	
 - Step 16:  From the visualization pane placed new card visuals to display the profit[by default the sales shown in for the current year]
	Added reference variables to visualize the comparison of the profit.
	Added arrow marks and formatted to show the difference with green and blue.

 # Snapshot 
 
![Image](https://github.com/user-attachments/assets/432d8bd0-3364-4e82-92f9-f4996370c904)

	Following dax used 
		Totalprofit = SUM(Sales[Profit]) 

		profitDrop = [Cyprofit]-[Pyprofit]

		profitDiff % = DIVIDE([CyProfit],[Profit],0)*100 
		
		PyProfit = 
			VAR Latestyear = MAX(DateTable[Dates])
			VAR previousYearprofit= CALCULATE(([profit),
				REMOVEFILTERS(DateTable[Dates]),
					DATESBETWEEN(DateTable[Dates],
						EOMONTH(Latestyear,-24)+1,
						EOMONTH(Latestyear,-12)
					)
				)
	
		RETURN previousYearprofit

		Cyprofit= 
		VAR latestYear = MAX(DateTable[Dates])

		VAR CurrentYearProfit = CALCULATE(([profit]),
			REMOVEFILTERS(DateTable[Dates]),
				DATESBETWEEN(DateTable[Dates],
					EOMONTH(latestYear,-12)+1,
					EOMONTH(latestYear,0)
		)			)

		RETURN CurrentYearProfit
		
		Arrows = 
		 VAR upArrow = UNICHAR(9206) //uparrow
		 VAR downArrow = UNICHAR(9207) //DownArrow

		VAR Arrows1 =  SWITCH(
			    TRUE(),
       				[Cyprofit]>[Pyprofit], upArrow,
      				 [Cyprofit]<[Pyprofit],downArrow,
				" "
			 )

		 RETURN Arrows1

		Formatted Color = 
		SWITCH(
		TRUE(),
		[Cyprofit]>[Pyprofit], "#00CC00",   
		[Cyprofit]<[Pyprofit], "#FF0000", 
		"#000000" 
		)
        
 - Step 17 :From the visualization pane placed new card visuals to display the orders[by default the sales shown in for the current year]
	Added reference variables to visualize the comparison of the Orders
	Added arrow marks and formatted to show the difference with green and blue.

 # Snapshot  
 
![Image](https://github.com/user-attachments/assets/69c10db1-0bc0-4bd7-8109-522dcca7a18b)

Following DAX expression was written for the same,

	Totalprofit = SUM(Sales[Order id]) 

		orderdiff = [Cyorders]-[Pyorders]

			
		PyProfit = 
			VAR Latestyear = MAX(DateTable[Dates])
			VAR previousYearprofit= CALCULATE(([Orders]),
				REMOVEFILTERS(DateTable[Dates]),
					DATESBETWEEN(DateTable[Dates],
						EOMONTH(Latestyear,-24)+1,
						EOMONTH(Latestyear,-12)
					)
				)
	
		RETURN previousYearOrders

		Cyprofit= 
		VAR latestYear = MAX(DateTable[totalOrders])

		VAR CurrentYearOrders= CALCULATE(([TotalOrders]),
			REMOVEFILTERS(DateTable[Dates]),
				DATESBETWEEN(DateTable[Dates],
					EOMONTH(latestYear,-12)+1,
					EOMONTH(latestYear,0)
		)			)

		RETURN CurrentYearOrders
		
		Arrows = 
		 VAR upArrow = UNICHAR(9206) //uparrow
		 VAR downArrow = UNICHAR(9207) //DownArrow

		VAR Arrows1 =  SWITCH(
			    TRUE(),
       				[Cyorders]>[Pyorders], upArrow,
      				 [Cyorders]<[Pyorders],downArrow,
				" "
			 )

		 RETURN Arrows1

		Formatted Color = 
		SWITCH(
		TRUE(),
		[Cyorders]>[Pyorders], "#00CC00",   
		[Cyorders]<[Pyorders], "#FF0000", 
		"#000000" 
		)
        
 - Step 18 : A card visual was used to represent count of customers.
 # Snapshot 
 
![Image](https://github.com/user-attachments/assets/9c7d4920-597a-42b2-bcbf-90fa8b035b15)

		Dax Used 
		Total Customers = SUM(sales[customer id])

Bar Chart
        
 - Step 19 : Stacked bar chart to visualize and understand the sales contribution  by ship mode.
	
	 # Snapshot of the chart

![Image](https://github.com/user-attachments/assets/fb338ef9-0445-474c-8af7-045048e4d11e)	
	
 - Step 20 : Stacked bar chart to show the top 10 sold product of all the time.

	 # Snapshot  of the chart

![Image](https://github.com/user-attachments/assets/bb96c350-fdfb-44b5-825d-2dcc544230e2)

 - Step 21 : Clustered column chart to find out the which category are targted or bought  by different segment of customers.

	 # Snapshot  of the chart

![Image](https://github.com/user-attachments/assets/272aeed7-1d85-499a-96c0-6792ca5b4544)

 - Step 22 : Funnel chart to visualize and get the details on top 5 products with max discounts to make a conclusion on providing discounts.

	 # Snapshot  of the chart

![Image](https://github.com/user-attachments/assets/0869ec64-9f19-4e4c-880f-165f261df9ef)


- Step 23 : Clustered bar chart to gain the counts and order made by the customer in each state.

	 # Snapshot  of the chart
  

![Image](https://github.com/user-attachments/assets/8fc9f375-f370-4e3c-8cbc-ba3a5edd2cb9)

- Step 24 : Donut chart to analyse the total sales done by segment wise 

	 # Snapshot  of the chart

![Image](https://github.com/user-attachments/assets/f89cbb27-4be7-417f-afa0-9d81e3b0b3ab)

- Step 25 : Pie chart to analyse the total sales done by segment category

	 # Snapshot  of the chart

![Image](https://github.com/user-attachments/assets/2762e29c-7a1c-4ec0-a724-371e657893a8)

Line Chart

 - Step 26 : line chart tree added to the report design for collecting thorough sales trend by quater and month 
	
	 # Snapshot  of the visual

![Image](https://github.com/user-attachments/assets/bd365b89-2fd2-4855-9a5d-1c954fc82f61)

  
 - Step 27 : Multi Row card added to the for grabbing the details about top 5 and bottom 5 customers by sales ,quantity and profit.
	bookmark was added to see the bottom customers within the same visual.
	
	 # Snapshot  of the visual
top 5
![Image](https://github.com/user-attachments/assets/3d2f1bb2-b443-47f3-ae1c-4a73fc02cf9d)

Bottom 5


 - Step 28 : Created slicers with state and city to analyse all  total sales aspects.
	added bookmarks accordingly.
	
	 # Snapshot  of the filters

![Image](https://github.com/user-attachments/assets/013066bc-2779-446a-b856-8f66e97f2a0b)

![Image](https://github.com/user-attachments/assets/bf5868af-aa24-45bb-af01-8216b65d72a6)

 -Step 29 : Added year ,month and quater slicers to customer page.

	 # Snapshot  of slicers
  
![Image](https://github.com/user-attachments/assets/bf3d84bf-3dda-4a41-86ec-221db7dbbe84)

 - Step 30 : Assigned page navigators to navigate through the pages and designed.
    # Snapshot  of navigators

![Image](https://github.com/user-attachments/assets/640098b0-4905-420d-b6ba-b991dc28843a)


 - Step 30 :  Created three bookmarks namely for opeining the slicer, closing the slicer ,clearing all the applied filters and multi row card switching,
	 alongside Used selection pane to group the visuals accordinlgy to manage the dashboard effieciently.

 # Snapshot  of the bookmarks and selection pane

![Image](https://github.com/user-attachments/assets/b3f44a84-f0bc-4cd0-a6c4-c92948078155)

- Step 31:  Edited the tool tip by giving the similar colors accross the dashboard and font.


# Insights

	###Following inferences can be drawn from the dashboard.

### [1] Current year and previous year sales:
	
	Upon analysis the total sales  from the year 2021 till 2024 there is a good amount increments noted .
	for instance the sales for 2021 is 407k it has hit an increse upto 733k
	
	only for the year 2022 the sales had little fall around 13k

	Note: previous years achieved sales, profit and orders are set as the target for the upsomming years.

### [2] Current year and previous year profit and order :

	Profit is doing well throughout the mentioned period  although there was slip in total slaes in one of the year 
	east has faced small decrease in profit in the 2023

	Orders on the other hand also been great along with the profit.


### [3] Top sold products and Discounts:
	
	mobile phones stand tall in top sold products followed by chairs.However this changes in every year with chair.
	despite of discounts given chairs has sold most. But the discounts for phones are higher than chairs.


### [4] Sales by ship mode and category:

	Each year the standard class shipmode has produced the maximum sales 
	and technology category is max sold category among the other 2.

### [5] Quaterly and monthly sales:

	It is absorbed that sales trends remains same for all the filters applied like year, region, state. The sales has seen a hike during specific months,
	precisely in the month march, november and december where sales trends goes high due to the festivals. 
	

### [6] Customers:
	
	California holds majority of the customers and it is seen that california has the most number of order and virginia stays in the last 
	customer retention is also good meanwhile , there considerable amount of the customer addition is seen throughout.
	

	As far as the analysis is concrerned improvements in strategy must be applied in shipmode and products whihc sold least in numbers
	Either the discounts could be little higher to achieve good sales in other products as well,
	a slight improvement in shipping can be made inorder for the customer to choose the same day delivery ,same day delivery is crucial part in ecommerse.
	Between Q2 and Q3 has continously doing low in business.

