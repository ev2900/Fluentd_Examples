# Fluentd Examples

1. Install Fluentd

```gem install fluentd --no-doc```

2. Install the S3 plugin

```gem install fluent-plugin-s3```

3. Run the the Fluentd setup

```fluentd --setup ./fluent```

4. Open the ```fluent.conf``` file under the fluent folder and replace the content of the folder with the [fluent.conf](https://github.com/ev2900/Fluentd_Examples/blob/main/fluent.conf) file. 

5. Change the premissions on the ```/var/log/apache2/access.log``` folder and the ```/var/log/td-agent/s3``` folder to allow Fluentd access

sudo chmod 777 ```/var/log/apache2/access.log```
sudo chmod 777 ```/var/log/td-agent/s3```

6. Start Fluentd

```fluentd -c ./fluent/fluent.conf -vv &```

Optinal to stop Fluentd run ```pkill -f fluentd```

7. Generate sample Apache access log data

```ab -n 100 -c 10 http://localhost/```
