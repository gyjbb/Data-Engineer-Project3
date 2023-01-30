# Data-Engineer-Project3
Create Data Warehouse with AWS Redshift
Sparkify, a music stream startup, would like to move the data storage and analytics process to cloud services AWS as the datasets for songs and users keep increasing. The users activities datasets and song metadata resides in AWS S3 in the form of JOSN logs. In this project, ETL pipelines would be built to extract data in S3, and stage the dtaa in Redshift. And dimensional tables would be designed.

## Project Dataset
The two original datasets reside in S3 in the form of JSON logs.
#### Song Dataset
The song dataset consists of metadata for song details. The files are catelogged by the first three leters of song's tracking ID. For example, the file paths are listed below: \
![song data path](https://github.com/gyjbb/Data-Engineer-Project3/blob/main/song_data_path.png?raw=true) \
And a song file contains the details of the song: \
![song data](https://github.com/gyjbb/Data-Engineer-Project3/blob/main/song_data.png?raw=true) 


#### Log Dataset
The log dataset is about the song play activities of users in Sparkify app. The data was collected on a daily basis. below are the log file path for each day's activities: \
![log data path](https://github.com/gyjbb/Data-Engineer-Project3/blob/main/log_data_path.png?raw=true) \
And below is an example of the data in a single log file: \
![log data](https://github.com/gyjbb/Data-Engineer-Project3/blob/main/log_data.png?raw=true) 

## Database schema
#### staging tables
Staging tables provide a buffer between the Redshift warehouse and the data sources. Data file in S3 are process into two staging tables:
- staging_songs: process the song files into a table 
- staging_events: process the log files into a table 
#### fact tables
- song_plays: records event data associated with song plays. Columns include: 
  - songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent 
#### dimension tables
- user: app users
  - user_id, first_name, last_name, gender, level 
- songs: songs in song dataset
  - song_id, title, artist_id, year, duration 
- artists: artists on song dataset
  - artist_id, name, location, lattitude, longitude 
- time: timestamp of song play records 
  - start_time, hour, day, week, month, year, weekday

## Project structure
The project includes the following python files: 
- create_cluster_IaC.py: the Infrastructure as Code file that creates a cluster and a role Note: Make sure that the role and the cluster are connected to the right secuirty group. 
- create_table.py: contains fact and dimension tables for the star schema in the Redshift data warehouse. 
- etl.py: data gets loaded from S3 into staging tables on Redshift and then processed into the analytics tables on Redshift. 
- sql_queries.py: SQL statements are defined, which are then used by etl.py, create_table.py. 

## Steps to run
Create IAM role in AWS and save the  aws_access_key and aws_secret_access_key in the dwh.cfg file. \
Then run the create_cluster script to set up the needed infrastructure for this project. \
Run the create table script to set up the database staging tables. \
Finally, run the etl script to extract data from the files in S3, stage it in Redshift, and store it in the dimensional tables for analytical process.









