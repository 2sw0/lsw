CRONTAB
======================
## 1. 크론탭 설정

### 1.1. 현재 크론탭 출력
```
crontab -l
```

### 1.2. 크론탭 수정
```
crontab -e
```

### 1.3. 크론탭 삭제
```
crontab -r
```

## 2. 주기 결정
```
*　　　　　　*　　　　　　*　　　　　　*　　　　　　*
분(0-59)　　시간(0-23)　　일(1-31)　　월(1-12)　　　요일(0-7)
```

### 2.1. 매분 실행
```
# 매분 test.sh 실행
* * * * * /home/script/test.sh
```

### 2.2. 특정 시간 실행
```
# 매주 수요일 오후 2시 30분에 test.sh 를 실행
30 14 * * 3 /home/script/test.sh
```

### 2.3. 반복 실행
```
# 매일 매시간 0분, 20분, 40분에 test.sh 를 실행
0,20,40 * * * * /home/script/test.sh
```

### 2.4. 범위 실행
```
# 매일 1시 0분부터 30분까지 매분 tesh.sh 를 실행
0-30 1 * * * /home/script/test.sh
```

### 2.5. 범위 실행
```
# 매 10분마다 test.sh 를 실행
*/10 * * * * /home/script/test.sh
```

### 2.6. 응용
```
# 10일에서 12일까지 3시,4시에 매 10분마다 test.sh 를 실행
*/10 3,4 10-12 * * /home/script/test.sh
```

## 3. 주의사항

### 3.1. 한줄에 하나의 명령어 작성
```
# 잘못된 예
10 3 * * *
/home/script/test.sh

# 잘된 예
10 3 * * * /home/script/test.sh
```

## 4. 크론 로깅

### 4.1. 로그 갱신
```
* * * * * /home/script/test.sh > /home/script/test.sh.log 2>&1
```

### 4.2. 로그 누적
```
* * * * * /home/script/test.sh >> /home/script/test.sh.log 2>&1
```

### 4.3. 로그 필요없는 크론
```
* * * * * /home/script/test.sh > /dev/null 2>&1
```

## 5. 크론탭 백업

### 5.1. 백업 기본
```
crontab -l > /home/bak/crontab_bak.txt
```

### 5.2. 크론탭 백업 크론
```
30 15 * * * crontab -l > /home/bak/crontab_bak.txt
```
