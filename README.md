Migrating Medical Data to MongoDB
This project demonstrates a complete ETL (Extract, Transform, Load) pipeline for migrating medical data from CSV files into a MongoDB database. It consists of:

Docker Compose orchestration for:

Jupyter Notebook (for running and editing the ETL code)

MongoDB (target database)

Mongo-Express (web UI for browsing MongoDB collections)

Jupyter Notebook (Python) that implements:

Automatic detection of new CSV files in the ./Data folder

Data validation and cleaning (checking expected columns, parsing dates, handling nulls)

Field transformation/normalization (renaming columns for MongoDB)

Bulk insertion into MongoDB

Archiving processed CSVs into ./Data/archive

Logging each major step of the pipeline

Docker Compose file (docker-compose.yml) to spin up:

A JupyterLab container (exposing port 9988)

A MongoDB container (exposing port 27017)

A Mongo-Express container (exposing port 8081)

Table of Contents
Prerequisites

Project Structure

Environment Variables

Starting with Docker Compose

ETL Pipeline Overview (Notebook)

Sample MongoDB Aggregations

Accessing Mongo-Express UI

Connecting via MongoDB Compass

License

Prerequisites
Docker (20.x or later)

Docker Compose (1.29.x or later)

(Optional) MongoDB Compass or another MongoDB client for direct connections

Project Structure
graphql
Copier
Modifier
Migrating-Medical-Data-to-MongoDB/
├── Data/
│   ├── healthcare_dataset-20250506.csv      # Example medical data CSV
│   └── archive/                             # Processed CSVs will be moved here
├── notebooks/
│   └── ETL_Script.ipynb                     # Jupyter Notebook with the ETL pipeline
├── docker-compose.yml                       # Orchestrates Jupyter, MongoDB, and Mongo-Express
├── .gitignore
└── README.md                                # (You are here)
Data/

Contains raw CSV files to be processed.

Each CSV is moved to Data/archive/ after processing to avoid reprocessing.

notebooks/ETL_Script.ipynb

Implements the full ETL pipeline in Python:

Scans Data/ for new CSVs

Validates and cleans each file (column checks, date parsing, null handling)

Transforms/renames fields for MongoDB

Inserts records in bulk into MongoDB

Archives each processed CSV

Logs every step

docker-compose.yml

Defines three services:

notebook: uses the jupyter/scipy-notebook image, exposes port 9988, mounts ./notebooks to /home/jovyan/work and ./Data to /data.

mongo: uses mongo:latest, exposes port 27017, mounts ./Data to /data (for reading/archiving) and attaches a named volume mongo_data for persistence.

mongo-express: uses mongo-express:latest, exposes port 8081 to browse the database via a web UI.


