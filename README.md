# Mars Demonstration
Monitoring, Auditing and Reporting System (MARS)

## TO MAKE **MARS** WORK
gcloud config set project YOURPROJECTNAME\
Bucket named "projectid-bucket"\
Dataflow API enabled  (enabled via script in run-cloud.sh)\
    `Command:
    gcloud services enable dataflow.googleapis.com`

BigQuery Dataset called "mars"\
    `Command: 
        bq mk mars`

BigQuery Table called "activities" - starting schema\
    `Command: 
        bq mk --schema 
        timestamp:STRING,ipaddr:STRING,action:STRING,srcacct:STRING,destacct:STRING,amount:NUMERIC,customername:STRING 
        -t mars.activities`
    
    `Schema:
        timestamp:STRING,
        ipaddr:STRING,
        action:STRING,
        srcacct:STRING,
        destacct:STRING,
        amount:NUMERIC,
        customername:STRING`

Copy Data Studio Dashboard and adjust to your project.dataset.table\
    https://datastudio.google.com/reporting/3f79b633-ac24-43b3-86c8-41f386ea514a


Sample Data Bucket: gs://moonbank-mars-sample\
Production Data Bucket: gs://moonbank-mars-production\

## CONVERSION TO PUB/SUB
gcloud pubsub subscriptions create mars-activities --topic projects/moonbank-mars/topics/activities\
Update requirements.txt\
    add google-cloud-pubsub==1.7.0\