# This is Guide on Using GATK4 on Seasnet for CS259

[https://ariesll.github.io/CS259-GATK-Guide/](https://ariesll.github.io/CS259-GATK-Guide/)

You need to work on your SEAS temporary folder, /w/tempcs259/${seasID}.

Please change ${seasID} as your seasnet account in the following setup.

The scripts are self-explanary, please make change on file and directory path as needed. 


## Log on to lnxsrv02
Log on to lnxsrv02.seas.ucla.edu 
(We request this machine to run Spark applications for CS259 students)

## Setup JAVA 8 environment
`export JAVA_HOME=/usr/local/cs133/2017cs259/jdk1.8.0_73`

`export PATH=${JAVA_HOME}/bin:$PATH`

`export LD_LIBRARY_PATH=${JAVA_HOME}/jre/lib/amd64/server/:$LD_LIBRARY_PATH`

## Setup GATK4 tool
`git clone https://github.com/broadinstitute/gatk.git`

After download and unzip gatk folder, within gatk folder (please also read gatk git README), use the following to build GATK4.

`./gradlew installAll`


## Setup Spark
`wget http://d3kbcqa49mib13.cloudfront.net/spark-2.1.0-bin-hadoop2.7.tgz`

`tar –xvzf spark-2.1.0-bin-hadoop2.7.tgz`

`cd spark-2.1.0-bin-hadoop2.7/conf`

`cp spark-env.sh.template spark-env.sh`

You need to configure spark environment (spark.local.dir) by changing spark-env.sh. (Please refer details on http://spark.apache.org/docs/latest/configuration.html)

add two lines in the spark-env.sh

*export SPARK_LOCAL_DIRS=/w/tempcs259/${seasID}/SPARK_TMP/*

*export SPARK_WORKER_DIR=/w/tempcs259/${seasID}/SPARK_TMP/*

this will setup temporary files directory when running Spark applications. Now it is in your CS259 temporary directory. 

*Make sure you already mkdir /w/tempcs259/${seasID}/SPARK_TMP*

## Run GATK pipeline

copy GATK launch pipeline script,

`cp /usr/local/cs133/2017cs259/local_reads_pipeline.sh /usr/local/cs133/${seasID}`

change the local_reads_pipeline.sh by specifying ${seasID} in the script.


launch local_reads_pipeline.sh using 8 cores

`./local_reads_pipeline.sh 8`

You could run with different core number by giving different number as input.

And after successful running, you will get output bam file in /w/tempcs259/${seasID}.

## Monitor using Spark GUI

Your could using ssh -XY lnxsrv02.seas.ucla.edu to enable X forwarding.
Then launch firefox using

`firefox&`

make sure Xming (windows) or Xterm (mac) are turned on.

And in firefox, go to localhost:4040, you can monitor the running spark application.









