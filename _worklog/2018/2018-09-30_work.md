# 개발서버 구축

## vagrant


### mariadb

https://websiteforstudents.com/reset-mariadb-root-password-ubuntu-17-04-17-10/
https://websiteforstudents.com/mariadb-installed-without-password-prompts-for-root-on-ubuntu-17-10-18-04-beta/
https://mariadb.com/kb/en/library/create-user/
https://mariadb.com/kb/en/library/set-password/
https://brunch.co.kr/@artiveloper/21


### redis

protected mode?
이걸 끄는게 아니고
https://www.digitalocean.com/community/tutorials/how-to-secure-your-redis-installation-on-ubuntu-14-04
비밀번호를 사용하게 설정 해 놓으면 된다.

docker사용시에는 시작 파라미터에 넣어주고.
설치형으로 쓸 때는 설정파일 수정.
requirepass jorij03j09329j032

비밀번호 생성 

sudo systemctl restart redis.service



### rabbitmq

https://www.rabbitmq.com/rabbitmqctl.8.html

rabbitmqctl add_user root password


2018-09-30 15:09:33.249 DEBUG 8828 --- [   container-20] o.s.a.r.l.SimpleMessageListenerContainer : Consumer raised exception, processing can restart if the connection factory supports it

org.springframework.amqp.AmqpIOException: java.io.IOException
	at org.springframework.amqp.rabbit.support.RabbitExceptionTranslator.convertRabbitAccessException(RabbitExceptionTranslator.java:71) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:484) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.CachingConnectionFactory.createConnection(CachingConnectionFactory.java:628) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.ConnectionFactoryUtils.createConnection(ConnectionFactoryUtils.java:240) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.ConnectionFactoryUtils$1.createConnection(ConnectionFactoryUtils.java:106) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.ConnectionFactoryUtils.doGetTransactionalResourceHolder(ConnectionFactoryUtils.java:157) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.ConnectionFactoryUtils.getTransactionalResourceHolder(ConnectionFactoryUtils.java:92) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.ConnectionFactoryUtils.getTransactionalResourceHolder(ConnectionFactoryUtils.java:75) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.listener.BlockingQueueConsumer.start(BlockingQueueConsumer.java:566) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.listener.SimpleMessageListenerContainer$AsyncMessageProcessingConsumer.run(SimpleMessageListenerContainer.java:996) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_181-1-ojdkbuild]
Caused by: java.io.IOException: null
	at com.rabbitmq.client.impl.AMQChannel.wrap(AMQChannel.java:126) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel.wrap(AMQChannel.java:122) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel.exnWrappingRpc(AMQChannel.java:144) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQConnection.start(AMQConnection.java:401) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1104) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1054) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:994) ~[amqp-client-5.4.1.jar:5.4.1]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:457) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	... 9 common frames omitted
Caused by: com.rabbitmq.client.ShutdownSignalException: connection error; protocol method: #method<connection.close>(reply-code=530, reply-text=NOT_ALLOWED - access to vhost '/' refused for user 'root', class-id=10, method-id=40)
	at com.rabbitmq.utility.ValueOrException.getValue(ValueOrException.java:66) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.utility.BlockingValueOrException.uninterruptibleGetValue(BlockingValueOrException.java:36) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel$BlockingRpcContinuation.getReply(AMQChannel.java:494) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel.privateRpc(AMQChannel.java:288) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel.exnWrappingRpc(AMQChannel.java:138) ~[amqp-client-5.4.1.jar:5.4.1]
	... 14 common frames omitted

2018-09-30 15:09:33.249  INFO 8828 --- [   container-20] o.s.a.r.l.SimpleMessageListenerContainer : Restarting Consumer@2d7a4cf: tags=[{}], channel=null, acknowledgeMode=AUTO local queue size=0
2018-09-30 15:09:33.250 DEBUG 8828 --- [   container-20] o.s.a.r.listener.BlockingQueueConsumer   : Closing Rabbit Channel: null
2018-09-30 15:09:33.250 DEBUG 8828 --- [   container-21] o.s.b.f.s.DefaultListableBeanFactory     : Returning cached instance of singleton bean 'queue'
2018-09-30 15:09:33.250  INFO 8828 --- [   container-21] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [192.168.56.101:5672]
2018-09-30 15:09:33.363 ERROR 8828 --- [   container-21] o.s.a.r.l.SimpleMessageListenerContainer : Failed to check/redeclare auto-delete queue(s).

org.springframework.amqp.AmqpIOException: java.io.IOException
	at org.springframework.amqp.rabbit.support.RabbitExceptionTranslator.convertRabbitAccessException(RabbitExceptionTranslator.java:71) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:484) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.CachingConnectionFactory.createConnection(CachingConnectionFactory.java:628) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.connection.ConnectionFactoryUtils.createConnection(ConnectionFactoryUtils.java:240) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.doExecute(RabbitTemplate.java:1816) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.execute(RabbitTemplate.java:1790) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitTemplate.execute(RabbitTemplate.java:1771) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.core.RabbitAdmin.getQueueProperties(RabbitAdmin.java:345) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.listener.AbstractMessageListenerContainer.redeclareElementsIfNecessary(AbstractMessageListenerContainer.java:1604) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at org.springframework.amqp.rabbit.listener.SimpleMessageListenerContainer$AsyncMessageProcessingConsumer.run(SimpleMessageListenerContainer.java:995) [spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_181-1-ojdkbuild]
