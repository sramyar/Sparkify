# Sparkify: Data Modeling and Pipelining for a Music Library
 This project involves data modeling and pipeling for Sparkify; a music library containing data on user activity as well as song and artist information.
 
 ## Installation and Requirements
 The data modeling is done in PostgreSQL. In addition, psycopg2 is used as the database adapter. Pandas library is required for data manipulation.
 
 ## Motivation
 Analyzing user activity requires well-organized data models to faciliate analytics and extract insights. In Sparkify, we intend to organize data in a Star Schema and dedicate separate tables for data on users, artits, songs, and activity. This enhances future data storage and accessibility as well as easier queries.
 
 ## Organization
 As mentioned earlier, the data is organized in form of a star schema containing the following tables:
 - song plays: this is the **fact** table containing these columns:
 * songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent
 
 Other tables are **dimension** tables including data on users, time, artists, and songs.
 - users: data on users with columns:
 * user_id, first_name, last_name, gender, level
 - songs: data on songs with columns:
 * song_id, title, artist_id, year, duration
 - artists: data on artits with columns:
 * artist_id, name, location, latitude, longitude
 - time: data on time and duration:
 * start_time, hour, day, week, month, year, weekday
 
 ## Data Engineering Process
 * The first step is data modeling and creating the tables. This is done in `sql_queries.py` containing the `CREATE TABLE` statements.
 * The next step is gathering the data and inserting it to the schemas. This involves the following steps:
 - The songs and artists' data are read from the `song_data` directory JSON files. The data are then transformed to pandas dataframe and used in the corresponding `INSERT` statements.
 - The log data for song plays, time, and users are extracted from the `log_data` directory JSON files.
 - The timestamps in the original data set was in *milliseconds* that is now transformed to standard datetime format.
 - The missing values for `userId` are omitted to preserve data consistency and integrity.
 - The songplays schema is filled in with data coming from the log data as well as querying the songs and artists tables to find matching items.
 - The pipeling process is implemented in the `etl.py`
 
 ## Files
 - `data` directory contains the songs and log data in JSON format
 - `create_tables.py` contains the `CREATE` and `INSERT` statements for creating and filling the schemas
 - `etl.ipynb` is the jupyter notebook as the scratchbook for developing the ETL process
 - `etl.py` is the python file for ETL
 - `test.ipynb` contains the test queries
 
 ## Acknowledgements
 Data is provided by [Million Songs Dataset](https://labrosa.ee.columbia.edu/millionsong/)