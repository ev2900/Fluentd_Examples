# Send Apache access logs from an Ubuntu Cloud9 to a S3 bucket

Follow the instructions below

1. Run the CloudFormation stack below. It will create the required resources required for this example

[![Launch CloudFormation Stack](https://sharkech-public.s3.amazonaws.com/misc-public/cloudformation-launch-stack.png)](https://console.aws.amazon.com/cloudformation/home#/stacks/new?stackName=fluentd-demo&templateURL=https://sharkech-public.s3.amazonaws.com/misc-public/fluentd_cloud9.yml)

The resources created by the CloudFormation stack are documented in the architecture below

<img width="500" alt="Fluentd_cloud9_Architecture" src="https://github.com/ev2900/CloudFormation_Examples/blob/main/Architecture%20Diagrams%20for%20README/Fluentd_Cloud9_yml.png">

2. Open the Cloud9 environment and install Fluentd. Complete all of the subsequent steps in the Cloud9 terminal

```gem install fluentd --no-doc```

3. Install S3 plugin

```gem install fluent-plugin-s3```

4. Run Fluentd setup

```fluentd --setup ./fluent```

5. Open *fluent.conf* file under the *fluent* folder that was created during install and setup. Replace the content of the file with the content of the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/Cloud9_Apache_Logs_S3/fluent.conf) file in the repository

6. In the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/Cloud9_Apache_Logs_S3/fluent.conf)
- Replace *<your_aws_id>* next to *aws_key_id*
- Replace *<your_aws_security_key>* next to *aws_sec_key*
- Replace *<your_S3_bucket_name>* next to *s3_bucket* 

**Note** the CloudFormation stack creates an S3 bucket and IAM user that you may use for this example. The output section of the CloudFormation stack will provide you with the name of the S3 bucket and an access_id + security_key

7. Change the permissions on the */var/log/apache2/access.log* folder and the */var/log/td-agent/s3* folder to allow Fluentd access

```sudo chmod 777 /var/log/apache2/access.log``` <br>
```sudo mkdir /var/log/td-agent | sudo chmod 777 /var/log/td-agent```

8. Start Fluentd

```fluentd -c ./fluent/fluent.conf -vv &```

Optional. To stop Fluentd run ```pkill -f fluentd```

9. Generate sample Apache access log data

```ab -n 100 -c 10 http://localhost/```

Fluentd is now send your logs to S3. Open your S4 bucket and you will see a directory *logs/*. This directory will have a copy of the Apache access logs from your Cloud9 environment
