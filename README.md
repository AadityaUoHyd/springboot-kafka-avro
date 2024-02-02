# springboot-kafka-avro
we are integrating a producer and consumer against Kafka with Avro schemas and the Confluent Schema Registry. Suppose you need multiple POJO classes, and you don't
want to code again and again. It makes code resuable and flexible. It will maintain versions of code as well with backward compatibility.

Here We did this in a single application, but the producer and consumer could have been deployed in different applications and would have been able to have their own versions of the schemas, kept in sync via the registry. Ensure you have docker installed, we will use to spin 'Confluent Kafka'.

## Introduction
Apache Kafka is a messaging platform. With it, we can exchange data between different applications at scale.

Spring Cloud Stream is a framework for building message-driven applications. It can simplify the integration of Kafka into our services.

Conventionally, Kafka is used with the Avro message format, supported by a schema registry. In this tutorial, we’ll use the Confluent Schema Registry. We’ll try both Spring’s implementation of integration with the Confluent Schema Registry and also the Confluent native libraries.

## Confluent Schema Registry
Kafka represents all data as bytes, so it’s common to use an external schema and serialize and deserialize into bytes according to that schema. Rather than supply a copy of that schema with each message, which would be an expensive overhead, it’s also common to keep the schema in a registry and supply just an id with each message.

Confluent Schema Registry provides an easy way to store, retrieve and manage schemas. It exposes several useful RESTful APIs.

Schemata are stored by subject, and by default, the registry does a compatibility check before allowing a new schema to be uploaded against a subject.

Each producer will know the schema it’s producing with, and each consumer should be able to either consume data in ANY format or should have a specific schema it prefers to read in. The producer consults the registry to establish the correct ID to use when sending a message. The consumer uses the registry to fetch the sender’s schema. 

When the consumer knows both the sender’s schema and its own desired message format, the Avro library can convert the data into the consumer’s desired format.

## Apache Avro
Apache Avro is a data serialization system.

It uses a JSON structure to define the schema, providing for serialization between bytes and structured data.

One strength of Avro is its support for evolving messages written in one version of a schema into the format defined by a compatible alternative schema.

The Avro toolset is also able to generate classes to represent the data structures of these schemata, making it easy to serialize in and out of POJOs.

## Sources to learn from :
- https://www.baeldung.com/spring-cloud-stream-kafka-avro-confluent <br>
- https://medium.com/@sunilvb/spring-boot-kafka-schema-registry-c6e32485a7c8 <br>
- https://www.confluent.io/blog/schema-registry-avro-in-spring-boot-application-tutorial/
