<b>PROBLEM DESCRIPTION</b>:

The JSON data set represents the email activity of customers during a campaign.
PS: Please make necessary assumptions where necessary 

<b>DELIVERABLES</b>:
1) Script to load the data
2) Table(s) design 

<b>DIRECTORY STRUCTURE</b>:

- /config - This directory contains project configuration settings and, if needed, connectivity setting to any RDBMS
- /data - This directory contains SQLite DB
- /data - This directory contains log file. In production, timestamp would be added to each log file name.
- /sql - This directory contains all SQL scripts


3) Assumptions

    <b>ASSUMPTIONS MADE</b>:
    1) This solution is not for real-time processing and therefore does not streaming
    2) Each email campaign is provided in JSON files. Each JSON file contains responses for a single campaign. 
    In case of additional responses for the same campaign, they will be upserted into the database
    3) This solution uses SQLiteDB for portability purposes. In production, it would be replaced with a full-scale RDBMS.
    4) Due to the use of SQLiteDB, each table has only column "updated", vs typically used "created" and "updated" and does not use UPSERT operator that is not available for this version of SQLite 3.6. In production, the code would include both "created" and "updated" and the new records would be upserted to update, for instance, users who decided to get unsibscribed.

4) Write SQL to answer the following questions (Use the tables designed above) 
   - Get emails of users who opened email
   - Number of users who opened emails between 1-2 days, 2-5 days and > 5 days after email is sent. Example: If the email is sent 21st, # of users who opened email between 23rd and 26th including both 23rd and 26th
   - Identify the campaign which is more successful? (Define what you think success means and write SQL) 
5) Dockerize the solution
6) Any test cases you can think of?

<b>RESPONSE: The following parameters can be subject to A/B testing:</b>

-	Subject line (Length, Topic, Personalization)
-	Pre-header (Inclusion, Content)
-	Day or time (Day of week, time)
-	Call to action (Copy, color)
-	Content (positive, specific or generic)


7) How would you design it if it was streaming data?

<b>RESPONSE: If latency is an issue, then Kafka or Spark streaming would more appropriate than Python processing of batch processing. Otherwise, Python would be OK.</b>

The Spark-based solution for data stream would be a microservice with REST API where JSON data are processed by Spark and the processed data would be stored in datastore.
The Python code would be adapted for PySpark.

8) Any other insights you can derive from the data? 

<b>RESPONSE: The following metrics can be captured to measure email campaign funnel</b>
- #1: Number of emails delivered
- #2: Number of emails opened
- #3: Click-through rate
- #4: Click-to-open rate
- #5: Unsubscribe rate
- #6: Bounce rate
- #7: Spam complaints 




