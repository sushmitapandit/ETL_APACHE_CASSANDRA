# Data Modeling with Apache Cassandra

Sparkify is a music streaming app Company. They have been collecting data on songs and user activity. Now they want to analyze using this data particularly to find out

  - Which songs users are listening to

## Data
Currently, the company do not have an easy way to query their data, their data resides in

  -  in a directory of CSV files on user activity on the app.

## Database creation and ETL data pipeline creation
We are creating Apache Cassandra database and creating an ETL pipeline to load data on the database.

### Data
  event_data is the dataset. The directory of CSV files are partitioned by date. The filepaths are given as event_data/<yyyy>-<mm>-<dd>-events.csv where <yyyy> indicates the year, <mm> indicates the month and <dd> indicates the year. The fields of of event_data are:

- artist (string)
- auth (string)
- firstName (string)
- gender (char)
- itemInSession (int)
- lastName (string)
- length (float)
- level (string)
- location (string)
- method (string)
- page (string)
- registration (float)
- sessionId (int)
- song (string)
- status (int)
- ts (float)
- userId (int)

##### Since, Apache cassandra is a no sql database. We design the tables keeping in mind the queries we want to perform.
### Queries used
1. Give me the artist, song title and song's length in the music app history that was heard during  sessionId = 338, and itemInSession  = 4
    - "SELECT artist, song, length from music_app_history WHERE sessionId=338 AND itemInSession=4"
 2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182.
     - "SELECT artist, song, firstName, lastName FROM artist_song_user_session WHERE userId=10 AND sessionId=182" 
 3. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'
    - "SELECT firstName, lastName FROM user_song WHERE song='All Hands Against His Own'" 

### ETL process
- Start with the raw csv data files as described in Dataset
- For each row of the csv data, insert the data in the appropriate column as described in Schema
- Perform the Select query as described in Queries
 



