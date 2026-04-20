# kasdb

`kasdb` is a simple and easy-to-use database library for Node.js.

## Installation

```bash
npm install @kasperenok/kasdb
```
## Usage

```javascript
const { DB } = require("@kasperenok/kasdb");
const db = new DB({ filename: "database/example", extension: ".db" });
```
## Functions
### Save Data to File
```javascript
db.saveData("money", { username: "example username", count: 0 });
```
### Get Data from File 

1. Get full data from file:
```javascript
const data = db.getData();
console.log(data.money.count);
```

2. Get data by key:
```javascript
const data = db.getData("money");
console.log(data.count);
```

## Event Handling with `on` Function
### Listen for Data Retrieval Event
```javascript
db.on("getData", (eventData) => {
  console.log(`Data retrieved from key ${eventData.key} in file ${eventData.filename}`);
});
```
Attributes in `eventData` for event `getData`:
- key
- data
- filename

### Listen for Data Save Event
```javascript
db.on("saveData", (eventData) => {
  console.log(`Data saved with key ${eventData.key} in file ${eventData.filename}`);
});
```
Attributes in `eventData` for event `saveData`:
- key
- value
- filename

---

## AsyncDB

`AsyncDB` has the same API as `DB`, but all methods are `async`.

```javascript
const { AsyncDB } = require("kasperdb");
const db = new AsyncDB({ filename: "database/example", extension: ".db" });
```

### Save Data
```javascript
await db.saveData("money", { username: "example", count: 0 });
```

### Get Full Data
```javascript
const data = await db.getData();
console.log(data.money.count);
```

### Get Data by Key
```javascript
const data = await db.getData("money");
console.log(data.count);
```

### Event Handling
Works the same as `DB`:
```javascript
db.on("getData", (e) => console.log(`Got key ${e.key} from ${e.filename}`));
db.on("saveData", (e) => console.log(`Saved key ${e.key} to ${e.filename}`));
```

---

## Dependencies
- [fs](https://nodejs.org/api/fs.html): File system module.
- [msgpack-lite](https://www.npmjs.com/package/msgpack-lite): MessagePack implementation for Node.js.