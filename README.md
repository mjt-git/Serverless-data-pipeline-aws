# Serverless-data-pipeline-aws

This is a project to demo serverless data pipeline within AWS.

The basic workflow looks like below:

![alt text](https://camo.githubusercontent.com/bb29cd924f9eb66730bbf7b0ed069a6ae03d2f1a/68747470733a2f2f757365722d696d616765732e67697468756275736572636f6e74656e742e636f6d2f35383739322f35353335343438332d62616537616638302d353437612d313165392d393930392d6135363231323531303635622e706e67)

Two AWS lambda function is used, which are consumer and producer.

This project is a reproduce from https://github.com/noahgift/awslambda

### Caveat & Bug fixed

1. "Task ... is time out"

> By default, the lambda function has time limit of 3 seconds. However, the consumer lambda function has a little bit complex logic to deal with, so it always exceeds 3 seconds when fetching “s3” resource from boto3. 
> At first I thought the issue was caused by API version, but it turned out that codes are correct, just increasing the time limit of lambda function works.

2. Variables' value shoule be set correctly.
> According to aws setting, correctly assign variables like “BUCKET”, “REGION” in consumer lambda function.

3. Second lambda function can't be deployed with service provided in cloud9
> After creating producer lambda function, I can’t deploy consumer lambda function with service provided in cloud9. Instead, I have to use command line tools (“sam deploy --guided”) to deploy Consumer SAM application

4. The original Wikipedia api call raised error “Page id "google\" does not match any pages. Try another id!”
> Add extra arguments to solve.
> wikipedia_snippit.append(wikipedia.summary(name, sentences=1, auto_suggest=False, redirect=True))
