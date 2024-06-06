TOO MANY OPEN FILES
======================
> 프로세스가 운영체제에 요청할 수 있는 최대 Open 가능한 파일 개수(limit) 초과 시 발생

## 1. 계정 Limit 확인 및 변경
### 1.1. Limit의 경우 크게 Soft, Hard
* soft
  ```
  Non-root 계정에서도 설정 가능
  일시적으로 넘어도 경고 메일 정도만 보냄
  ```
* Hard
  ```
  Root 계정에서만 설정 가능
  절대 넘을 수 없음
  Too many open files가 계속 발생하고 기능이 멈추는 경우 hard limit을 넘었을 가능성이 큼
  ```
### 1.2. NOFILE Limit 확인
```
ulimit -Hn
ulimit -Sn
```
### 1.3. 영구적 open files 설정 : /etc/security/limits.conf 파일에 추가
```
#vi /etc/security/limits.conf

root hard nofile 500000
root soft nofile 500000
user1 hard nofile 500000 -> 특정 유저(user1) 계정에 지정
user1 soft nofile 500000 -> 특정 유저(user1) 계정에 지정
* hard nofile 500000 -> 모든 유저계정에 지정
* soft nofile 500000 -> 모든 유저계정에 지정
```

### 1.4. 일시적 open files 설정(즉시 적용)
```
# ulimit -n 500000
```

### 1.5. limit 값들 확인
```
# ulimit -a
```
****
## 2. ulimit 옵션
```
-a : 모든 제한 사항을 보여줌.
-c : 최대 코어 파일 사이즈
-d : 프로세스 데이터 세그먼트의 최대 크기
-f : shell에 의해 만들어질 수 있는 파일의 최대 크기
-s : 최대 스택 크기
-p : 파이프 크기
-n : 오픈 파일의 최대수
-u : 오픈파일의 최대수
-v : 최대 가상메모리의 양
-S : soft 한도
-H : hard 한도
```
****
## 3. 주의 사항
> 새로 설정한 limit 값(500000)이 system 전체 limit 보다 작아야함

### 3.1. system 전체 limit 확인 방법
```
cat /proc/sys/fs/file-max
```
****
## 4. 프로세스에 대한 limit 올리기
> 프로세스 limit의 경우 변경한 뒤 재시작을 하면 되지만 실시간 서비스 환경에서 프로세스 재시작이 안되는 때가 있다고 가정하에 필요

### 4.1. 해당 프로세스의 PID를 확인
```
ps -ef | grep [프로세스명]
```
### 4.2. PID를 기준으로 해당 프로세스의 limit을 확인
```
prlimit --nofile -output RESOURCE, SOFT, HARD --pid [PID 번호]
```
### 4.3. limit을 변경
```
prlimit --nofile=500000 --pid=[PID 번호]
```
