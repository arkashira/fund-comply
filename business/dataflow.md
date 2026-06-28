# Dataflow Architecture
## Overview
The fund-comply dataflow architecture is designed to streamline regulatory requirements and reduce operational inefficiencies for small and medium-sized investment funds. The system will ingest data from various external sources, process and transform it, store it securely, and provide query and serving capabilities to users.

## External Data Sources
* Regulatory databases (e.g. SEC, FINRA)
* Financial institutions' APIs (e.g. banking, trading platforms)
* User-inputted data (e.g. fund information, compliance reports)

## Ingestion Layer
```markdown
+---------------+
|  External   |
|  Data Sources  |
+---------------+
       |
       |
       v
+---------------+
|  API Gateway  |
|  (NGINX, AWS  |
|   API Gateway) |
+---------------+
       |
       |
       v
+---------------+
|  Message Queue |
|  (Apache Kafka, |
|   RabbitMQ)     |
+---------------+
```
* API Gateway (NGINX, AWS API Gateway): handles incoming API requests and routes them to the message queue
* Message Queue (Apache Kafka, RabbitMQ): buffers and prioritizes incoming data for processing

## Processing/Transform Layer
```markdown
+---------------+
|  Message Queue |
|  (Apache Kafka, |
|   RabbitMQ)     |
+---------------+
       |
       |
       v
+---------------+
|  Stream Processor|
|  (Apache Flink,  |
|   Apache Beam)   |
+---------------+
       |
       |
       v
+---------------+
|  Batch Processor |
|  (Apache Spark,  |
|   Apache Hadoop) |
+---------------+
```
* Stream Processor (Apache Flink, Apache Beam): processes real-time data streams and performs transformations
* Batch Processor (Apache Spark, Apache Hadoop): processes batch data and performs transformations

## Storage Tier
```markdown
+---------------+
|  Batch Processor |
|  (Apache Spark,  |
|   Apache Hadoop) |
+---------------+
       |
       |
       v
+---------------+
|  Data Warehouse  |
|  (Amazon Redshift,|
|   Google BigQuery) |
+---------------+
       |
       |
       v
+---------------+
|  NoSQL Database  |
|  (MongoDB, Apache |
|   Cassandra)     |
+---------------+
```
* Data Warehouse (Amazon Redshift, Google BigQuery): stores processed data for analytics and reporting
* NoSQL Database (MongoDB, Apache Cassandra): stores user-inputted data and metadata

## Query/Serving Layer
```markdown
+---------------+
|  Data Warehouse  |
|  (Amazon Redshift,|
|   Google BigQuery) |
+---------------+
       |
       |
       v
+---------------+
|  Query Engine    |
|  (Apache Presto,  |
|   Apache Hive)   |
+---------------+
       |
       |
       v
+---------------+
|  API Gateway     |
|  (NGINX, AWS API |
|   Gateway)      |
+---------------+
```
* Query Engine (Apache Presto, Apache Hive): executes queries on the data warehouse
* API Gateway (NGINX, AWS API Gateway): handles incoming API requests and routes them to the query engine

## Egress to User
```markdown
+---------------+
|  API Gateway     |
|  (NGINX, AWS API |
|   Gateway)      |
+---------------+
       |
       |
       v
+---------------+
|  User Interface  |
|  (Web Application,|
|   Mobile App)    |
+---------------+
```
* User Interface (Web Application, Mobile App): presents data to users and handles user input

## Auth Boundaries
* API Gateway: authenticates and authorizes incoming API requests
* User Interface: authenticates and authorizes user access to the system
* Data Warehouse: encrypts and access-controls stored data
* NoSQL Database: encrypts and access-controls stored data

Components per tier:
* External Data Sources:
	+ Regulatory databases
	+ Financial institutions' APIs
	+ User-inputted data
* Ingestion Layer:
	+ API Gateway
	+ Message Queue
* Processing/Transform Layer:
	+ Stream Processor
	+ Batch Processor
* Storage Tier:
	+ Data Warehouse
	+ NoSQL Database
* Query/Serving Layer:
	+ Query Engine
	+ API Gateway
* Egress to User:
	+ User Interface
* Auth Boundaries:
	+ API Gateway
	+ User Interface
	+ Data Warehouse
	+ NoSQL Database