systemd
=======

centos 자동시작

```ini
[Unit]
Description=zookeeper-service
After=network.target

[Service]
Type=forking
User=root
Group=root
SyslogIdentifier=zookeeper-server
WorkingDirectory=/usr/local/zookeeper
Restart=always
RestartSec=0s
ExecStart=/usr/local/zookeeper/bin/zkServer.sh start
ExecStop=/usr/local/zookeeper/bin/zkServer.sh stop
```

systemctl daemon-reload
systemctl start zookeeper-server.servcie

stop
restart

enable
disable

status

