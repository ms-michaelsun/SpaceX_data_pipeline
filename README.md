# SpaceX Missions Data Engineering Pipeline

## Overview
This project implements a modern data engineering pipeline that extracts data from the SpaceX API, loads it into Snowflake data warehouse using Singer framework, and transforms it using dbt (data build tool). The pipeline enables analysis of SpaceX launches, rockets, and missions data in a structured and scalable way.

## Architecture
![Architecture Diagram](/data-arq.png)

The pipeline consists of the following components:

### 1. Data Source
- **SpaceX API**: Public REST API providing comprehensive data about SpaceX operations
- Endpoints include launches, rockets, missions, crew, and more
- Data is retrieved in JSON format

### 2. Data Ingestion
- **Singer Tap (Python)**: Custom tap implementation to extract data from SpaceX API
- **Singer Target**: Snowflake connector for loading data
- Incremental loading capability to handle updates efficiently
- Error handling and retry mechanisms
- Logging and monitoring integration

### 3. Data Storage
- **Snowflake Data Warehouse**: Cloud-native storage solution
- Raw data zone for initial data landing

### 4. Data Transformation
- **DBT (Data Build Tool)**: Modern transformation framework
- Modular transformation logic
- Testing and documentation


## Setup and Installation

This is an opinionated setup. You might not need to do it the way I do.
Each folder has a separate virtual requirements and virtual environment.
This helps us keep the dependencies separate.

The only requirement to run this project is uv.
To install uv, run:

```sh
brew install uv
```

### Intro Scripts

To run the intro scripts, run:

```sh
cd intro
uv sync
uv run -- <script.py>
```

### Tap

Our tap lives in tap-spacex.
To set that up run:

```sh
cd tap-spacex
uv sync
uv run -- python tap_sapcex.py
```

### Target

Our tap lives in tap-spacex.
To set that up run:

```sh
cd tap-spacex
uv sync
```

### Running the pipeline

To run the data integration pipeline run:

```sh
cd target-snowflake
cp sample.config.json config.json
```

Edit the config.json file to include your snowflake credentials.
Then run:

```sh
bash pipeline.sh
```
