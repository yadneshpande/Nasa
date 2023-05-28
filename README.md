# Data Ingestion Pipeline Template

This repository consists of boilerplate folder structure to write and organize your scripts for a data ingestion pipeline

## Folder Structure
The tree diagram below represents a general file structure

```
|--- data_source_name                      
     |--- deploy                            # pipeline orchestration and configuration of DAGs
     |    |---dev              
     |    |---prod
     |--- src
          |--- dependencies
          |    |--- cleaning
          |    |    |--- __init__.py
          |    |    |--- cleaner.py         ## Cleaning script here
          |    |--- geocoding
          |    |    |--- __init__.py
          |    |    |--- geocoder.py        ## Geocoding script here
          |    |--- scraping                # This folder contains all data harvesting scipts
          |    |    |--- __init__.py
          |    |    |--- scraper.py         ## Harvesting script here
          |    |--- standardization
          |    |    |--- __init__.py
          |    |    |--- standardizer.py    ## Standardization script here
          |    |--- utils                   # Utility and helper scipts to be placed here
          |         |--- __init__.py
          |--- .dockerignore
          |--- Dockerfile
          |--- client.py                    # Master script that connects all the above blocks
          |--- requirements.txt
```

## Different Blocks of ETL pipeline
1. Scraping/Data Harvesting
    - Contains all the scripts that extracts metadata and raw data to be processed further from database, websites, webservices, APIs, etc.
2. Cleaning
    - Treatment missing fields and values
    - Treatment of duplicate entries
    - Convert country codes to `ISO 3166-1 alpha3` i.e. 3 letter format
    - Identify region name and region code using the country code
3. Geocoding
    - Based upon location information available in the data
        - Location label
        - Geo-spatial coordinates
    - Missing field can be found either by using geocoding or reverse geocoding with max precision available
4. Standardization
    - Fields to be strictly in **lower snake casing**
    - Taking care of data types and consistency of fields
    - Standardize fields like `sector`, `subsector`, `domain`, `subdomain`
    - Renaming of field names as per required standards
    - Manipulation of certain fields and values to meet up the global standards for presentation, analytics and business use of data
    - Refer to the [Global Field Standards](https://docs.google.com/spreadsheets/d/1Zyn0qLI1JdZD-3EQdvpi7twzUUy3vExg80SL3CK6sWI/edit#gid=0) spreadsheet for the standards to be followed

### Note
> Depending upon what fields are already available in the data `GEOCODING` step may or may not be required.

> It is recommended that the resultant data after each and every step is stored and backed up for recovery purpose.

> Apart from the primary fields listed down in [Global Field Standards](https://docs.google.com/spreadsheets/d/1Zyn0qLI1JdZD-3EQdvpi7twzUUy3vExg80SL3CK6sWI/edit#gid=0) spreadsheet, there are several other secondary fields that are to be scraped; given by the data provider for every document that holds significant business importance.

## Submission and Evaluation
- For assignment submission guidelines and evaluation criteria refer to the [WIKI](https://github.com/Taiyo-ai/ts-mesh-pipeline/wiki) documentation

---
Copyright © 2021 Taiyō.ai Inc.
