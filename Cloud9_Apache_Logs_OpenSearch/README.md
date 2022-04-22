# Send Apache access logs from an Ubuntu Cloud9 to a S3 bucket

Follow the instructions below

1. Run the CloudFormation stack below. It will create the required resources required for this example

TO DO - CLOUD FORMATION STACK
  
The resources created by the CloudFormation stack are documented in the architecture below
  
TO DO - ARCHITECTURE DIAGRAM

2. Map IAM user to all_access OpenSearch role

TO DO - INSTRUCTIONS

3. Open the Cloud9 environment and install Fluentd. Complete all of the subsequent steps in the Cloud9 terminal

```gem install fluentd --no-doc```

4. Install OpenSearch plugin

```gem install fluent-plugin-opensearch```

5. Run Fluentd setup

```fluentd --setup ./fluent```

6. Open fluent.conf file under the fluent folder that was created during install and setup. Replace the content of the file with the content of the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/Cloud9_Apache_Logs_OpenSearch/fluent.conf) file in the repository

7. In the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/Cloud9_Apache_Logs_OpenSearch/fluent.conf)

* Replace <your_aws_id> next to aws_key_id
* Replace <your_aws_security_key> next to aws_sec_key
* Replace <your_S3_bucket_name> next to s3_bucket

