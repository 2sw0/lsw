테이블 및 데이터 복사
======================
## 1. 테이블 복사

### 1.1. 테이블 복사 (스키마 & 데이터)
```sql
CREATE TABLE 새로만들테이블명 AS
SELECT * FROM 복사할테이블명 [WHERE 절];
```

### 1.2. 테이블 구조만 복사
```sql
CREATE TABLE 새로만들테이블명 AS
SELECT * FROM 복사할테이블명 WHERE 1=2 [where절에 '참'이 아닌 조건을 넣어줌];
```

## 2. 데이터 복사

### 2.1. 테이블 생성되어 있고 데이터만 복사(데이터 구조 동일)
```sql
INSERT INTO 복사할테이블명 SELECT * FROM 테이블명 [WHERE 절];
```
### 2.2. 테이블 생성되어 있고 데이터만 복사(데이터 구조 다름)
```sql
INSERT INTO 복사할테이블명 (column1, column2, column3) SELECT column1, column2, column3 FROM 테이블명;
```