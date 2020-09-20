# Data Pipeline With Amazon Redshift and Apache Airflow                           

![N|Solid](https://cdn.freelogovectors.net/wp-content/uploads/2018/07/amazon-redshift-logo.png)

# Introduction
A music streaming startup, Sparkify, has grown their user base and song database and want to move their processes and data onto the cloud. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As their data engineer, my job tasked with building an ETL pipeline that extracts their data from S3, stages them in Amazon Redshift, and transforms data into a set of dimensional tables for their analytics team to continue finding insights in what songs their users are listening to. Also create a Data Pipeline to update the data every single day.

# Project Description
In this project, I have to apply data warehouses and AWS to build an ETL pipeline for a database hosted on Amazon Redshift. To complete the project, I needed to load data from S3 to staging tables on Redshift and execute SQL statements that create the analytics tables from these staging tables.

# Dataset
We have 2 types of .json files i.e. song_data , log_data. We have to extract data from json files and import it into tables for analysis.

### song_data
Song data file structure example.
`song_data/A/B/C/TRABCEI128F424C983.json`
`song_data/A/A/B/TRAABJL12903CDCF1A.json`

Here is the example of TRAABJL12903CDCF1A.json file.

```json
{
   "num_songs": 1,
  "artist_id": "ARJIE2Y1187B994AB8",
  "artist_latitude": null,
  "artist_longitude": null,
  "artist_location": "",
  "artist_name": "Line Renaud",
  "song_id": "SOUPIRU12A6D4FA1R9",
  "title": "Der Kleine Dompfaff",
  "duration": 162.92036,
  "year": 0
}
```

### log_data
log data file structure example.
`log_data/2018/11/2018-11-12-events.json`
`log_data/2018/11/2018-11-13-events.json`

Here is an example of `2020-11-12-events.json` file.

```json
{
  "artist": "Pavement",
  "auth": "Logged In",
  "firstName": "Sylvie",
  "gender": "F",
  "itemInSession": 0,
  "lastName": "Cruz",
  "length": 99.16036,
  "level": "free",
  "location": "Washington-Arlington-Alexandria, DC-VA-MD-WV",
  "method": "PUT",
  "page": "NextSong",
  "registration": 1540266185796.0,
  "sessionId": 345,
  "song": "Mercy:The Laundromat",
  "status": 200,
  "ts": 1541990258796,
  "userAgent": "\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_4) AppleWebKit/537.77.4 (KHTML, like Gecko) Version/7.0.5 Safari/537.77.4\"",
  "userId": "10
}
```

# Project Steps

## Step 1: Create a Redshift Cluster

- Set up IAM Roles, Redshift Clusters, Config files and security groups.
- Open Redshift Dashboard.
- Configure general Redshift settings and start the cluster.
- Alternatively you can also setup the cluster using python script.


> Get the host name and database information from Redshift cluster and update it in `dwh.cfg` file.

## Step 2: Create tables.

- Edit the `sql_queries.py` and add all the create tables query.
- Run the `create_table.py` script.


## Step 3: Build ETL Pipeline.

- Implement the logic in `etl.py` to load data from S3 to staging tables on Redshift.
- Implement the logic in `etl.py` to load data from staging tables to analytics tables on Redshift.
- Test by running `etl.py` after running create_tables.py and running the analytic queries on  Redshift database to compare your results with the expected results.
- Delete your redshift cluster when finished.


### Final Tables.

#### Fact Table
> songplays table : this table stores the details of the songs being played.

| start_time  | user_id | level | song_id | artist_id | session_id | location | user_agent |
| ------ | ------ |  ------ | ------ |  ------ | ------ | ------ | ------ |


#### Dimension Tables.

> Song Table

| song_id             | title                       | artist_id | year | duration |
| ------ | ------ |  ------ | ------ |  ------ |

> Artist Table

| artist_id           | name                      | location | latitude | longitude |
| ------ | ------ |  ------ | ------ |  ------ |


> time_table

| start_time  | hour | day | week | month | year | week_day |
| ------ | ------ |  ------ | ------ |  ------ | ------ | ------ |

> users table,

| user_id   | first_name| last_name | gender | level |
| ------ | ------ |  ------ | ------ |  ------ | 


# Conclusion

In this project you'll be able to successfully make a Redshift cluster and copy data from Amazon S3 bucket and make the tables. In the final stage Data Pipeline is built using Apache Airflow.
