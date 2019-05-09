# kafka

카프카 그냥 대충 쓰면 되는거 아니었나...
스펙이랑 아키텍처만 신경썼는데
설치에서 하루를 날릴 줄은 몰랐다.

## aws에서 비트나미 AMI로 설치 관련문서

https://docs.bitnami.com/aws/infrastructure/kafka/administration/run-producer-consumer/

https://cwiki.apache.org/confluence/display/KAFKA/KIP-103%3A+Separation+of+Internal+and+External+traffic

https://stackoverflow.com/questions/42998859/kafka-server-configuration-listeners-vs-advertised-listeners



## 문제점 해결순서

1. 리모트에서 접속이 안된다
2. 설정값을 바꿔줘야되는데...바꾸려고 보니
3. asws에서 비트나미로 설치한 경우 에러메세지가 잘 안나온다
4. 로컬에 vagrant로 설치해서
5. vagrant에서 pubsub 확인
6. host에서 vagrant로 pubsub 확인

그래서 결과...

원본파일
```
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#    http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# see kafka.server.KafkaConfig for additional details and defaults

############################# Server Basics #############################

# The id of the broker. This must be set to a unique integer for each broker.
broker.id=-1

############################# Socket Server Settings #############################

# The address the socket server listens on. It will get the value returned from 
# java.net.InetAddress.getCanonicalHostName() if not configured.
#   FORMAT:
listeners=SASL_PLAINTEXT://:9092
#   EXAMPLE:
#     listeners = PLAINTEXT://your.host.name:9092
#listeners=PLAINTEXT://:9092

# Hostname and port the broker will advertise to producers and consumers. If not set, 
# it uses the value for "listeners" if configured.  Otherwise, it will use the value
# returned from java.net.InetAddress.getCanonicalHostName().
advertised.listeners=SASL_PLAINTEXT://:9092

# Maps listener names to security protocols, the default is for them to be the same. See the config documentation for more details
listener.security.protocol.map=PLAINTEXT:PLAINTEXT,SSL:SSL,SASL_PLAINTEXT:SASL_PLAINTEXT,SASL_SSL:SASL_SSL

# The number of threads that the server uses for receiving requests from the network and sending responses to the network
num.network.threads=3

# The number of threads that the server uses for processing requests, which may include disk I/O
num.io.threads=8

# The send buffer (SO_SNDBUF) used by the socket server
socket.send.buffer.bytes=102400

# The receive buffer (SO_RCVBUF) used by the socket server
socket.receive.buffer.bytes=102400

# The maximum size of a request that the socket server will accept (protection against OOM)
socket.request.max.bytes=104857600


############################# Log Basics #############################

# A comma separated list of directories under which to store log files
log.dirs=/opt/bitnami/kafka/data

# The default number of log partitions per topic. More partitions allow greater
# parallelism for consumption, but this will also result in more files across
# the brokers.
num.partitions=1

# The number of threads per data directory to be used for log recovery at startup and flushing at shutdown.
# This value is recommended to be increased for installations with data dirs located in RAID array.
num.recovery.threads.per.data.dir=1

############################# Internal Topic Settings  #############################
# The replication factor for the group metadata internal topics "__consumer_offsets" and "__transaction_state"
# For anything other than development testing, a value greater than 1 is recommended for to ensure availability such as 3.
offsets.topic.replication.factor=1
transaction.state.log.replication.factor=1
transaction.state.log.min.isr=1

############################# Log Flush Policy #############################

# Messages are immediately written to the filesystem but by default we only fsync() to sync
# the OS cache lazily. The following configurations control the flush of data to disk.
# There are a few important trade-offs here:
#    1. Durability: Unflushed data may be lost if you are not using replication.
#    2. Latency: Very large flush intervals may lead to latency spikes when the flush does occur as there will be a lot of data to flush.
#    3. Throughput: The flush is generally the most expensive operation, and a small flush interval may lead to excessive seeks.
# The settings below allow one to configure the flush policy to flush data after a period of time or
# every N messages (or both). This can be done globally and overridden on a per-topic basis.

# The number of messages to accept before forcing a flush of data to disk
log.flush.interval.messages=10000

# The maximum amount of time a message can sit in a log before we force a flush
log.flush.interval.ms=1000

############################# Log Retention Policy #############################

# The following configurations control the disposal of log segments. The policy can
# be set to delete segments after a period of time, or after a given size has accumulated.
# A segment will be deleted whenever *either* of these criteria are met. Deletion always happens
# from the end of the log.

# The minimum age of a log file to be eligible for deletion due to age
log.retention.hours=168

# A size-based retention policy for logs. Segments are pruned from the log unless the remaining
# segments drop below log.retention.bytes. Functions independently of log.retention.hours.
log.retention.bytes=1073741824

# The maximum size of a log segment file. When this size is reached a new log segment will be created.
log.segment.bytes=1073741824

# The interval at which log segments are checked to see if they can be deleted according
# to the retention policies
log.retention.check.interval.ms=300000

############################# Zookeeper #############################

# Zookeeper connection string (see zookeeper docs for details).
# This is a comma separated host:port pairs, each corresponding to a zk
# server. e.g. "127.0.0.1:3000,127.0.0.1:3001,127.0.0.1:3002".
# You can also append an optional chroot string to the urls to specify the
# root directory for all kafka znodes.
zookeeper.connect=localhost:2181

# Timeout in ms for connecting to zookeeper
zookeeper.connection.timeout.ms=6000


############################# Group Coordinator Settings #############################

# The following configuration specifies the time, in milliseconds, that the GroupCoordinator will delay the initial consumer rebalance.
# The rebalance will be further delayed by the value of group.initial.rebalance.delay.ms as new members join the group, up to a maximum of max.poll.interval.ms.
# The default value for this is 3 seconds.
# We override this to 0 here as it makes for a better out-of-the-box experience for development and testing.
# However, in production environments the default value of 3 seconds is more suitable as this will help to avoid unnecessary, and potentially expensive, rebalances during application startup.
group.initial.rebalance.delay.ms=0
message.max.bytes: 1000012
delete.topic.enable: false
default.replication.factor: 1
sasl.mechanism.inter.broker.protocol=PLAIN

sasl.enabled.mechanisms=PLAIN

security.inter.broker.protocol=SASL_PLAINTEXT
```

변경포인트
```
# 기본값은 이렇게 돼 있다
listeners=SASL_PLAINTEXT://:9092
# 이건 접속한 사용자에게 브로커에 접속할 수있는 주소를 알려주는 건데... 왜 있는거지? 잘 이해가 안간다.
advertised.listeners=SASL_PLAINTEXT://:9092

# 브로커끼리 통신할 프로토콜을 여기서 정의 해줘야한다. PLAINTEXT로 바꾸거나 할거면 여기도 바꿔줘
security.inter.broker.protocol=SASL_PLAINTEXT
```

주의 및 변경포인트
```
# SASL은 로컬접속용으로 놔두고. 인증없이 사용가능한 PLAINTEXT를 추가했다.
listeners=SASL_PLAINTEXT://:9092,PLAINTEXT://:9093
# 위에서 추가하면 끝나는게 아니라 해당 프로토컬//포트로 접속한 사용자에게 이 카프카 서버의 주소를 알려주는 셋팅을 해줘야한다.
# 9092로 접속한 애들은 기본값인 localhost를 가져각고 9003접속한 애들은 54.180.146.111을 가져간다.
advertised.listeners=SASL_PLAINTEXT://:9092,PLAINTEXT://54.180.146.111:9093
```
