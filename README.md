# Hadoop / Spark Recommendation Engine

Recommendation engine for music using last.fm dataset, with Spark running on Hadoop

Changed to MovieLens dataset because it's a lot cleaner and easier to use. Small version of the MovieLens dataset included, the large one failed to upload and caused syncing issues.

##To Run:##

* Start Apache Spark instance on IBM Bluemix

* Create a linked Object Storage

* Copy the contents of the dataset folder to the Object Storage
  
* **EDIT CREDENTIALS:**
  
 * vcap.json contains the Spark cluster credentials

 * Start of run.py contains Object Storage credentials (if this isn't altered it will fail with a Null Pointer Exception)
  
* Run RUNTHIS.sh in bash, can be used with \*nix or the Windows 10 bash terminal

* This runs spark-submit.sh with the required commands to upload run.py and engine.py and execute run.py on the Spark cluster
  
* The bash terminal will poll the cluster and provide some information about progress of the task
  
* Outputs downloaded to the current folder as stdout\_\<numbers\>, along with stderr and Spark logs
  
**WILL RUN WITHOUT A NEW SPARK CLUSTER AND OBJECT STORAGE SET UP AS LONG AS THE CURRENT CLUSTER IS ACTIVE**

##File List:##

dataset/movies_small.csv
> *movie data: movie_id, title, genre. Genre unused, but could improve accuracy by adding content-based filtering in addition to collaborative filtering*
  
dataset/ratings_small.csv
> *ratings: user_id, movie_id, rating, timestamp. 100k ratings total*
  
logs/bash output
> *outputs from bash for an example run of the task*
  
logs/Interesting Logs
> *failed with full dataset, appears to run out of resources*
  
logs/stdout
> *output, cleaned up slightly to be more readable with the test ratings included*
  
bluemix_get_file.py
> *old mostly pointless script for reading a file from Object Storage, used before credentials issues were sorted out*
  
engine.py
> *RecommendationEngine class*
  
key.ppk
> *unimportant*
  
README.md
> *this file, obviously*
  
run.py
> *main python script, trains the model and then adds test ratings for a new user (retraining), then gets recommendations*
  
RUNTHIS.sh
> *executes the task*
  
spark-submit.sh
> *script to interface with the Spark cluster, provided by IBM*
  
vcap.json
> *Spark credentials*

##References##

Heavily based on the tutorial from codementor.io available [here](https://www.codementor.io/spark/tutorial/building-a-recommender-with-apache-spark-python-example-app-part1)

IBM Bluemix documentation, mostly [here](https://console.ng.bluemix.net/docs/services/AnalyticsforApacheSpark/index-gentopic1.html#genTopProcId2), [here](https://console.ng.bluemix.net/docs/services/AnalyticsforApacheSpark/index-gentopic3.html#genTopProcId4), and [here](https://console.ng.bluemix.net/data/notebooks/samples/Precipitation%20Analysis)

Uses the [GroupLens MovieLens dataset](http://grouplens.org/datasets/movielens/)

[Spark documentation](http://spark.apache.org/docs/latest/mllib-collaborative-filtering.html)

[R-Bloggers](https://www.r-bloggers.com/recommender-systems-101-a-step-by-step-practical-example-in-r/) helped to understand the subject a bit better
