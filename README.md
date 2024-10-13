# Supply Chain Analysis for years 2015, 2016, 2017 and Januray 2018 
## Data Collection 
A DataSet of Supply Chains used by the company DataCo Global was used for the analysis.
From kaggel https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis 
CSV file.
## Data Cleaning & Preparation 
using power query 
- Handling data types
- handling missing values
- Remove useless columns
## Data Modeling 
- spliting data to six tables are orders, order items , products, departments,customers and dates
- Create Star Schema which the fact table is Order Items and all other columns are the dimentions tables
## DAX Measures 
- Average Inventory Cost per Product =  [Total inventory cost] /COUNT(Products[Category Id])
- Backorders(BO) = DIVIDE(CALCULATE([Total Orders], Orders[Order Status]= "RETURNED") , [Total Orders])
- Defective Inventory Rate = DIVIDE([Returned Items], [Quantity])
- Fill Rate = DIVIDE([ShippedOrders],[Total Orders])
- Inventory Cost to Sales Ratio = [Total inventory cost]/[Total Sales]
- inventory level = [Quantity]-CALCULATE([Quantity], Orders[Order Status]="Completed")
- Lead Time Service Level = DIVIDE(CALCULATE([Total Orders],Orders[Delivery Status]="Shipping on time") ,
                                          ([Total Orders]- CALCULATE(
                                               [Total Orders], Orders[Delivery Status]="Shipping canceled")))
- Loss per orders = CALCULATE(SUM('Order Items'[Order Profit Per Order]), 'Order Items'[Order Profit Per Order]<=0)
- Net Profit = SUM('Order Items'[Order Profit Per Order])
- on time Delivery(OTD) = DIVIDE(
                            CALCULATE(COUNT(Orders[Delivery Status]),Orders[Delivery Status]="Shipping on time")
                                  ,[Total Orders])
- OrderCycleTime(real) = AVERAGE(Orders[Days for shipping (real)])
- OrderCycleTime(schedualed) = AVERAGE(Orders[Days for shipment (scheduled)])
- orders get loss % = CALCULATE([Total Orders], 'Order Items'[Order Profit Per Order]<0) / [Total Orders]
- Profit Margin% = DIVIDE([Net Profit], [Total Sales])
- Profit per orders = CALCULATE(SUM('Order Items'[Order Profit Per Order]) , 'Order Items'[Order Profit Per Order]>0)
- Quantity = SUM('Order Items'[Order Item Quantity])
- Returned Items = CALCULATE([Quantity],Orders[Order Status]="RETURNED")
- Returned Items % = DIVIDE(CALCULATE([Quantity],Orders[Order Status]="RETURNED"), [Quantity])
- Shipped Items = [Quantity]- CALCULATE([Quantity],Orders[Delivery Status]="Shipping canceled")
- ShippedOrders = [Total Orders]- CALCULATE([Total Orders],Orders[Delivery Status]="Shipping canceled")
- Top Selling Product = TOPN(1,VALUES(Products[Category Name]),[Quantity])
- Total inventory cost = SUM(Products[Inventory Cost Per Product])
- Total Orders = DISTINCTCOUNT('Order Items'[Order Id])
- Total Sales = SUM('Order Items'[Sales])
- Inventory Cost Per Product = Products[Quantity]*Products[Inventory Cost Per Unit]
## Data Visualization 
- Create report consist of siven pages are Home, Order Fulfillment, Shipping , Inventory,  Revenue , Units sold in each department and Overview 
- use charts, cards,tables, filters and simple colors to visualize insights and KPIs
## Insights & KPIs 
- Order Fulfillment page 
     - Fill Rate 94.91%
     - 32% of total orders are completed and 2.5% canceled 
     - The markets Pacific Asia and LATAM have the highest value in orders number
     - The products category Cleats, Women`s Apperal and Indoor/Outdoor Games have the highest Orders and units sold
- Shipping
     - On Time Delevery Rate 17.7%
     -  Average of order cycle time real   4 
     -  Average of order cycle time schedual 3
     -  56% of total orders are late delevery
     -  The highest shipping mode is Standard Class
     -  some of country all the orders deleverd late
     -  Not all country use all Shipping modes
- Inventory
     - The highest 3 products in terms of inventory level and average inventory cost per product are
    products Perfect Fitness Perfect Rip Deck, Nike Men's Free 5.0+ Running Shoe and O'Brien Men's Neoprene Life Vest
     - The highest 3 products in terms of inventory cost to sales ratio are Toys, CDs of rock and Team Golf Pittsburgh Steelers Putter Grip
 - Revenue
       - Total Sales 35.5M
       - Orders Get Loss 37%
       - Net Profit 3.8%
       - Profit Margin 11%
       - in year 2015 : in first 6 months orders volume have loss more than orders volume got profit and, the reverse in the last 6 months
      cause this the highest net profit  Net profit in the last six months of the year , we can track the values for the other years through the dashboard...
- Department
        - the highest departments in terms of quantity of units sold are Apperal,Golf, Outdoors, Fanshop and footware
        - the Fan Shop Department is the highest department get profit and sold units
        - Each department produce set of products and we can track sold units and sales for each department in any year through the report 










 


