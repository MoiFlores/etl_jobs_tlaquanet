# TlaquaNet ETL: Parallel Insights Challenge

## Project Overview
This repository contains a modular ETL pipeline that moves data from a PostgreSQL application database to a Snowflake Data Warehouse using Apache Spark and Airflow.

## Challenge: Implementing Parallel Insights
For this exercise, you will learn how to expand a data pipeline by adding a new, independent task that runs in parallel with existing ones.

### The Objective
Implement a "Most Popular Posts" insight job that calculates the top 3 most engaging posts based on likes and comments. This task should run at the same time as the "User Engagement" job.

### Step-by-Step Implementation Guide

#### 1. Define the Analytical Logic (SQL)
Create a new SQL script to perform the aggregation. This script should:
*   Identify the central content table (Posts).
*   Join with engagement tables (Likes and Comments).
*   Assign points to different actions (e.g., 1 point per like, 2 points per comment).
*   Sort and limit the results to the top 3.
*   Save the result into a new dedicated insights table in Snowflake.

#### 2. Create the Python Execution Script
Develop a small Python script to serve as the "bridge" between the workflow orchestrator and the database. This script will:
*   Locate the SQL file you created in Step 1.
*   Establish a secure connection to Snowflake using environment variables.
*   Execute the SQL instructions.

#### 3. Update the Orchestration Logic (Airflow DAG)
Modify the Airflow DAG to include the new task. To achieve true parallelism, you must:
*   Define a new task using the appropriate Operator (e.g., DockerOperator).
*   Configure the task dependencies so it starts immediately after the main data load finishes.
*   Group it with other independent tasks to ensure they run concurrently.

#### 4. Build and Verify
*   Rebuild your project's container image to include the new files.
*   Trigger the workflow in the Airflow UI.
*   Use the "Graph View" to visually verify that the pipeline "branches" into two parallel paths after the main Spark job.

---