Caused by: java.io.IOException: null
	at com.rabbitmq.client.impl.AMQChannel.wrap(AMQChannel.java:126) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel.wrap(AMQChannel.java:122) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel.exnWrappingRpc(AMQChannel.java:144) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQConnection.start(AMQConnection.java:401) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1104) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:1054) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.ConnectionFactory.newConnection(ConnectionFactory.java:994) ~[amqp-client-5.4.1.jar:5.4.1]
	at org.springframework.amqp.rabbit.connection.AbstractConnectionFactory.createBareConnection(AbstractConnectionFactory.java:457) ~[spring-rabbit-2.0.6.RELEASE.jar:2.0.6.RELEASE]
	... 9 common frames omitted
Caused by: com.rabbitmq.client.ShutdownSignalException: connection error; protocol method: #method<connection.close>(reply-code=530, reply-text=NOT_ALLOWED - access to vhost '/' refused for user 'root', class-id=10, method-id=40)
	at com.rabbitmq.utility.ValueOrException.getValue(ValueOrException.java:66) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.utility.BlockingValueOrException.uninterruptibleGetValue(BlockingValueOrException.java:36) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel$BlockingRpcContinuation.getReply(AMQChannel.java:494) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel.privateRpc(AMQChannel.java:288) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQChannel.exnWrappingRpc(AMQChannel.java:138) ~[amqp-client-5.4.1.jar:5.4.1]
	... 14 common frames omitted

2018-09-30 15:09:33.363 DEBUG 8828 --- [   container-21] o.s.a.r.listener.BlockingQueueConsumer   : Starting consumer Consumer@33e3ede9: tags=[{}], channel=null, acknowledgeMode=AUTO local queue size=0
2018-09-30 15:09:33.363 ERROR 8828 --- [168.56.101:5672] c.r.c.impl.ForgivingExceptionHandler     : An unexpected connection driver error occured

java.net.SocketException: socket closed
	at java.net.SocketInputStream.socketRead0(Native Method) ~[na:1.8.0_181-1-ojdkbuild]
	at java.net.SocketInputStream.socketRead(SocketInputStream.java:116) ~[na:1.8.0_181-1-ojdkbuild]
	at java.net.SocketInputStream.read(SocketInputStream.java:171) ~[na:1.8.0_181-1-ojdkbuild]
	at java.net.SocketInputStream.read(SocketInputStream.java:141) ~[na:1.8.0_181-1-ojdkbuild]
	at java.io.BufferedInputStream.fill(BufferedInputStream.java:246) ~[na:1.8.0_181-1-ojdkbuild]
	at java.io.BufferedInputStream.read(BufferedInputStream.java:265) ~[na:1.8.0_181-1-ojdkbuild]
	at java.io.DataInputStream.readUnsignedByte(DataInputStream.java:288) ~[na:1.8.0_181-1-ojdkbuild]
	at com.rabbitmq.client.impl.Frame.readFrom(Frame.java:91) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.SocketFrameHandler.readFrame(SocketFrameHandler.java:164) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQConnection$MainLoop.run(AMQConnection.java:596) ~[amqp-client-5.4.1.jar:5.4.1]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_181-1-ojdkbuild]

2018-09-30 15:09:33.364  INFO 8828 --- [   container-21] o.s.a.r.c.CachingConnectionFactory       : Attempting to connect to: [192.168.56.101:5672]
2018-09-30 15:09:33.478 DEBUG 8828 --- [   container-21] o.s.a.r.l.SimpleMessageListenerContainer : Recovering consumer in 5000 ms.
2018-09-30 15:09:33.478 ERROR 8828 --- [168.56.101:5672] c.r.c.impl.ForgivingExceptionHandler     : An unexpected connection driver error occured

java.net.SocketException: Socket Closed
	at java.net.SocketInputStream.socketRead0(Native Method) ~[na:1.8.0_181-1-ojdkbuild]
	at java.net.SocketInputStream.socketRead(SocketInputStream.java:116) ~[na:1.8.0_181-1-ojdkbuild]
	at java.net.SocketInputStream.read(SocketInputStream.java:171) ~[na:1.8.0_181-1-ojdkbuild]
	at java.net.SocketInputStream.read(SocketInputStream.java:141) ~[na:1.8.0_181-1-ojdkbuild]
	at java.io.BufferedInputStream.fill(BufferedInputStream.java:246) ~[na:1.8.0_181-1-ojdkbuild]
	at java.io.BufferedInputStream.read(BufferedInputStream.java:265) ~[na:1.8.0_181-1-ojdkbuild]
	at java.io.DataInputStream.readUnsignedByte(DataInputStream.java:288) ~[na:1.8.0_181-1-ojdkbuild]
	at com.rabbitmq.client.impl.Frame.readFrom(Frame.java:91) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.SocketFrameHandler.readFrame(SocketFrameHandler.java:164) ~[amqp-client-5.4.1.jar:5.4.1]
	at com.rabbitmq.client.impl.AMQConnection$MainLoop.run(AMQConnection.java:596) ~[amqp-client-5.4.1.jar:5.4.1]
	at java.lang.Thread.run(Thread.java:748) [na:1.8.0_181-1-ojdkbuild]


https://stackoverflow.com/questions/17054533/allowing-rabbitmq-server-connections


set_permissions [-p vhostpath] {user} {conf} {write} {read}

rabbitmqctl set_permissions -p /myvhost guest ".*" ".*" ".*"