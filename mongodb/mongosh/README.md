MongoDB User
===

### 일반 유저 생성

MongoDB에서 일반 유저를 생성하기 위해선 특정 데이터베이스로 이동 후 생성해야 함.
```sh
# 인증 데이터베이스(authentication database)는 test
> use test
# testuser라는 유저를 생성
> db.createUser( { 
    user: "testuser", 
    pwd: "pwd123", 
    roles: [ "readWrite" ]
  }
)
Successfully added user: { "user" : "testuser", "roles" : [ "readWrite" ] }
```
인증 데이터베이스가 달라지면 다른 계정으로 인식이 되게 되기 때문에 tdb1, tdb2, tdb3 과 같은 데이터베이스 별로 동일한 이름의 유저를 생성할 수 있음.
\
(MongoDB에선 이름이 같더라도 서로 다른 계정으로 인식되어 3개의 계정으로 인식)
```sh
> use tdb1
> db.createUser( { 
    user: "testuser", 
    ...

> use tdb2
> db.createUser( { 
    user: "testuser", 
    ...


> use tdb3
> db.createUser( { 
    user: "testuser", 
    ...
```

### 생성한 데이터베이스 이외에 권한을 부여하여 다른 데이터베이스를 사용하는 방법

생성 시
```sh
> use tdb1
> db.createUser( { 
    user: "testuser", 
    pwd: "pwd123", 
    roles: [ "readWrite", {role:"read", db:"tdb2"} ]
  }
)
```

생성 후 권한 부여
```sh
> use tdb1
> db.createUser( { 
    user: "testuser2", 
    pwd: "pwd123", 
    roles: [ "readWrite" ]
  }
)
> db.grantRolesToUser("testuser2",[
    {role:"read", db:"tdb2"}
  ]
)
```

계정에 부여된 권한 확인
```sh
> db.getUsers()
```

인증 데이터베이스 관계 없이 admin으로 사용자 조회
```sh
> use admin
> db.system.users.find().pretty()
```
<br>
