---
title: Integrate Apache kafka on Confluent Cloud with Service Connector
description: Integrate Apache kafka on Confluent Cloud into your application with Service Connector
author: maud-lv
ms.author: malev
ms.service: service-connector
ms.topic: how-to
ms.date: 11/07/2023
ms.custom: event-tier1-build-2022
---
# Integrate Apache Kafka on Confluent Cloud with Service Connector

This page shows supported authentication methods and clients to connect Apache Kafka on Confluent Cloud to other cloud services using Service Connector. You might still be able to connect to Apache Kafka on Confluent Cloud in other programming languages without using Service Connector. This page also shows default environment variable names and values (or Spring Boot configuration) you get when you create the service connection. 

## Supported compute services

- Azure App Service
- Azure Functions
- Azure Container Apps
- Azure Spring Apps

## Supported Authentication types and client types

Supported authentication and clients for App Service, Azure Functions, Container Apps and Azure Spring Apps:

| Client type        | System-assigned managed identity | User-assigned managed identity | Secret / connection string | Service principal |
|--------------------|----------------------------------|--------------------------------|----------------------------|-------------------|
| .NET               | No                               | No                             | Yes                        | No                |
| Java               | No                               | No                             | Yes                        | No                |
| Java - Spring Boot | No                               | No                             | Yes                        | No                |
| Node.js            | No                               | No                             | Yes                        | No                |
| Python             | No                               | No                             | Yes                        | No                |
| None               | No                               | No                             | Yes                        | No                |

## Default environment variable names or application properties

Use the connection details below to connect compute services to Kafka. For each example below, replace the placeholder texts `<server-name>`, `<Bootstrap-server-key>`, `<Bootstrap-server-secret>`, `<schema-registry-key>`, and `<schema-registry-secret>` with your server name, Bootstrap server key, Bootstrap server secret, schema registry key, and schema registry secret. For more information about naming conventions, check the [Service Connector internals](concept-service-connector-internals.md#configuration-naming-convention) article. Refer to [Kafka Client Examples](https://docs.confluent.io/cloud/current/client-apps/examples.html#) to build Kafka client applications on Confluent Cloud.

### Secret / Connection String

#### SpringBoot client type

| Default environment variable name                            | Description                              | Example value                                                                                                                                |
| ------------------------------------------------------------ | ---------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| spring.kafka.properties.bootstrap.servers                    | Your Kafka bootstrap server              | `pkc-<server-name>.eastus.azure.confluent.cloud:9092`                                                                                      |
| spring.kafka.properties.sasl.jaas.config                     | Your Kafka SASL configuration            | `org.apache.kafka.common.security.plain.PlainLoginModule required username='<Bootstrap-server-key>' password='<Bootstrap-server-secret>';` |
| spring.kafka.properties.schema.registry.url                  | Your Confluent registry URL              | `https://psrc-<server-name>.westus2.azure.confluent.cloud`                                                                                 |
| spring.kafka.properties.schema.registry.basic.auth.user.info | Your Confluent registry user information | `<schema-registry-key>:<schema-registry-secret>`                                                                                           |

#### Other client types

| Default environment variable name           | Description                              | Example value                                                                                                                              |
|---------------------------------------------|------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------|
| AZURE_CONFLUENTCLOUDKAFKA_BOOTSTRAPSERVER   | Your Kafka bootstrap server              | `pkc-<server-name>.eastus.azure.confluent.cloud:9092`                                                                                      |
| AZURE_CONFLUENTCLOUDKAFKA_KAFKASASLCONFIG   | Your Kafka SASL configuration            | `org.apache.kafka.common.security.plain.PlainLoginModule required username='<Bootstrap-server-key>' password='<Bootstrap-server-secret>';` |
| AZURE_CONFLUENTCLOUDSCHEMAREGISTRY_URL      | Your Confluent registry URL              | `https://psrc-<server-name>.westus2.azure.confluent.cloud`                                                                                 |
| AZURE_CONFLUENTCLOUDSCHEMAREGISTRY_USERINFO | Your Confluent registry user information | `<schema-registry-key>:<schema-registry-secret>`                                                                                           |

## Next steps

Follow the tutorials listed below to learn more about Service Connector.

> [!div class="nextstepaction"]
> [Learn about Service Connector concepts](./concept-service-connector-internals.md)
