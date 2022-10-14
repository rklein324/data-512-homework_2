# The Project
The goal of this project is to explore bias in Wikipedia articles on political figures from different countries. 

# License and Sources
[Terms of Use for WikiMedia API](https://foundation.wikimedia.org/wiki/Terms_of_Use/en)  
[Documentation for page info request](https://www.mediawiki.org/wiki/API:Info)  
[Documentation for ORES](https://www.mediawiki.org/wiki/ORES)  
[Page info request example](https://drive.google.com/file/d/1Z8DqXpHmNUJ3RD7e-OOwx2WYJPIYjUPp/view?usp=sharing)  
[ORES request example](https://drive.google.com/file/d/1rZdBrtCe9XO4IkDWqm0A2RA-HfZCsqHh/view?usp=sharing)  
[Politicians article list](https://docs.google.com/spreadsheets/u/0/d/1Y4vSTYENgNE5KltqKZqnRQQBQZN5c8uKbSM4QTt8QGg/edit)  
[Population list](https://docs.google.com/spreadsheets/u/0/d/1POuZDfA1sRooBq9e1RNukxyzHZZ-nQ2r6H5NcXhsMPU/edit)  
[Source for population list](https://www.prb.org/international/indicator/population/table)

# Data Files
## Raw Data
### politicians_by_country.csv
This is the file with all the Wikipedia article titles used in this analysis.
  
| Column | Description |
| ------ | ------------- |
| name   | name of the article/politician  |
| url    | url to Wikipedia article (not used in this repo)  |
| country    | country the politician is from  |

### population_by_country.csv
This is the file with the population of countries and regions used in this analysis.

| Column | Description |
| ------ | ------------- |
| Geography  | name of the country/region – regions are in all caps  |
| Population (millions)  | population of the country/region in millions  |

## Processed Data
### wp_politicians_by_country.csv
This is the file with the predicted article quality score as well as population for each article used in this analysis

| Column  | Description |
| ------- | ------------- |
| country   | country the politician is from  |
| region   | region the country is in (lowest in hierarchy from population_by_country.csv  |
| Population (millions)  | population of the country/region in millions  |
| name | name of the article/politician  |
| revision_id | latest revision ID of the article at the time the analysis was run  |
| article_quality | predicted quality score from the ORES API for the article  |

### wp_countries-no_match.txt
This file is the list of countries that do not appear in *both* politicians_by_country.csv and population_by_country.csv

# Scripts
Only one script was created for this analysis, and it is in the src folder. The code is split into the following categories:
- Set Up
- Functions
- Retrieve and Process Data
- Analysis

If you do not want to retrieve the data yourself, you can just run the ‘Import Packages’ cell, the last function (‘Function to take a dataset and population to return article coverage’), as well as uncomment and run the first cell in the ‘Analysis’ section.

# Research Implications
The top and bottom 10 countries for total articles per capita has very little overlap with high quality articles per capita. There is only one country (Andorra) in the top 10 and only two countries (India and Vietnam) in the bottom 10. The articles per captia was more interesting by region. For example, all European regions are in top 6 for both total articles and high quality articles. Both Central America and Southeast Asia gain 5 spots when going from total to high quality articles. Eastern Africa and South America drop 3 spots, and Oceana and Middle Africa drop 2 spots.

*What (potential) sources of bias did you discover in the course of your data processing and analysis?*  
There seems to be a bias towards wealthier countries/regions. I looked up some [data](https://www.prb.org/international/indicator/gross-national-income/table#) from the same source as the population, and saw that the top 9 regions included all the wealthiest ones. In addition, there were a number of countries that were not included, such as Ireland and New Zealand.

*What might your results suggest about (English) Wikipedia as a data source?*  
Articles are only included on Wikipedia if they are considered ‘notable’. Notable may include being covered in the news, but the news has its own bias towards covering politics in wealthier countries. Thus, this bias is transferred to Wikipedia. Because Wikipedia is staffed by volunteers, English Wikipedia volunteers may be less familiar with or care less about politicians from poorer countries.

*Can you think of a realistic data science research situation where using these data (to train a model, perform a hypothesis-driven research, or make business decisions) might create biased or misleading results, due to the inherent gaps and limitations of the data?*  
One example of this would be if you tried to model peoples’ interest in politics by region. If this was done by collecting viewcounts for all of the politician articles and divided by the number of articles, this would not include any interest people may have in politicians or regions that do *not* have articles. This could almost be an example of survivorship bias by only including articles that made it past the ‘notable’ reqirements.

# Additional Notes
Some politicians are listed as just being ‘Korean’. For those politicians, I change the country to ‘Korea’ and add a row in the population dataset for ‘Korea’ with the population being the sum of North and South Korea. This is done in the script, and the input files themselves are not changed.
