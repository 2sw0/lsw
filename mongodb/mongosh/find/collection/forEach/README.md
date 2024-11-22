DB내 컬렉션 별 컬럼 조회

```
const dbName = "DB 이름";
const collections = db.getSiblingDB(dbName).getCollectionNames();

collections.forEach((collectionName) => {
    const fields = new Set();
    db[collectionName].find().forEach((doc) => {
        Object.keys(doc).forEach((key) => fields.add(key));
    });
    print(`Collection: ${collectionName}`);
    print(`Fields: ${Array.from(fields).join(", ")}`);
    print("-".repeat(40));
});
```

컬럼 한줄에 한개씩
```
const dbName = "DB 이름";
const collections = db.getSiblingDB(dbName).getCollectionNames();

collections.forEach((collectionName) => {
    const fields = new Set();
    db[collectionName].find().forEach((doc) => {
        Object.keys(doc).forEach((key) => fields.add(key));
    });
    print(`Collection: ${collectionName}`);
    print("-".repeat(40));
    Array.from(fields).forEach((field) => print(field));
    print("\n");
});
```
