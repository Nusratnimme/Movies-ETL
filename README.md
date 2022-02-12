# Data pipeline for Amazing Prime


## Overview

Amazing prime, a movie streaming service, would like to have an algorithm that can predict which movies will become popular so that they can buy the streaming rights at a bargain price. To this end, they have organized a hackathon and provided the participants with scrapped wikipedia information on movies and a dataset containing movie ratings. 

### Data Source

- Data Source: wikipedia_movies.json, movies_metadata.csv, ratings.csv

- Data Tools: PostgreSQL13, pgAdmin

- Softwares:Python 3.9.7, Jupyter Notebook 6.4.5


### Purpose

The main task is to create a pipeline to extract available/provided data on movies; clean, transform and merge them into structured datasets; and load them to a SQL database.



## Results

An Extract-Transform-Load (ETL) function was created which took three variables as arguments to read three data files, transformed them as required, and returned three output dataframes. More details are given in below steps.

### Step-1: Read Three Data Files

The data files are as below:

- wiki_movies_df: Wikipedia JSON file transformed to a Pandas DataFrame.

![wiki_movies_df]()

- kaggle_metadata: Kaggle metadata file transformed to a Pandas DataFrame.

![kaggle_metadata]()

- ratings: MovieLens ratings data file transformed to a Pandas DataFrame.

![ratings]()


### Step-2:  Transform the Wikipedia Data 

- A list comprehension was used to filter out TV shows from the raw  movie file.
- With **try_except** block, duplicate IMDB IDs were removed.
- Four cloumns **Box Office**, **Budget**, **release date** and **running time** were cleaned by initiating regular expressions and **Lambda** function.
- By setting three variables equal to the function created in step one, the clean wikipedia movie dataframe was generated.

The clean wiki movies dataframe and columns are listed below.

![clean_wiki_movies]()

![wiki_movies_columns]()


### Step-3: Extract and Transform the Kaggle Data

- Kaggle metadata & wiki movies dataframe were merged to get a new movies dataframe titled **movies_df**.
- Unnecessary columns were dropped from the dataframe.
- With defined function **fill_missing_kaggle_data()**, missing values were filled.
- Columns were renamed.
- A new dataframe titled **movies_with_ratings_df** was created by merging **movies_df** and **ratings**.
- **movies_with_ratings_df** was cleaned, merged with the cleaned ratings data, and empty values in the dataframe were filled with “0”.

![movies_with_ratings]()

![movies_df]()


### Step-4: Load to SQL Database

- Connection to the PostgreSQL database was established to load **movies_df** dataframe and **ratings.csv**
file.

![movies_query]()

![ratings_query]()
