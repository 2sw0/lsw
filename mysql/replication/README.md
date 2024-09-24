Replication 상태 확인

1. DB(root) 접속 후 확인

MariaDB [(none)]> show slave status\G;

 

2. DB 미 접속 상태에서 명령어로 확인

# mysql -uroot -p'패스워드' -e 'SHOW SLAVE STATUS \G'

# mysql -uroot -p'패스워드' -e 'SHOW SLAVE STATUS \G' | egrep "Master_Log_Pos|Running|IO_Err|SQL_Err|Seconds_Behind_Master"

           Read_Master_Log_Pos: 67320722

              Slave_IO_Running: Yes

             Slave_SQL_Running: Yes

           Exec_Master_Log_Pos: 67320722

         Seconds_Behind_Master: 0

                 Last_IO_Errno: 0

                 Last_IO_Error:

                Last_SQL_Errno: 0

                Last_SQL_Error:

       Slave_SQL_Running_State: Slave has read all relay log; waiting for the slave I/O thread to update it

 

3. 상태 값 내용

Read_Master_Log_Pos : Master DB로부터 mysql-bin 로그파일의 Read Posion 값

Exec_Master_Log_Pos : Slave DB에 저장된 Posion 값

 

Slave_IO_Running: IO 스레드가 - Master 연결 후 bin 로그 읽는지 여부 -> Master binlog 읽어서 자기거 relay 로그에 저장

Slave_SQL_Running: SQL 스레드가 - SLAVE 디스크에 저장되는 트랙잭션 여부

 

Seconds_Behind_Master : Master - Slave gap 차이 초단위로 표시

 

Master_Log_File : Master DB서버에 현재 생성 및 기록되고 있는 binary 로그파일

Relay_Log_File : Slave DB서버에 현재 생성 및 기록되고 있는 Relay 로그파일

 

Slave_IO_Running와 Slave_SQL_Running이 모두 Yes,

Read_Master_Log_Pos와 Exec_Master_Log_Pos 값이 일치,

Last_Errno는 0, Last_Error는 공란, Seconds_Behind_Master이 0이면 정상 복제중
