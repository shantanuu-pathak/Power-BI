# SHANTA HOUSING DATA INSIGHTS

## Problem Statement

I recently developed an interactive Power BI report that provides comprehensive insights into Austin, Texas's housing market. This dashboard allows users to explore various facets of the real estate landscape, including:

Property Location & Pricing: Visualize where properties are located and their corresponding costs.
Amenities & Features: Analyze the number of bedrooms, bathrooms, and other key amenities.
Agent Insights: Gain valuable perspectives from listing agent notes.
Key Features:

Summary View: Get a quick overview of the Austin market, including median home prices, living areas, and construction trends.
Interactive Map: Explore property locations and filter by price range to understand market dynamics.
School Analysis: Find top-rated schools near your preferred neighborhoods, including student-teacher ratios and school size.
This tool empowers users to make informed decisions based on data-driven insights. A big shout-out to Sean Chandler for providing the dataset and inspiration for this project!


### Steps followed 

#### Modeling

- Step 1 : The dataset is loaded in the Power BI and the root file is .csv
- Step 2 : After the dataset is loaded, the original file is hidden from the front end using the disbale load option.
- Step 3 : A reference is created for the above original file, and named with the suffix "clean", so that the original file is not affected by the the cleaning transformations.
- Step 4: Following cleaning transformations are carried out:
            
            a. Capatalize Each Word
            b. Replace values containing true and False with Yes and No
- Step 5: Creation of Fact and Dimension tables: 

            A fact and 4 dimension tabels are created. On the dimension tables, transformations such as removing duplicates, adding index column and creating a merge between the fact and dimension tables are performed. Other additional transformations like rounding off values and unpivot columns is also done as required and necessary.
            
#### Evaluation
- Step 1 : Following Dax measures are created:

            Property Count = COUNT(housing_fact[zpid])

            Median Home Price = Median(housing_fact[latestPrice])

            Average House Price = AVERAGE(housing_fact[latestPrice])

            Word Count = COUNT(descrption[zpid])

            Word Find = CALCULATE(MIN(word_summary_pqe[Value]),FILTER(word_summary_pqe,[Word Rank]=SELECTEDVALUE(z_word_rank[Rank])))


- Step 2: Following visuals are created in this Summary insights page and color gradient coding is given to bar charts and column charts.

            Card (new)
            Clustered Bar chart
            Line and Stacked column charts
            Clustered Column chart
            100% Stacked Bar Chart
            Map

Snapshot of Summary Insights Dashboard:

![Image](https://github.com/user-attachments/assets/d563f4ad-7c33-4b8c-a9a9-b3ef88ee269b)

- Step 3: Following visuals are created in the Location page and color gradient coding is given to the Map.
            
            Map
            Slicer
    For the color coding of the map, following measure is created.
            
            Property Color 1 = SWITCH(TRUE(),
                    [Average House Price]>=[Min Parameter Value]&&[Average House Price]<=[Max Parameter Value],"#E0144C",
                    "#cccccc")
Snapshot of Location Dashboard:

![Image](https://github.com/user-attachments/assets/69aa8e9b-e43b-434b-ad39-3894a61ee394)

- Step 4: Following visuals are created in this Schools page and color gradient coding is given to the bar chart, tile slicer and map.

            100% stacked bar chart
            Map with style greyscale
            Card (new)
            Tile Slicer
Snapshot of Schools Dashboard:

![Image](https://github.com/user-attachments/assets/74902e9c-6d42-4630-bce1-8925dc13ea53)

- Step 4: Following visuals are created in this Features page and color gradient coding is given to the clustered column chart and key influencers.

            Clustered column chart
            Matrix
            Key influencers

    Following measure is created for the word rank: 
            
            Word Rank = RANKX(ALLSELECTED('word_summary_pqe'[Value]),[Word Count],,DESC,Dense)

Snapshot of Features Dashboard:

![Image](https://github.com/user-attachments/assets/54d0b10f-c01c-4070-9818-db311d2c20ba)

#### Integration of Buttons, Custom Slicer Panel and Tooltip

Power point is ueed to design the background, logos and images for buttons. The colour scheme for the theme for power bi is also imported.

Buttons and slicer panel is integrated and utilised for the better user navigation.

Snapshot of the slicer panel:

![Image](https://github.com/user-attachments/assets/52ee0c7f-4d54-43fa-a643-13cd67854715)

Tooltip is used on the maps to give users a better understanding of the different geolocational aspects.

Snapshot of the tooltip

![Image](https://github.com/user-attachments/assets/4ce964c4-4148-4af1-b252-5b9925032505)

#### Cover page

A cover page is created to give the user some details on what to expect in the report and, subsequently different tabs are created to let the user jump to different views.

Snapshot of the Cover Page

![Image](https://github.com/user-attachments/assets/417799ac-5169-40ef-b700-40254e3dc4c5)


# Insights

This report contains 4 pages, which is created on Power BI Desktop and a number of inferences can be drawn from it. Following are some of the inferences:

### [1] Number of Properties Available by Home Type

        Single Family properties are available the most with the count of 14,241
           
### [2] Number of Properties Available by Build Year

        2006 recorded the highest number of property count available with the count of 496 properties.
  
### [3] Median Home Price and Average Home Price:

        Median home price recorded was $405,000 and Average Home Price recorded was $512,768.
        The most expensive home seen was $13,500,000 and the least expensive home was $5,500


### [4] % of properties by Features

        Referring the percent of properties by feature 100% stacked bar chart, we can see the distribution of different features with the houses containing them or not.
        For example, it is seen that 45% houses dont have Garage and 55% houses have Garage.
 
### [5] How do different parameters influence the median home price:

Many permutation and combinations can be created to check which features or parameters inflence the median home price to increase or decrease.
        
        For example: It is seen that having more number of appliances directly affects the increase in the median price.

### [5] What influences listing price to (using the key influencers visual):

The key influencers visual gives an apt description of how different parameters repond to the changing influencers.

        For example, it is seen that when the number of bathrooms are more than 4,5 then the average of listing price increases by $1,09M.
