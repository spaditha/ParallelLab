# Swathi Padithala AmazonTop100PositiveReviewers

# Executing AmazonTop100PositiveReviewers.java
**What are the top 100 Postive Verified reviewer first names?  What is the average rating "overall" for each of these names?**
1. Log into dsba-hadoop.uncc.edu using ssh
2. `https://github.com/spaditha/ParallelLab.git` to clone this repo
3. Go into the repo directory.  In this case: `cd ParallelLab`
4. Make a "build" directory (if it does not already exist): `mkdir build`
5. Compile the java code (all one line).  You may see some warnings--that' ok. 
`javac -cp /opt/cloudera/parcels/CDH/lib/hadoop/client/*:/opt/cloudera/parcels/CDH/lib/hbase/* AmazonTop100PositiveReviewers.java -d build -Xlint`
6. Now we wrap up our code into a Java "jar" file: `jar -cvf Process_toppositiveverifiedReviewers.jar -C build/ .`
7. This is the final step  
 - Note that you will need to delete the output folder if it already exists: `hadoop fs -rm -r /user/smamilla/Top100PositiveVerified_Reviewers` otherwise you will get an "Exception in thread "main" org.apache.hadoop.mapred.FileAlreadyExistsException: Output directory hdfs://dsba-nameservice/user/... type of error.
 - Now we execute the map-reduce job: ` HADOOP_CLASSPATH=$(hbase mapredcp):/etc/hbase/conf:Process_toppositiveverifiedReviewers.jar hadoop jar Process_toppositiveverifiedReviewers.jar AmazonTop100PositiveReviewers '/user/spaditha/Top100PositiveVerified_Reviewers'`
 - Once that job completes, you can concatenate the output across all output files with: `hadoop fs -cat /user/spaditha/Top100PositiveVerified_Reviewers/*
 ` or if you have output that is too big for displaying on the terminal screen you can do `hadoop fs -cat /user/spaditha/Top100PositiveVerified_Reviewers/* | sort -n -k3 -r > TopPositiveVerified_Reviewers.txt` 
 8. To get top 100 - ` hadoop fs -cat /user/spaditha/Top100PositiveVerified_Reviewers/* | sort -n -k3 -r | head -n100`
 9. store the output to text  `hadoop fs -cat /user/spaditha/Top100PositiveVerified_Reviewers/* | sort -n -k3 -r | head -n100 >Top100PositiveVerified_Reviewers.txt`
 
 The output is: in Top100PositiveVerified_Reviewers.txt
