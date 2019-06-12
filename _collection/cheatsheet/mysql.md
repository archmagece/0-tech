# mysql 사용법


## 사용자 관리


## connection

현재 열린 커넥션
show status where `variable_name` = 'Threads_connected';
show processlist;

가능한 커넥션 확인
show variables like 'max_connections';
최대 커넥션 늘리지
SET GLOBAL max_connections

vi /etc/my.cnf
max_connections = 250
