# Movies-ETL

## Background Information
AmazingPrime video is a platform for streaming videos and TV shows. The company wants to develop an algorithm to predict which low-budget movies being released will become popular, so they can effectively buy the streaming rights. AmazingPrime decided to sponsor a hackathon providing a clean dataset of movie data and asking participants to make these predictions. 

## Purpose 
We are tasked with creating the datasets for this hackathon. We will create an automated ETL (Extract, Transform, and Load) pipeline to ensure that the data follows a consistent and robust data structure. 

## ETL Overview

### Extract 
The data was extracted from two sources:
- **Scarped Wikipedia movie data** stored as a JSON file. The file contains movie information between 1990 and 2018 such as but not limited to, movie titles and languages, budget and box office returns, cast and crew, production and distribution. The dataset has 7,311 records. 
- **Kaggle MovieLens ratings dataset** with over 20 million reviews and **Kaggle metadata** containing details about the movies for which the reviews were given. Both datasets come in CSV formats.
- The raw data could not be uploaded to this repository due to its large size. 


### Transform
Cleaning of data was done using Pandas and Python RegEx module. Wikipedia does not have strict data presentation standards, so a lot of cleaning needs to be done. Kaggle metadata and rating data also require cleaning and transformations. We need to organize and merge data in a structured format before we can send it to SQL. 

### Load
Using PostgreSQL and pgAdmin, the final merged datasets need to be sent to SQL. 

## Results
The initial work on the datasets was done in [this one file](https://github.com/Aigerim-Zh/Movies-ETL/blob/main/Exploratory%20data%20analysis.ipynb). As a part of the project, the code was refactored to the following deliverables:

[Deliverable 1](https://github.com/Aigerim-Zh/Movies-ETL/blob/main/ETL_Deliverable1_function_test.ipynb). 
- Writing a function ```extract_transform_load``` that reads in the three data files and creates three separate DataFrames.  
    - Extracting data in JSON and CSV formats.
    - CSV files are already in flat-file formats, we will put them into Pandas DataFrames directly.
    - Load the JSON file and read it in as a list of dictionaries in Pandas and then converted it into a Pandas DataFrame. 

[Deliverable 2](https://github.com/Aigerim-Zh/Movies-ETL/blob/main/ETL_Deliverable2_clean_wiki_movies.ipynb)
- Extracting and transforming the Wikipedia data to merge it with the Kaggle metadata. 
- Creating function ```clean_movie``` that combines alternative movie titles into one column ```alt_titles```.
- Creating a sub-function ```change_column_name``` to put columns in a consistent pattern. 
- In the ```extract_transform_load``` function, the Wikipedia movie data is transformed using:
    - Python list comprehensions
    - Python RegEx module for regular expressions
    - Lambda functions
- Dropping redundant columns.
- Dropping duplicates.
- Filtering out TV shows. 

[Deliverable 3](https://github.com/Aigerim-Zh/Movies-ETL/blob/main/ETL_Deliverable3_clean_kaggle_data.ipynb)
- Extracting and transforming the Kaggle data into separate DataFrames. The function ```extract_transform_load``` has additional tasks for cleaning and transforming the Kaggle data such as:
- Fixing columns to the correct data types.
- Dropping no-value-added columns.
- Filling missing values.
- Merging with the Wikipedia movies DataFrame into a ```movies_df``` DataFrame.
- Finally, merging the MovieLens rating data DataFrame with the ```movies_df``` to create ```movies_with_ratings_df```. 

[Deliverable 4](https://github.com/Aigerim-Zh/Movies-ETL/blob/main/ETL_Deliverable4_create_database.ipynb) 
- Creating the Movie Database.  
- The function ```extract_transform_load``` performs the last step of connecting to the SQL database using ```to_sql``` method of the ```sqlalchemy``` library.
- The final code executes the whole ETL pipeline.