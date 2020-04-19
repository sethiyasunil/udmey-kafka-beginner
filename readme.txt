set KAFKA_HOME=D:\snl\kafka\confluent-5.4.1

%KAFKA_HOME%\bin\windows\zookeeper-server-start.bat %KAFKA_HOME%\etc\kafka\zookeeper.properties
%KAFKA_HOME%\bin\windows\kafka-server-start.bat %KAFKA_HOME%\etc\kafka\server.properties


#### producer consumer example
# https://www.tutorialkart.com/apache-kafka/kafka-console-producer-and-consumer-example/
%KAFKA_HOME%\bin\windows\kafka-topics.bat --create --topic test --partitions 5 --replication-factor 3 --bootstrap-server localhost:9092

%KAFKA_HOME%\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic  test1
%KAFKA_HOME%\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic test1 --from-beginning

### 
%KAFKA_HOME%\bin\windows\kafka-topics.bat --describe --topic test1 --bootstrap-server localhost:9092

### connector
%KAFKA_HOME%\bin\windows\connect-standalone.bat %KAFKA_HOME%\etc\kafka\connect-standalone.properties %KAFKA_HOME%\etc\kafka\connect-file-source.properties etc\kafka\connect-file-sink.properties

###run a java program
mvn -q clean compile exec:java -Dexec.mainClass="guru.learningjournal.kafka.examples.HelloProducer"


### consumer-group
%KAFKA_HOME%\bin\windows\kafka-topics.bat --create --topic stock-ticks --partitions 3 --replication-factor 1 --bootstrap-server localhost:9092
%KAFKA_HOME%\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic stock-ticks --from-beginning --group stock-ticks-group
%KAFKA_HOME%\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic stock-ticks --from-beginning --group stock-ticks-group
%KAFKA_HOME%\bin\windows\kafka-dump-log.bat --files D:\tmp\kafka-logs-0\stock-ticks2-1\00000000000000000000.log
%KAFKA_HOME%\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic  stock-ticks

### Get last message
%KAFKA_HOME%\bin\windows\kafka-run-class.bat kafka.tools.GetOffsetShell --broker-list localhost:9092 --topic topic10 
%KAFKA_HOME%\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic testsegment --offset 10 --partition 0


###zookeeper shell
%KAFKA_HOME%\bin\windows\zookeeper-shell.bat localhost:2181
ls /
ls /brokers/ids



