TABLE
======================
## 1. Create table

### 1.1. 기본 양식
```
CREATE TABLE [스키마명].[테이블명]
(
  [컬럼명] [데이터 타입] [기본 값(생략가능)] [NULL(생략가능)]
) TABLESPACE [테이블스페이스명];
```

### 1.2. 기본키(Primary Key) 설정
> 해당 테이블에 있는 데이터를 식별하는 유일한 KEY에 해당하는 컬럼을 의미

#### 1.2.1 제약조건으로 추가
```
ALTER TABLE [테이블명] ADD CONSTRAINT [제약조건명] PRIMARY KEY([컬럼명]);

-- 예제 --
ALTER TABLE emp ADD CONSTRAINT emp_pk PRIMARY KEY(empno);
```

#### 1.2.2 테이블 생성 시 추가
```
-- 예제 --
CREATE TABLE emp 
( 
  empno       NUMBER(5)	  NOT NULL    primary key,
  name        VARCHAR2(20), 
  hiredate    DATE,
  salary      NUMBER(7,2)
) TABLESPACE tablespace_name;
   
OR

CREATE TABLE emp 
( 
  empno       NUMBER(5)	  NOT NULL,
  name        VARCHAR2(20),
  hiredate    DATE,
  salary      NUMBER(7,2)
  CONSTRAINTS emp_pk PRIMARY KEY(empno)
) TABLESPACE tablespace_name;
```

### 1.3. 외래키(Foreing Key) 설정
> 외래키의 경우 보통 자식 테이블에 많이 사용. 자식 테이블에 데이터가 있음에도 부모 테이블의 데이터를 지우고자 시도할 때 이를 방지하기 위한 목적으로 사용 
```
ALTER TABLE 테이블명
ADD CONSTRAINT 외래키이름 FOREIGN KEY(컬럼명)
REFERENCES 부모테이블 (부모테이블 컬럼명);

-- 예제 --
ALTER TABLE COMPANY_INFO
ADD CONSTRATINT EMP_FK FOREIGN KEY(EMP_SEQ)
REFERENCES TEMP (TEMP_SEQ);
```

### 1.4. 인덱스 생성
```
CREATE INDEX [스키마명].[인덱스명] ON [스키마명].[테이블명]([컬럼명]) TABLESPACE [테이블스페이스명];

-- 예제 --
CREATE INDEX emp_idx ON emp(name) TABLESPACE emp_tablespace;
CREATE UNIQUE INDEX emp_uk ON emp(emp_seq) TABLESPACE emp_tablespace;
```

### 1.5. 코멘트 생성
```
-- 테이블 코멘트
COMMENT ON TABLE [테이블명] IS '[코멘트]';

-- 컬럼 코멘트
COMMENT ON COLUMN [테이블명.컬럼명] IS '[코멘트]';

-- 예제 --
COMMENT ON TABLE emp IS '직원 테이블';
COMMENT ON COLUMN emp.name IS '직원이름';
```