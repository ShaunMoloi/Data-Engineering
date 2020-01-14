# Sparkify Project

## Background

<p>A startup company called Sparkify provides music streaming to the users through the application. The analytics team is interested in understanding what songs users are listening to. The analytics team would like to analyse the data and gather insights and understanding to what songs their client base listens to. At the moment the team does not have a robust way to query the data which is stored in JSON formats about the song details and user activity from the application. The data is stored in JSON log files and meta data hosted on two local directories. </p>

<p>As a Data Engineer assigned to this task, I am going to assist Sparkify: </p>

- 1. Creating a Data Model with Postgres
- 2. Design Database, through defining fact and dimension tables for a star schema
- 3. Automate an ETL pipeline that transfers data from two local directories


### Sparkify Datasets

- **Song dataset**: All song data is in JSON format under a subdirectory from root in */data/song_data*.

- **Log dataset**: All log data are in JSON format under a subdirectory from root in */data/log_data*. 


### Database Schema
The data consists of a main fact table containing all foreign keys and four dimensional tables with primary keys, thus, a *star schema* will be used for the project: 
#There is one main fact table containing all the measures associated to each event (user song plays), 
#and 4 dimentional tables, each with a primary key that is being referenced from the fact table.

On why to use a relational database for this case:
- Potential to use JOINS when querying data
- Ability to use Structured Query Language (SQL) for analysis purposes
- Referential integrity

#### Fact Table
**songplays** - records in log data associated with song plays i.e. records with page NextSong
- songplay_id (INT) PRIMARY KEY
- start_time (TIMESTAMP) NOT NULL
- user_id (INT) NOT NULL
- level (VARCHAR)
- song_id (VARCHAR)
- artist_id (VARCHAR)
- session_id (INT)
- location (VARCHAR)
- user_agent (VARCHAR)

#### Dimension Tables
**users** - users in the app
- user_id (INT) PRIMARY KEY
- first_name (VARCHAR) 
- last_name (VARCHAR) 
- gender (VARCHAR)
- level (VARCHAR)

**songs** - songs in music database
- song_id (VARCHAR) PRIMARY KEY
- title (VARCHAR)
- artist_id (VARCHAR) NOT NULL
- year (INT)
- duration (FLOAT) 

**artists** - artists in music database
- artist_id (VARCHAR) PRIMARY KEY
- name (VARCHAR)
- location (VARCHAR)
- latitude (NUMERIC)
- longitude (NUMERIC)

**time** - timestamps of records in songplays broken down into specific units
- start_time (TIMESTAMP) PRIMARY KEY
- hour (INT)
- day (INT)
- week (INT)
- month (INT)
- year (INT)
- weekday (VARCHAR)


### Project structure

Files in the repository for the project:
1. **data** folder nested on root cointaining JSON files.
2. **create_tables.py** Python script to drop and create tables. You run this file to reset your tables before each time you run your ETL scripts.
3. **etl.ipynb** This jupyter notebook reads and processes a single file from song_data and log_data and then loads the data into your tables. 
4. **README.md** Markdown file includes a summary of the project, how to run the Python scripts, and an explanation of the files in the repository.
5. **sql_queries.py** Python script that contains all the SQL queries for Sparkify.
6. **etl.py** reads and processes files from song_data and log_data and loads them into your tables. 
7. **test.ipynb** Is a Jupyter notebook which enables for testing to display if the first few rows of each table have been succesfully uploaded.


### How to run project. 

1. Using the terminal, run create_tables.py using the command supplied below, this will allow you to QUERY, DROP, CREATE and INSERT query statements in sql_queries.py:
```
python create_tables.py
```
2. Run each cells inside the Jupyter notebook test.ipyn to check if the tables have been correctly loaded. 

3. Once step 2 has been verified, running etl.py will: Connect to the sparkify database, create tables, begin processing song and log data, apply dataframe parameters and finally query the data. Run using command below:

 ```
python etl.py
```

###Success, if project does not run feel free to reach out to me or drop an email to moloishaun5@gmail.com

