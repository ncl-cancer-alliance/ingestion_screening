# NCL Cancer Alliance Ingestion EMIS

This is an ingestion pipeline for data sourced from the NHS Futures [Cancer Screening Coverage & Uptake dashboard](https://future.nhs.uk/vaccsandscreening/view?objectID=42174992)

Refer to the generic project template for standard best practice: [Link](https://github.com/ncl-cancer-alliance/nclca_template/blob/main/README.md)

## Scripting Guidance

Please refer to the Internal Scripting Guide documentation for instructions on setting up coding projects including virtual environments (venv).

The Internal Scripting Guide is available here: [Internal Scripting Guide](https://nhs.sharepoint.com/:w:/r/sites/msteams_38dd8f/Shared%20Documents/Document%20Library/Documents/Git%20Integration/Internal%20Scripting%20Guide.docx?d=wc124f806fcd8401b8d8e051ce9daab87&csf=1&web=1&e=qt05xI)

## Usage

### Pulling the source data
A visual SOP document is available here: [NHS Futures Screening Data SOP](https://nhs.sharepoint.com/:w:/r/sites/msteams_38dd8f/Shared%20Documents/Document%20Library/In-production%20dashboards/NCL/Cancer%20Primary%20Care%20Dashboard/Documents/NHS%20Futures%20Screening%20Data%20Extraction%20SOP.docx?d=w396fced8b00d4afa8ad72ddae75e58ad&csf=1&web=1&e=skwiOB).

### First Time Setup

Set up the project as usual as depicted in the [Internal Scripting Guide](https://nhs.sharepoint.com/:w:/r/sites/msteams_38dd8f/Shared%20Documents/Document%20Library/Documents/Git%20Integration/Internal%20Scripting%20Guide.docx?d=wc124f806fcd8401b8d8e051ce9daab87&csf=1&web=1&e=qt05xI).

Create a .env file using the sample.env file as a reference. Some fields are left blank and can be filled in using the Account Details section on the Snowflake website. The DATABASE and SCHEMA fields refer to the destination location where both file staging and the destination tables will appear.

Before running the code, any named schema and database in the .env file must be created in snowflake first.

### Regular Use

* From the downloaded csv files from NHS Futures, move the corresponding csv files to the correct data directories:
  * CSV files containing NCL Practice data -> data/Screening/Local
  * CSV files containing Regional data -> data/Screening/National

When the src/main.py code is executed, all data files found in the corresponding data_dir locations as specified in the config.toml will be ingested into Snowflake. By default this should be to DATA_LAKE.CANCER__SCREENING.

The ingested data will append to the existing table and have a _TIMESTAMP column appended to the destination table for logging and debugging purposes.

### Custom Processing
Because of the format the NHSE Tablau site exports CSV files the following settings are required for each dataset in the config.toml file (by default, these will already be there):

    #Optional fields  
    field_delimiter = '\t'  
    encoding = "UTF-16LE"

## Changelog

### [1.0.0] - 2025-07-29
- Initial pipeline for Screening data ingestion

## Licence
This repository is dual licensed under the [Open Government v3]([https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/) & MIT. All code can outputs are subject to Crown Copyright.

## Contact
Jake Kealey - jake.kealey@nhs.net