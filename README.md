# Fluentd Examples

1. Install Fluentd

```gem install fluentd --no-doc```

2. Install the S3 plugin

```gem install fluent-plugin-s3```

3. Run the the Fluentd setup

```fluentd --setup ./fluent```

4. Open the ```fluent.conf``` file under the fluent folder and replace the content of the folder with the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/fluent.conf) file. 

5. 

---

4. Open the ```fluent.conf``` file under the fluent folder that was created during the install and set up. Replace the content of the file 

Optional - ```sudo systemctl status td-agent.service``` provides the status of the Fluentd service <br />
Optional - ```sudo systemctl stop td-agent.service``` stops the Fluentd service

5. Ping the Apache Host to Generate Access Logs

```ab -n 100 -c 10 http://localhost/```
