# kafka-security
Enable Kafka Security

Sample Projet to run docker compose with zookeeper and kafka using SASL_SSL protocol and SCRAM-SHA-512 mechanism, then inject the configuration into existing spring boot application.



**Step 1:** <a href="https://docs.docker.com/desktop/install/mac-install/"> Install Docker Desktop on Mac </a>

**Step 2:** Create docker compose file (docker-compose.yml) and place it into root

**Step 3:** Create Configuration files, then place them into config directory
  * client.properties
  * kafka-jaas.conf
  * zoo-jaas.conf

**Step 4:** Create TrustStore and KeyStore and place them into certs directory
  * kafka.server.keystore.jks
  * kafka.server.truststore.jks
  * keystore_creds (containing the password of keystore)
  * truststore_creds (containing the password of truststore)
  * sslkey_creds (containing the password of SSL certificate)

**Step 5:** Startup zookeeper and kafka by running below command while in root directory
```
docker-compose up
```

Then check docker desktop, you will see below
<img width="1125" alt="image" src="https://github.com/tabuamireh/kafka-security/assets/39899733/984f3db8-d8c0-4797-9f43-fb522a59b822">


**Step 6:** Startup consumner Listener by run below command while in root directory

```
docker-compose exec kafka kafka-console-consumer --bootstrap-server <<BOOTSTRAP SERVER URL>> --topic <<TOPIC NAME>> --consumer.config <<CONFIG PATH>> --property <<SECURITY PROTOCOL>> --property <<MECHANISM>>
```

_Actual command_
```
docker-compose exec kafka kafka-console-consumer --bootstrap-server kafkajs:9095 --topic tariq-topic --consumer.config /opt/kafka/config/client.properties --property "security.protocol=SASL_SSL" --property "sasl.mechanism=SCRAM-SHA-512"
```



**Step 7:** Startup Producer by run below command while in root directory

```
docker-compose exec kafka kafka-console-producer --broker-list <<BOOTSTRAP SERVER URL>> --topic <<TOPIC NAME>> --producer.config <<CONFIG PATH>> --property <<SECURITY PROTOCOL>> --property <<MECHANISM>>
```
_Actual Command_
```
docker-compose exec kafka kafka-console-producer --broker-list kafkajs:9095 --topic tariq-topic --producer.config /opt/kafka/config/client.properties --property security.protocol=SASL_SSL --property sasl.mechanism=SCRAM-SHA-512
```

# Change on Application
### Change the configuration into your Springboot Application (this example ran on springboot version 2.7.2)

<img width="1053" alt="image" src="https://github.com/tabuamireh/kafka-security/assets/39899733/5e1bc101-248f-4749-ac4c-69c57494cce1">



