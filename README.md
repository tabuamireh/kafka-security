# kafka-security
Enable Kafka Security

Sample Projet to run docker compose with zookeeper and kafka using SASL_SSL protocol and SCRAM-SHA-512 mechanism, then inject the configuration into existing spring boot application.



**Step 1:** <a href="https://docs.docker.com/desktop/install/mac-install/"> Install Docker Desktop on Mac </a>

**Step 2:** Create docker compose file (docker-compose.yml) and pace it into root

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

