# Overview
I wanted to create a tool that a user can use to look up a specific food item from the FoodData Center database file and output the vitamins and minerals listed in that food. This requires loading in .csv files as dataframes, merging the dataframes on primary/foreign keys, then creating several functions used to grab the relevant data according to a user input.

# Tools Used
**Power Query** - Combining data sheets together so all relevant information is in one place<br>
**Python** - Language used to write the scripts<br>
**Jupyter Notebook** - IDE used <br>
[**FoodData Central**](https://fdc.nal.usda.gov) - Data for food nutritional values<br>
[**FDA Dietary Guidelines**](https://www.fda.gov/food/nutrition-facts-label/daily-value-nutrition-and-supplement-facts-labels) - resource for identifying daily recommended intake values for specific vitamins and minerals<br>
[**FoodData Data Dictionary**](https://fdc.nal.usda.gov/portal-data/external/dataDictionary) - Data dictionary for the many column headers that exist within the data FoodData Central provides


## Data Exploration Phase

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

## Shaping the Data for Querying

- Created dataframes from the .csv files listed above.
- Identified primary and foreign key columns in each dataframe
- Merged all dataframes into one that included the food item and nutrient values/amounts
- Grouped dataframe rows based on the food type, then aggregated the data into multiple sub-dataframes where each food item was it's own dataframe


## Creating Function for Food Item Querying 

- Created function to look up a specific food item using both fuzzywuzzy and regex
  - if there are more than one matches containing the specified food item string, it lists all of the matches with an idex number and food item
  - user then inputs the index number of the food item they are searching for
  - function outputs the user's choice as the food item and displays a dataframe of the nutrients
 

# Future Improvements

- Re-work nutrient volumes so I can only display the nutrients that are above 0 in the final dataframe output
- Add in function that would allow a user to either choose a food item or nutrient
  - searching for a nutrient would return the top 10 foods that have a large amount of that nutrient
- Allow a user to input more than one food, and then output a dataframe with the sum of all nutrients in the foods they input
- Display how much of each nutrient is still required to hit the FDA's daily recommended value.
  - Show negative values when a user has less than the amount
  - Show positive values when a user is over the amount
 
Thank you for stopping by! 


