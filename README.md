# Apache_Kafka

# Step 1: Download and extract Kafka

1. Download Kafka by running the command below:

```sh
wget https://archive.apache.org/dist/kafka/3.8.0/kafka_2.13-3.8.0.tgz
```

2. Extract Kafka from the zip file by running the command below

```sh
tar -xzf kafka_2.13-3.8.0.tgz
```

This command will create a new directory `kafka_2.13-3.8.0` in the current directory

# Step 2: Configure KRaft and start server

1. Navigate to the kafka_2.13-3.8.0 directory

```sh
cd kafka_2.13-3.8.0
```

2. Generate a cluster UUID that will uniquely identify the Kafka cluster

```sh
KAFKA_CLUSTER_ID="$(bin/kafka-storage.sh random-uuid)"
```

This cluster id will be used by the KRaft controller.

3. KRaft requires the log directories to be configured. Run the following command to configure the log directories passing the cluster ID.

```sh
bin/kafka-storage.sh format -t $KAFKA_CLUSTER_ID -c config/kraft/server.properties
```

4. Now that KRaft is configured, we can start the Kafka server by running the following command

```sh
bin/kafka-server-start.sh config/kraft/server.properties
```

sure that the Kafka server has started when the output displays messages like "Kafka Server started"

# Step 3: Create a topic and start producer

**We need to create a topic before we can start to post messages**

1. Start a new terminal and change to the kafka_2.13-3.8.0 directory.

```sh
cd kafka_2.13-3.8.0
```

2. To create a topic named news, run the command below

```sh
bin/kafka-topics.sh --create --topic news --bootstrap-server localhost:9092
```

You will see the message: ```Created topic news```

3. Need a producer to send messages to Kafka. Run the command below to start a producer

```sh
bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic news
```

4. After the producer starts, and you get the '>' prompt, type any text message and press enter. Or you can copy the text below and paste. The below text sends three messages to Kafka

```sh
Good morning
Good day
Enjoy the Kafka lab
```

# Step 4: Start Consumer

**We need a consumer to read messages from Kafka**

1. Start a new terminal and change to the kafka_2.13-3.8.0 directory.

```sh
cd kafka_2.13-3.8.0
```

2. Run the command below to listen to the messages in the topic news

```sh
bin/kafka-console-consumer.sh   --bootstrap-server localhost:9092   --topic news   --from-beginning
```

3. You should see all the messages you sent from the producer appear here.

4. You can go back to the producer terminal and type some more messages, one message per line, and you will see them appear here
