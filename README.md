# DATA 301 Lab 6 - Visualization with Tableau

## Instructions

For this lab, the instructions are in this README file.
There is an accompanying video as part of the Week 10 Videos

This lab uses Tableau to visualize, analyze, and explore data sets. **This lab should be done individually.**

## Important links

- [Seminar outline](./data/seminar_outline.md)
- [Google slides for presentation](https://docs.google.com/presentation/d/1rTyl5_-MAjgimppsRoRSwzDqFY7bZsA4xO-Q4H6omZw/edit?ts=5ecc2dd0#slide=id.p1)
- [Follow along building a dashboard](./tableau_workshop.md)

## Objectives

1.  Explore the capabilities of Tableau for importing, formatting, and visualizing data sets.
1.  Visualize data from an Excel spreadsheet including using bar charts, line charts, maps, and trend lines.
1.  Apply filtering, sorting, and aggregation in visualizations.
1.  Create a dashboard consisting of multiple related visualizations.

## Installing Tableau

[Download Tableau](https://www.tableau.com/tft/activation).

- Download the latest version of Tableau Desktop (you do not need Tableau Prep Builder).
- Click on the link above and select “Download Tableau Desktop”. On the form, enter your school email address for Business E-mail and enter the name of your school for Organization.
- Activate with your product key: `TCHO-57EF-BE10-52AA-AE8F`
- If you already have a copy of Tableau Desktop installed: update your license in the application: Help menu → Manage Product Keys

## A. Load in the `street_trees` Data.

- 4 marks.

### A1. Load the data (2 marks)

We have provided you with a street_trees.csv file located in the data folder. 

This csv file was obtained from [The City of Vancouver's Open Data Portal](https://opendata.vancouver.ca/explore/dataset/street-trees/information/?disjunctive.species_name&disjunctive.common_name&disjunctive.height_range_id)
with minimal data wrangling done by the R package [DatateachR](https://github.com/UBC-MDS/datateachr).

#### Instructions

1. On the left-hand side in the blue bar, you'll see a "Connect" heading. This is where you can connect Tableau to your data.      
1. Since we are using a `.csv` file we are going to click on "**More...**" under the "**To a File**" subheading.           
 _💡You can connect to many different things such as Microsoft SQL, PostgresSQL, Google Sheets, MongoDB BI Connector, etc. This is all accessible in "**More...**" under the sub-heading "**To a Server**"._
1. Locate the data and click "**Open**". This should connect your data and you  should see a table. (You may need to click the "**Update Now**" button at the bottom)
1. You can choose to rename your data source by clicking the title at the top.
1. To start creating plots you can click "**Sheet 1**" at the bottom left of the window. 


### A2. Set the data types for the columns (2 marks)

Tableau automatically assigns variable types to your columns, however, sometimes it doesn't guess correctly.


#### Instructions 

1. We need to change the last 3 columns in our data `date_planted`, `latitude` and `longitude`. 
1. Scroll to the right and click on the icon (ABC) to the left of `date_planted` and convert it to **Date**. 
1. Next, convert `longitude` and `Latitude` to a **Number (decimal)** and the under the **Geographic Role** we can assign it to  **Longitude** and **Latitude** respectively.     
    - _💡If we do not convert these columns to decimals first, Tableau will not give you the **Latitude** and **Longitude** options under **Geographic Role**_ 

## B. Bar Charts in Tableau.

- 4 marks.

### B1. Tree count (2 marks)

Make a new worksheet called `B1` by going to the menu bar under "**Worksheet**" and clicking "**New Worksheet**" (Or Command+T on a Mac, Ctrl+T on Windows). 

We are going to make a bar chart for the number of trees of each species.

#### Output

![](images/Trees_by_name.png)


#### Instructions 
1. Since we are interested in the species name, we are going to drag from the left-hand side under the heading "**Tables**" the column named `Species Name` to the "**Column**" toolbar. 
1. We are interested in the count of the trees for each Species, so I like to use the index to count the rows but you can use multiple different columns here. Drag the `tree_id` to the "**Rows**" toolbar.
1. We need to convert this variable to a "**Measure**" specifically a "**Count**". We can do this by right-clicking on it. 
1. Voila! A bar chart! 
1. Let's change the colour. Go to the mark card and select a new colour. 
1. Let' edit our y-axis label. Right-click on the axis and click "**Edit Axis...**" Under "**Axis**", you can edit your axis "**Title**".
1. You can edit the title in two ways by editing the sheet name or by editing the title. I prefer to edit the sheet name by double-clicking the sheet at the bottom. 
1. You can sort the bars by clicking the icon beside the axis title. Go ahead and sort the data in a decending order.  
1. Let's convert it to a verticle bar chart. On the toolbar right above "**Columns**" you'll see a "Swap rows and columns" icon. This transposes your graph so the x and y-axes are flipped (remember keep your text description values on the y-axis so you don't have to turn your head to read them.

### B2. Tree diameter (2 marks)

Create a new sheet called `B2` and plot the average `diameter` of the tree trunks of each `genus_name` & 'species name' type.

The columns for this plot are: genus_name as well as species name (you can have multiple feilds for the rows or columns!)

The rows should be diameter. he 

#### Output

![](images/Diameter.png)

#### Instructions 

1. Drag from the left-hand side under the heading "**Tables**" the column named `genus_type` to the "**Column**" toolbar. Then drag 'species name' as well.
2. We want the mean diameter for each genus so we can drag `diameter` to the "**Rows**" toolbar.
3. This is where things differ. We right click the `diameter`  and transform the "**Measure**" to "**Average**". 
4. Instead of using a bar chart, try a dot plot would be more ideal. We can convert it by clicking the dropdown menu under the "**Marks**" card. Selecting "**Circle**" or "**Shape**" will instantly convert it.     

_💡You can add your own shape icons by adding a folder to your "My Tableau Repository" folder under "Shapes"_ 

## C. Time Series.

- 4 marks.

### C1. Trees planted by Year (2 marks)

Create a new sheet called `C1` and plot the number of trees planted and the date they were planted.
#### Output

![](images/Trees_planted_per_year.png)

#### Instructions 
1. Drag the `date_planted` variable to the "**Columns**" toolbar and again the `tree_id` to "**Rows**". We are again interested in the amount of trees planted at selected dates so once again we want to transform this to a "**Count**" type "**Measure**".  
1. Since `date_planted' is a continuous variable, it's a good idea to right-click and transform this into a **Continuous** Dimension. 
1. This automatically generates the number of trees planted at each year (but there are null values!)
1. Combining scatterplot onto our line graph by adding an identical `tree_id` to rows and converting it to a counting measurement again. At first, we should get 2 graphs on top of each other. We can right-click one of them and select "**Dual Axis**".
This will superimpose one on another with a left and a right axis title. We can hide the one on the right by right-clicking the axis and unticking the "**Show Header**" option. 
1. To change the colour of the line and the points, we need to make sure we change the colour of both measures by selecting the "**All**" tab under the "**Marks**" card on the right.      
1. Don't forget to give it a title and edit the y-axis label as we did earlier.

### C2. Trees planted by Month (2 marks)

Create a new sheet called `C2` that has the count of trees planted by month over the years. In other words, across all years, January trees should be reported together.

#### Output

![](images/Trees_planted_by_month.png)

## D. Maps (Choropleths)

- 2 marks.

This, and creating dashboards, is where Tableau really shines!

### D1. Map of the trees planted (2 marks)

Plot the location of the planted trees on a map of Vancouver.

#### Output

![](images/Map.png)

### Instructions 
1. Drag `Longitude` to the "**Columns**" toolbar.
2. Drag `Latitude` to the  "**Rows**" toolbar.
3. You have essentially made your map but let's tidy it up. 
4. Decrease the size of your markers by clicking the "**Size**" icon under the "**Marks**" card. 
5. Click "**Map**" on the top toolbar and select "**Map Layers...**". This gives you the ability to customize the appearance of your map. Change the style to streets.         
6. Add a title as before and change the color of the plot to red. 
Now you've got a functioning map plot in < 5 mins. 

## E. Putting it all Together in a Dashboard

- 7 marks.

You can take an arbitrary number of plots in sheets and lay them out in a "Dashboard". This part of the lab guides you on how to do this.

### E1. Making a Dashboard (5 marks)

1. Create a new dashboard by clicking "**Dashboard**" in the top menu bar and selecting "**New Dashboard**"
2. Before you do anything else, under the "**Size**" heading, click the triangle beside "Desktop Browser (1000x800)". Change "**Fixed Size**" to "**Automatic**". This will now make sure your dashboard adjusts to all monitor sizes. 
3. Let drag our sheets in using Tiled objects. Under "**Sheets**" on the left-hand side, drag and drop the sheets you want to include in your dashboard. 

### Sample Output

Here is a sample dashboard, you do not have to create one exactly like this one, but you should include at least 2 filters, and at least 4 plot elements.

![](images/Dashboard.png)

### Filters (2 marks)

1. Decide which filters you want for each plot. 
2. Go to the sheet my navigating on the bottom and selected the worksheet of interest.
3. Under "**Tables**" Drag the column you wish to filter.
4. Repeat this step for each of your worksheets. (OR wait and follow the next section) 
5. To obtain filters, on the side of the dashboard you will see a ▼ icon. Click this  and under "**Filter**" Select one of the column names. 
6. We can edit the filter style by clicking the "**More Options**" ▼ icon and changing the style. 
    - If it's filtering categorical data there are options like "**Single value (list)**", "**Single value (dropdown)**", "**Single value (slider)**", "**Multiple value (dropdown)**", etc. 
7. You can "**Customize**" The filter styles to include certain features as well. 

#### One Filter For Multiple Graphs
- If you want to use a single filter for multiple plots, you can do so using the "**Apply to Worksheet**" option. 
- This gives you the ability to select which sheet to also be filtered on this column or you can apply to "**All Using This Data Source**". 

#### Using a Graph as a Filter

If you want to use a highlight something on a plot and have it act as a filter on other sheets in the dashboard, this can be done with a single mouse click. 
- Simply find the funnel icon on the side. When you hover over it, it should say "**Use Sheet as Filter**". 

## Submission

Include the Tableau Workbook file (.twb), and a screenshot of your final dashboard called "final_dashboard.png" in this GitHub repository and you're done!

## Attribution

This seminar was conducted in collaboration with [Hayley Boyce](https://www.hayleyfboyce.com). 
Hayley created the first draft of this workshop, and it was adapted in the summer of 2020 for DATA 301 and DATA 532.
