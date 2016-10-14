Confluent Platform Security Tools
=================================

This repo contains a tool that generates Kafka keystores and trust stores, along with a diagram that explains how keystores and trust stores can be deployed in Kafka.

Both the diagram and the script store the CA in the trust store. The trust store can be configured in other ways, for example, with multiple CAs, or with certificates instead of CAs. However, at this time, the diagram and the script don't address these additional configurations.


Format transformation
---------------------

JKS to cert
```
keytool -export -alias mydomain -file cert.crt -keystore store.jks
```

cert to PEM:
```
openssl x509 -inform DER -in cert.crt -out cert.pem
```

Get the key:
```
keytool -importkeystore -srckeystore store.jks -destkeystore store.p12 -deststoretype PKCS12
openssl pkcs12 -in store.p12  -nodes -nocerts -out private.key
```
