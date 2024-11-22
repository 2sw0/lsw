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

컬럼 및 데이터 타입까지
```
const dbName = "DB 이름";
const collections = db.getSiblingDB(dbName).getCollectionNames();

collections.forEach((collectionName) => {
    const fieldTypes = {};
    db[collectionName].find().forEach((doc) => {
        Object.keys(doc).forEach((field) => {
            const value = doc[field];
            const currentType = typeof value;
            if (fieldTypes[field]) {
                fieldTypes[field].add(currentType);
            } else {
                fieldTypes[field] = new Set([currentType]);
            }
        });
    });
    print(`Collection: ${collectionName}`);
    print("-".repeat(40));
    Object.keys(fieldTypes).forEach((field) => {
        const types = Array.from(fieldTypes[field]).join(", ");
        print(`${field}: ${types}`);
    });
    print("\n");
});
```
