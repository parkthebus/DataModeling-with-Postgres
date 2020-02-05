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
>> - open song file(dataframe) and insert song, artist data into song_table and artist_table
>> - the inserted data is list of dataframe's specific columns at index 0.
>> - for example. select 'song_id','title','artist_id','year','duration' columns in dataframe as df and get values into list.
>>> ```list(df[['song_id','title','artist_id','year','duration']].values[0])```

- process_log_file(cur, filepath)
>> - open log file(dataframe) and filter by page==NextSong.
>> - convert timestamp columnn to datetime
>>> * use ```dataframe.assign()``` and ```datetime```library.
>>> * divide 1000 and convert each rows of timestamp_data('ts') in dataframe(df) to datetime using ```datetime``` library.
>>> <pre><code>t = df.assign(ts=[datetime.datetime.fromtimestamp(ts/1000) for ts in list(df['ts'])])</code></pre>
>> - extract timestamp, hour, day, week of year, month, year, and weekday data from timespamp converted dataframe and insert time data records into time_table.
>> - select user information from dataframe and insert into user_table.
>> - get songid and artistid from song and artist table using ```JOIN``` query.
>>> 1. get song, artist and length(duration) rows from dataframe iteration.
>>> 2. find songs from JOIN table using song, artist, length data
>>> *<pre><code>
SELECT s.song_id, a.artist_id 
FROM songs as s JOIN artists as a ON s.artist_id = a.artist_id
WHERE s.title = %s AND a.name = %s AND s.duration = %s;
</code></pre>
>>> 3.create songplay_data which insert into songplay_table.
>>> * get index from iteration enumerated number
>>> * get timestamp, userid, level, sessionid, location, useragent from dataframe's column
>>> * and use songid, artistid we've got above.
>>> <pre><code>songplay_data = (index, row.ts, row.userId, row.level, songid, artistid, row.sessionId, row.location, row.userAgent)</code></pre>
>>> <pre><code>cur.execute(songplay_table_insert, songplay_data)</code></pre>

