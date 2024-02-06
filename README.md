# Overview
I am creating a tool that allows a user to input what food(s) they are currently eating in a single meal. It will then scan a file containing all relevant information - nutrients (*vitamins and minerals*), calories, macros - and output those values based on the amount of food you ate. It will also show you, in a percentage, how close you are to fulfilling the recommended amount of nutrients you should be ingesting per day. <br><br>***Note: Calories and Macros will be part of a later phase as this information is either not completely available with the data provided by FoodDataCentral or will require additional calculations to be built into the project.***

For the first phase of my project, I will only be looking to write code that cleans the data and prepares it for the lookup functions. My first goal will be to successfully write code that allows users to simply look up nutrient values in each food product. A user will then be able to compare what they are seeing to what the recommended amount of nutrients are for adults. The FDA does not have separate calculations for gender or biological sex, so all values listed here are the recommended values based on FDA guidelines: [FDA.gov](https://www.fda.gov/food/nutrition-facts-label/daily-value-nutrition-and-supplement-facts-labels). 

Due to complexities with conversion factors, (methodology in conversion factors can be found here - [FICRCD Methodology and User Guide](https://www.ars.usda.gov/ARSUserFiles/80400530/pdf/ficrcd/FICRCD%20Methodology%20and%20User%20Guide.pdf), I will attempt to break up this project into phases - **Data Exploration** being a preliminary phase one. 



**Steps for looking up food:** 
  1. Input the food product(s) included in your meal.
  2. Input the total quantity in grams of the food included in your meal.
  3. Input the state your food is in (dried, raw, cooked.) - I will attempt to include this functionality, however I am unsure whether or not this can be achieved with the data provided. More analysis of the data will be required. 

I plan on displaying three methods for extracting and cleaning the data. [FoodDataCentral](https://fdc.nal.usda.gov/) is a site which provides users with the ability to either download their food data directly in .csv format, or provides an API for users to use for pulling food data. I will attempt to pull and clean the data using three different ways: 
  1. Download the .csv file directly from FoodDataCentral and use Power Query to join tables. The resulting tables will then be queried using python.
  2. Download the .csv file directly from FoodDataCentral and use Python for all ETL processes.
  3. Use the API from FoodDataCentral and use Python to call the API service for any foods users input into the program.
  4. (Possibly) Install a SQL server onto my machine and load the data needed into SQL. Use SQL to create needed tables. Use Python to then pull tables from SQL into dataframes for use.  - ***This is a possible outcome depending on how difficult it is for me to achieve the first three steps***

# Tools Used
**Power Query** - Combining data sheets together so all relevant information is in one place<br>
**Python** - Language used to write the scripts<br>
**Jupyter Notebook** - IDE used <br>
[**FoodData Central**](https://fdc.nal.usda.gov) - Data for food nutritional values<br>
[**FDA Dietary Guidelines**](https://www.fda.gov/food/nutrition-facts-label/daily-value-nutrition-and-supplement-facts-labels) - resource for identifying daily recommended intake values for specific vitamins and minerals<br>
[**FoodData Data Dictionary**](https://fdc.nal.usda.gov/portal-data/external/dataDictionary) - Data dictionary for the many column headers that exist within the data FoodData Central provides


## Preliminary Phase - Data Exploration

The data consists of 23 .csv files as shown below: 
![Food Data Files](https://github.com/dylanvowell/FoodAnalysisTool/assets/95980792/1ea9048b-3378-4630-be39-bb2af3b55dd7)

Each worksheet has a specific role in identifying the food, nutritional information, portions, etc. <br>
<br>
The first challenge is to identify what each column header means - "id" shows up in multiple sheets, but has different id types (4 digit, 5 digit, and 6 digit number codes) depending on what sheet is being viewed. I will need to indentify the primary/foriegn keys present in the following sheets required for the initial functions of this project: <br>
<br>
**food.csv** - Data indicating the fdc_id number associated with each type of food - e.g "HUMMAS, SABRA CLASSIC".
<br>
**food_nutrient.csv** - Data indicating the type of nutrient (nutrient_id), fdc_id (same id from food.csv indicating the type of food).
<br>
**food_portion.csv** - Data indicating the weight in grams of the food used in calculating nutrient values. Data also includes the fdc_id found in the previously listed files. 
<br>
**nutrient.csv** - Data indicating the nutrients present in food items.
<br>
**measure_unit.csv** - Data indicating measurments alongside their respective measurement codes.

## Additional Data That May Be Used

There are several other files that may include relevant information for my purposes, but further research into their contents is needed. They are listed below: 
<br> 
<br>
**food_attribute.csv** - Data indicating Ontology information including name, ID, name for FDC item, ID for FDC item, NCBI Taxon. This would provide users with a way to look up official ontology for foods used by the USDA and FDA. 
<br>
*Example values shown in below screenshot for HUMMUS, commercial:**
<br>
![Information for HUMMUS, commercial](https://github.com/dylanvowell/FoodAnalysisTool/assets/95980792/1404d231-9b6b-45fa-9359-f633b9472f5e)
<br>
**food_calorie_conversion_factor.csv** - Data showing Macro values, using a food_nutrient_conversion_factor_id.
<br>
**food_nutrient_conversion_factor.csv** - Data listing the food_nutrient_conversion_factor_id and the fdc_id, which allows me to find macro data for each food item listed in food.csv. 





