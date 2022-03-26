# Fluentd Examples

1. Install Fluentd

```curl -fsSL https://toolbelt.treasuredata.com/sh/install-ubuntu-bionic-td-agent4.sh | sh```

2. Install the S3 plugin

```gem install fluent-plugin-s3```

3. Configure the Fluentd agent

```sudo vim /etc/td-agent/td-agent.conf```

Copy code from [td-agent.conf]()

4. Start the Fluentd service

```sudo systemctl start td-agent.service```

Optional - ```sudo systemctl status td-agent.service```
optional - ```sudo systemctl stop td-agent.service```

5. Ping the Apache Host to Generate Access Logs

```ab -n 100 -c 10 http://localhost/```
