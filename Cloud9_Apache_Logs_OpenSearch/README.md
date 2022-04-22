# Send Apache access logs from an Ubuntu Cloud9 to a S3 bucket

Follow the instructions below

1. Run the CloudFormation stack below. It will create the required resources required for this example

TO DO CLOUD FORMATION STACK
  
The resources created by the CloudFormation stack are documented in the architecture below
  
TO DO ARCHITECTURE DIAGRAM

2. Map IAM user to all_access OpenSearch role

TO DO INSTRUCTIONS

3. Open the Cloud9 environment and install Fluentd. Complete all of the subsequent steps in the Cloud9 terminal

```gem install fluentd --no-doc```

4. Install OpenSearch plugin

```gem install fluent-plugin-opensearch```

5. Run Fluentd setup

```fluentd --setup ./fluent```

6. Open fluent.conf file under the fluent folder that was created during install and setup. Replace the content of the file with the content of the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/Cloud9_Apache_Logs_OpenSearch/fluent.conf) file in the repository

7. In the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/Cloud9_Apache_Logs_OpenSearch/fluent.conf)

* Replace <url> next to url with the domain endpoint of your OpenSearch domain
* Replace <region> next to region with the region of your OpenSearch domain ex. ```us-east-1``` 
* Replace <your_aws_id> next to aws_key_id
* Replace <your_aws_security_key> next to aws_sec_key

*Note* the CloudFormation stack creates an OpenSearch domain and IAM user that you may use for this example. The output section of the CloudFormation stack will provide you with the name of the ccess_id, security_key, AWS REGION and OPENSEARCH DOMAIN URL

8. Change the permissions on the
  
9. Start Fluentd
  
10. Generate sample Apache access log data
  
```ab -n 100 -c 10 http://localhost/```
  
