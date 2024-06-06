DROP
======================
>현재 테이블이 다른 테이블에 참조관계나 제약관계에 있다면 CASECADE CONSTRAINTS 옵션을 넣어 테이블 삭제
```sql
DROP TABLE 테이블 이름 [CASCADE CONSTRAINTS]

DROP TABLE EMP CASCADE CONSTRAINTS;
```