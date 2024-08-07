# Startup Entity Dataset Transformation

This repository contains the Python code and the resulting dataset for transforming a dataset of 10,000 startup-like entities. The transformation process involves filtering and cleaning the data based on specific criteria, using additional datasets for validation and exclusion.

## Introduction

In this project, the aim is to refine and cleanse a comprehensive dataset of startup entities. The task involves multiple stages of data processing, each designed to ensure the final dataset is both relevant and high-quality. By leveraging additional datasets, we validate and exclude specific entities, thereby enhancing the overall utility of the dataset for further analysis.

## Files in the Repository

`transform_dataset.ipynb`: The Python script or Jupyter notebook containing the code for data transformation.
- `resulting_test_task.csv`: The final transformed dataset.

## Datasets Used

1. `test_task.csv`: The core dataset containing the startup-like entities.
2. `db_domains.csv`: Contains the list of domains and UUIDs of entities already in our database.
3. `banned_domains.csv`: Contains the list of top-level domains we don't want in our database.
4. `banned_words.csv`: Contains the list of words that we don't associate with startups.
5. `funding_data.csv`: Contains the dataset with investments for various entities with stages.

## Transformation Steps

1. **Remove Duplicates**:
   - Removed rows with duplicate UUIDs or websites, keeping only one from each duplicate group.

2. **Remove Rows with Missing Values**:
   - Removed rows where any of the following columns are missing: website, description, category, or location.

3. **Filter by Valuation**:
   - Removed rows where the valuation is equal to or exceeds 1 billion dollars.

4. **Exclude Existing Entities**:
   - Removed rows with entities that have UUIDs or websites listed in `db_domains.csv`.

5. **Filter by Banned Domains**:
   - Removed rows where the top-level domains of the websites are listed in `banned_domains.csv`.

6. **Filter by Banned Words**:
   - Removed rows where the descriptions contain any words listed in `banned_words.csv`.

7. **Extract Categories**:
   - The "categories" column contains lists of dictionaries with names of categories for each entity. Created a new column "categories_list" with lists of extracted names of categories.

8. **Extract Locations**:
   - The "location" column contains dictionaries with lists of locations at different scales (city, region, country, and continent). Extracted these and created separate columns for cities, regions, and countries.

9. **Sum Investments**:
   - Summed up the investments from `funding_data.csv` per entity (using UUID) and added a new column in the main dataframe with the total investment for each entity. Entities without investments have blank spaces.

## Usage

To reproduce the transformation process:

1. Ensure you have all the required files (`test_task.csv`, `db_domains.csv`, `banned_domains.csv`, `banned_words.csv`, and `funding_data.csv`) in the same directory as the script/notebook.
2. Run the Python script or Jupyter notebook to perform the transformations.
3. The resulting dataset will be saved as `resulting_dataset.csv`.

## Requirements

- Python 3.x
- pandas
- json

## Code Explanation
The Python script/notebook transform_dataset.py or transform_dataset.ipynb contains detailed comments explaining each step of the transformation process.

## Results
The final transformed dataset is saved as resulting_test_task.csv and includes all the applied transformations according to the criteria specified.

