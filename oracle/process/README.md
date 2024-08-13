현재 실행중인 프로세스 확인
```sql
SELECT a.sid,  a.serial#,  a.status, a.process, a.username, a.osuser, b.sql_text, c.program
  FROM v$session a, v$sqlarea b, v$process c
 WHERE a.sql_hash_value=b.hash_value
   AND a.sql_address=b.address
   AND a.paddr=c.addr
   AND a.status='ACTIVE';
```
