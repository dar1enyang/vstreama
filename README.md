<p align="middle">
  <img src="https://github.com/dar1enyang/vstreama/blob/master/Images/vstreama.png" />

# Introduction

Knowing how customers interact with the platform via app or website is very important to the music streaming business. 

To entirely derive meaning from activity logs and song metadata, it's essential to design a data pipeline efficiently to complete the analysis answering to the following questions accordingly and iteratively.

The analytics team is interested in getting a better understanding of the following questions:

1. What types of songs are trending now? For what kind of audience?
2. Engagement - describes how active users are on the application
3. How long have users stayed on the app for each logging activity?

# Project Objective

Currently, there is no easy way to query the data to generate insights, since the data reside in a directory of JSON logs on user activity on the app, as well as a list with JSON metadata on the songs in the app.

Throughout this project, I have completed the following tasks:

1. Defined fact and dimension tables applying Star Schema to optimize queries on song play analysis
2. Build an ETL pipeline that transfers datasets into tables in Postgres using Python and SQL

# Technology 

<p align="middle">
  <img src="https://github.com/dar1enyang/vstreama/blob/master/Images/PostgreSQL.png" />
  <img src="https://github.com/dar1enyang/vstreama/blob/master/Images/Python.png" />

### Why SQL?

- Easier to change to business requirements- perform `adhoc queries` with ease
- Modeling the data not modeling queries
- ACID transactions: Guarantee validity even in event of errors, power failures



# Explore the datasets

##### 1. Song Dataset

The first dataset is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.

```txt
song_data/A/B/C/TRABCEI128F424C983.json
song_data/A/A/B/TRAABJL12903CDCF1A.json
```

And below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

```json
{"num_songs": 1, 
 "artist_id": "ARJIE2Y1187B994AB7", 
 "artist_latitude": null, 
 "artist_longitude": null, 
 "artist_location": "", 
 "artist_name": "Line Renaud", 
 "song_id": "SOUPIRU12A6D4FA1E1", 
 "title": "Der Kleine Dompfaff", 
 "duration": 152.92036, 
 "year": 0}
```

##### 2. Log Dataset

The second dataset consists of log files in JSON format. These describe app activity logs from a music streaming app based on specified configurations.

The log files in the dataset are partitioned by year and month. 

For example, here are filepaths to two files in this dataset.

```txt
log_data/2018/11/2018-11-12-events.json
log_data/2018/11/2018-11-13-events.json
```

And below is an example of what the data in a log file, 2018-11-12-events.json, looks like.

![](https://github.com/dar1enyang/vstreama/blob/master/Images/log-data.png)



### Schema for Song Played Analysis

Using the song and log datasets, I created a star schema optimized for queries on song play analysis. This includes the following tables.

![](https://github.com/dar1enyang/vstreama/blob/master/Images/erdplus-diagram.png)

---

# How to use this project

How to install and set up Postgres locally in case you want to follow along the project on your local machine. This [link](https://www.codementor.io/engineerapart/getting-started-with-postgresql-on-mac-osx-are8jcopb) provides it for MacOs. It goes through configuring Postgres, creating users, creating databases using the psql utility.

Perform ETL development in `etl.ipynb` and `test.ipynb`

1. Run `create_tables.py` to create database and tables 

   (Alter queries if you want in `sql_queries.py`)

2. Run `etl.py` to perform the complete ETL pipeline
