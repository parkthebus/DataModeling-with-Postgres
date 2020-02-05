DataModeling-with-Postgres
=============================
>Udacity Data Engineering Nanodegree program Project 1. Data Modeling with Postgres




The README file includes a summary of the project, how to run the Python scripts, and an explanation of the files in the repository. Comments are used effectively and each function has a docstring.

How to start
-------
1. Create Tables 
>    ```python create_table.py```
2. Run ETL script
> ```python etl.py```

Description
-----
create_tables.py
> create and drop tables

sql_queries.py
> contains all sql queries (CREATE, DROP, INSERT, SELECT)

etl.py
- process_song_file(cur, filepath)
>> - open song file and insert song, artist data into song_table and artist_table
>> - the inserted data is list of dataframe's specific columns at index 0.
>> - for example. select 'song_id','title','artist_id','year','duration' columns in dataframe as df and get values into list.
>>> ```list(df[['song_id','title','artist_id','year','duration']].values[0])```
