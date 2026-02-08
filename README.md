# Tennis Data Analysis (Databricks Lakehouse)

## Overview
This repository contains exploratory and analytical work focused on professional tennis data.  
The goal of this project is to create data engineering and analytics workflows using modern lakehouse patterns in Databricks. Publicly available tennis data is ingested and prepared to support downstream match- and point-level analysis.

At this stage, the repository serves as a foundation for deeper tennis analytics.

## Technology Stack
- Databricks (Serverless Compute)
- Unity Catalog & Volumes
- Delta Lake tables
- PySpark
- Databricks Workflows for orchestration
- GitHub for version control

## Data Source & License
This project uses publicly available tennis data from **Jeff Sackmann / Tennis Abstract**.

Source: https://github.com/JeffSackmann  

The data is licensed under the **Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License (CC BY-NC-SA 4.0)**.  
Attribution is required, and the data is used for non-commercial, educational, and portfolio purposes only.

## First Point Analysis
#### [Match First Point Winner](https://github.com/ashleyann9535/tennis-analysis/tree/fd2afbd0dfc95868a1be350778754b4fb33f57ce/notebooks/first_point_analysis/match_first_point_winner)
This section analyzes the question:

**If the first point of a match is a rally (more than 4 shots), does winning that point increase the likelihood of winning the match?**

##### Data Sources
The analysis uses point-by-point data from multiple Grand Slam tournaments:
- Australian Open: 2017, 2020-2021
- French Open: 2016-2017, 2020-2021
- Wimbledon: 2016-2019, 2021-2024
- US Open: 2016-2024

Data was processed using a bronze → silver → gold pipeline in Databricks Unity Catalog.

##### Results
Across all tournaments and seasons analyzed:
- When a player won the first point of the match, they won the match 56% of the time
- When a player lost the first point, they still won the match 44% of the time

##### Conclusion
Winning the first point—when it is a longer rally—does not have a meaningful impact on match outcome. The result shows only a slight advantage and is not a strong predictor of who will win the match.

##### Orchestration
The end-to-end pipeline is orchestrated in Databricks Workflows.  
An example export of the job configuration is included in:

[/pipeline/match_first_point_winner.json](https://github.com/ashleyann9535/tennis-analysis/blob/fd2afbd0dfc95868a1be350778754b4fb33f57ce/pipelines/match_first_point_winner.json)

This workflow triggers on new files arriving in the Unity Catalog volume and executes:

**file_ingestion → bronze → silver → gold**

This design enables repeatable and incremental processing as new tournament data becomes available.

