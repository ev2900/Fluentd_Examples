# Send Apache access logs from an Ubuntu Cloud9 to OpenSearch

Follow the instructions below

1. Run the CloudFormation stack below. It will create the required resources required for this example

[![Launch CloudFormation Stack](https://sharkech-public.s3.amazonaws.com/misc-public/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=fluentd-demo-opensearch&templateURL=https://sharkech-public.s3.amazonaws.com/misc-public/fluentd_cloud9_opensearch.yml)
  
The resources created by the CloudFormation stack are documented in the architecture below

<img width="650" alt="Fluentd_cloud9_Architecture" src="https://github.com/ev2900/CloudFormation_Examples/blob/main/Architecture%20Diagrams%20for%20README/fluentd_cloud9_opensearch_yml.png">

2. Open the Cloud9 environment and Map IAM user to all_access OpenSearch role by running the [map_IAM_user.py](https://github.com/ev2900/Fluentd_Examples/blob/main/Cloud9_Apache_Logs_OpenSearch/map_IAM_user.py) python script in the Cloud9 terminal

* Update the ```os_url``` variable with the URL of the OpenSearch domain endpoint 
* Update the ```iam_arn``` variable with the IAM of the role created by the CloudFormation stack

Note the CloudFormation stack output section can provide you with the domain endpoint URL and IAM role arn value

Once you have updated the values save the file and ```python map_IAM_user.py``` in the Cloud9 terminal 

3. Install Fluentd. Complete all of the subsequent steps in the Cloud9 terminal

```gem install fluentd --no-doc```

4. Install OpenSearch plugin

```gem install fluent-plugin-opensearch```

5. Run Fluentd setup

```fluentd --setup ./fluent```

6. Open fluent.conf file under the fluent folder that was created during install and setup. Replace the content of the file with the content of the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/Cloud9_Apache_Logs_OpenSearch/fluent.conf) file in the repository

7. In the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/Cloud9_Apache_Logs_OpenSearch/fluent.conf)

* Replace <opensearch_domain_endpoint> next to url with the domain endpoint of your OpenSearch domain
* Replace <aws_region> next to region with the region of your OpenSearch domain ex. ```us-east-1``` 
* Replace <your_aws_id> next to aws_key_id
* Replace <your_aws_security_key> next to aws_sec_key

**Note** the CloudFormation stack creates an OpenSearch domain and IAM user that you may use for this example. The output section of the CloudFormation stack will provide you with the name of the ccess_id, security_key, AWS REGION and OPENSEARCH DOMAIN URL

8. Change the permissions on the */var/log/apache2/ * folder and the */var/log/td-agent/ * folder to allow Fluentd access

If folder does not exist ```sudo mkdir /var/log/apache2/``` then run ```sudo chmod 777 /var/log/apache2/ ``` <br>
If folder does not exists ```sudo mkdir /var/log/td-agent/``` then run ```sudo chmod 777 /var/log/td-agent/ ```
  
9. Start Fluentd
  
  ```fluentd -c ./fluent/fluent.conf -vv &```

Optional. To stop Fluentd run ```pkill -f fluentd```
  
10. Generate sample Apache access log data
  
```ab -n 100 -c 10 http://localhost/```
  
