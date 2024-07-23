구성 파일 옵션
======================
> 프로세스가 운영체제에 요청할 수 있는 최대 Open 가능한 파일 개수(limit) 초과 시 발생

## 1. Configuration File
### 1.1. systemLog Options
* systemLog.logAppend
  ```
  Type: boolean
  Default: false
  When true, mongos or mongod appends new entries to the end of the existing log file when the instance restarts. Without this option, mongod or mongos backs up the existing log and create a new file.
  ```
* systemLog.logRotate
  ```
  Type: string
  Default: rename
  Determines the behavior for the logRotate command when rotating the server log and/or the audit log. Specify either rename or reopen : 
   rename : renames the log file.
   reopen : closes and reopens the log file following the typical Linux/Unix log rotate behavior. Use reopen when using the Linux/Unix logrotate utility to avoid log loss.
  If you specify reopen, you must also set systemLog.logAppend to true.
  ```
### 1.2. db.setProfilingLevel()
```
-- level 0 : 프로파일러가 꺼져 있고 데이터를 수집하지 않음 (기본 설정)
-- level 1 : slowms 값보다 오래 걸리거나 필터가 설정된 경우
-- level 2 : 모든 작업의 데이터를 수집
-- mongos에서는 프로파일링을 사용할 수 없기 때문에 db.setProfilingLevel()을 사용하여 0 이외의 값으로 설정할 수 없음

-- slowms : 기본값 100, 느린 작동 시간 임계값(밀리초 단위), 이 임계값보다 오래 실행되는 작업을 느린 것으로 간주
-- sampleRate : 기본값 1, 프로파일링하거나 기록해야 하는 저속 작업의 비율

ex)
db.setProfilingLevel(1, { slowms: 20, sampleRate: 0.42 })
```
### 1.3. logRotate
```
The logRotate command is an administrative command that allows you to rotate the MongoDB server log and/or audit log to prevent a single logfile from consuming too much disk space.
You must issue the logRotate command against the admin database.

ex)
db.adminCommand( { logRotate: 1 } )
db.adminCommand( { logRotate: "audit", comment: "Rotating audit log" } )
```

### 1.4. MongoDB LogLevel 변경
```
-- LogLevel : 1 ~ 5

> use admin
switched to db admin
> db.runCommand ({setParameter : 1, logLevel : 0})
{ "was" : 2, "ok" : 1 }
```