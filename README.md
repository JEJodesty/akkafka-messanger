# AkKafka Messenger
Developing a peer-to-peer messaging solution on a Kafka cluster for distributed message stream processing and message broadcasting. The current state of this solution includes a Akka HTTP / Apache Kafka Scala Server, Python Command Line Interface (CLI) chat clients, and Apache ZooKeepeer to launch multiple servers and manage distributed stream processing on computing clusters.
 
![Alt text](https://github.com/JEJodesty/akkafka-messager/blob/master/screenshots/AkKafka_demo.png?raw=true?raw=true "AkKafka Demo")


#### Step 1: Start Zookeeper, the Kafka Broker, and create Kafka Stream Topics
Before running the server and clients, run the following commands in separate CLIs from the base folder of your Kafka application, 
which in this case is ~/kafka_2.11-0.10.2.0.

This starts the Zookeeper at port 2181 and Kafka Broker at port 9092 
(which are the defaults and can be changed by editing the config files).

```shell
kafka_2.11-0.10.2.0$ bin/zookeeper-server-start.sh config/zookeeper.properties
kafka_2.11-0.10.2.0$ bin/kafka-server-start.sh config/server.properties
```

#### Step 2: Create the Topics needed for the application.
Run the following commands in separate CLIs from the base folder of your Kafka application

```shell
kafka_2.11-0.10.2.0$ bin/kafka-topics.sh --create --topic channelIn --replication-factor 1 --partitions 1 --zookeeper localhost:2181
kafka_2.11-0.10.2.0$ bin/kafka-topics.sh --create --topic channelOut --replication-factor 1 --partitions 1 --zookeeper localhost:2181
```

#### Step 3: Run Server
I had SBT / IntelliJ project issues when attempting to build a .jar
I must resolve these issues before I can give more simple running instructions.

In the meantime run it using IntelliJ IDEA 
#####(I've Also included screenshots of the UI).
* Clone this repository
```shel
git clone https://github.com/JEJodesty/akkafka-messager.git
```
* Download IntelliJ IDEA with the Scala Plugin. 
* Right click and Run the following Scala file.
```shell
src/main/scala/AkKafkaServer.scala
```
Output:
```sbtshell
Started server at 127.0.0.1:8080, press enter to kill server
```
#### Step 4: Run Multiple User Clients / Kafka Chat Log/Broadcaster
This is a CLI for multiple users to join a chat group.
Navigate to the project root directory and run the following (Python 2.7.12)
```shell
python clients/AkKafkaClient.py
``` 

This is a CLI for an administrator to monitor and broadcast messages to all users.
Navigate to the project root directory and run the following (Python 2.7.12)
```shell
python clients/KafkaBroadcastClient.py
``` 

##### To Do:
* Right now there is only a single group/channel called "chat" which is a bound endpoint. 
I will add more groups/channels/end points and include the ability for users to subscribe to channels.
* User Authentication.


