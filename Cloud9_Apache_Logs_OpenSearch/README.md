# Send Apache access logs from an Ubuntu Cloud9 to a S3 bucket

Follow the instructions below

1.

2. Open the Cloud9 environment and install Fluentd. Complete all of the subsequent steps in the Cloud9 terminal

```gem install fluentd --no-doc```

3. Install OpenSearch plugin

```gem install fluent-plugin-opensearch```

4. Run Fluentd setup

```fluentd --setup ./fluent```


