###### tags : `tutorial` `database`

# Tutorial MongoDB

## A. Database Method

### 1. General Method

| No  |       Method        |        Description         |
| :-: | :-----------------: | :------------------------: |
|  1  | `db.dropDatabase()` |      Delete database       |
|  2  |   `db.getName()`    |     Get database name      |
|  3  |   `db.hostInfo()`   | Get mongo host information |
|  4  |   `db.version()`    |     Get mongo version      |
|  5  |    `db.stats()`     |  Get mongo statistic info  |

### 2. Database Methods for Collection

| No  |            Method             |         Description          |  Alternate  |
| :-: | :---------------------------: | :--------------------------: | :---------: |
|  1  |   `db.getCollectionNames()`   |   Get all collection names   |      -      |
|  2  | `db.createCollection(<name>)` |   create <name> collection   |      -      |
|  3  |  `db.getCollection(<name>)`   | Get collection <name> object | `db.<name>` |
|  4  |   `db.getCollectionInfos()`   | Get info for all collection  |      -      |

## B. Collection Method

| No  |            Method             |              Description               |
| :-: | :---------------------------: | :------------------------------------: |
|  1  |   `db.<collection>.find()`    |      Get document in <collection>      |
|  2  |   `db.<collection>.count()`   | Get number of document in <collection> |
|  3  |   `db.<collection>.drop()`    |           Remove collection            |
|  4  | `db.<collection>.totalSize()` |          Get collection size           |
|  5  |   `db.<collection>.stats()`   |     Get collection statistic info      |

### 1. Insert Document

| No  |                      Method                       |                      Description                      |
| :-: | :-----------------------------------------------: | :---------------------------------------------------: |
|  1  |      `db.<collection>.insertOne(<document>)`      |          Insert <document> into <collection>          |
|  2  |    `db.<collection>.insertMany([<document>])`     | Insert more one document <document> into <collection> |
|  3  | `db.<collection>.insert(<document>/[<document>])` |    Insert one or more <document> into <collection>    |

#### example

```
// insert a document
db.players.insertOne({_id: 1, name: "Cristiano Ronaldo", club: ["Man United", "Real Madrid", "Juventus"]})

// insert documents
db.players.insertMany([
    {_id: 2, name: "Lionel Messi", club: ["Barcelona", "PSG"]},
    {_id: 3, name: "Ibrahimovic", club: ["AC Milan", "Barcelona", "PSG","MU"]},
])
```

### 2. Query Document

| No  |               Method               |          Description          |
| :-: | :--------------------------------: | :---------------------------: |
|  1  |  `db.<collection>.find(<query>)`   | Find all documents with query |
|  2  | `db.<collection>.findOne(<query>)` |  Find a document with query   |

##### Example

```
// Find a document where _id = 1
db.players.findOne({_id_: 1})

// Find documents where club = "PSG"
db.players.find({club: "PSG"})

// Find documents with embedded object
db.players.find({ "position.favorite": "CF" })
```

#### a. Query Operator

##### 1) Comparison Operator

| No  | Operator |       Description        |
| :-: | :------: | :----------------------: |
|  1  |  `$eq`   |          Equal           |
|  2  |  `$gt`   |       Greater than       |
|  3  |  `$gte`  |  Greater than or equal   |
|  4  |  `$lt`   |        Less than         |
|  5  |  `$lte`  |    Less than or equal    |
|  6  |  `$in`   | Comparing value in array |
|  7  |  `$nin`  |          Not in          |
|  8  |  `$ne`   |        Not Equal         |

Syntax :

```
db.<collection>.find({
    <field>: {
        <operator>: <value>
    }
})
```

###### Example

```
db.products.find({
    price: {
        $gte: 1000
    }
})

db.products.find({
    category: {
        $in : ["handphone", "laptop"]
    },
    price: {
        $lt: 10000000
    }
})
```

##### 2) Logical Operator

| No  | Operator |                Description                |
| :-: | :------: | :---------------------------------------: |
|  1  |  `$and`  |         Query dengan kondisi AND          |
|  2  |  `$or`   |          Query dengan kondisi OR          |
|  3  |  `$nor`  | Query dengan kondisi gagal di semua query |
|  4  |  `$not`  |      Query yang tidak sesuai kondisi      |

###### Syntax

```
// base syntax
db.<collection>.find(
    {} // logical operator
)

// and, or, nor
{
    $<operator>: [
        {
            // condition 1
        },
                {
            // condition 2
        },
        ...
    ]
}
// not
{
    <field>: {
        $not: {
            // condition
        }
    }
}
```

###### Example

```
db.products.find({
    $and: [
        {
            category: {
                $in: ["laptop", "handphone"]
            }
        },
        {
            price: {
                $gte: 5000000
            }
        }
    ]
})

db.products.find({
    category: {
        $not: {
            $in: ["laptop", "handphone"]
        }
    }
})
```

##### 3) Element Query Operator

| No  | Operator  |                      Description                      |                Value                |
| :-: | :-------: | :---------------------------------------------------: | :---------------------------------: |
|  1  | `$exists` |        Mencocokkan dokumen yang memiliki field        |             true/false              |
|  2  |  `$type`  | Mencocokkan dokumen yang memiliki type field tersebut | mongo type : string, int, long, ... |

###### Syntax

```
// Base Syntax
db.<collection>.find(
    {} // element operator
)

// $exists
{
    <field>: {
        $exists: <value>
    }
}

// $type
{
    <field>: {
        $type: <type>
    }
}

{
    <field>: {
        $type: [<type1>, <type2>, ..., <typen>]
    }
}

```

##### 4) Evaluation Operator

| No  |   Operator    | Description |                         Syntax                          |
| :-: | :-----------: | :---------: | :-----------------------------------------------------: |
|  1  |    `$expr`    |             |                                                         |
|  2  | `$jsonSchema` |             |                                                         |
|  3  |    `$mod`     |             |            `$mod: [<divisor>, <remainder>]`             |
|  4  |   `$regex`    |             |                    `$regex: /regex/`                    |
|  5  |    `$text`    |             | `$text: {$search: <string>, $caseSensitive: <boolean>}` |
|  6  |   `$where`    |             |                                                         |

##### 5) Array Operator

| No  |   Operator   |                         Description                         |
| :-: | :----------: | :---------------------------------------------------------: |
|  1  |    `$all`    |         Mencari dokumen dengan memenuhi semua array         |
|  2  | `$elemMatch` | Mencari dokumen dengan array yang memenuhi kondisi tertentu |
|  3  |   `$size`    |        Mencari dokumen dengan ukuran array tertentu         |

###### Syntax

```
// Base Syntax
db.<collection>.find(
    {} // Array Operator
)

// all
{
    <field>: {
        $all : ["value-1", "value-2", ..., "value-n"]
    }
}

// elemMatch
{
    <field>: {
        $elemMatch : {
            //query1
            //query2
        }
    }
}

// size
{
    <field>: {
        $size : <size>
    }
}
```

###### Example

```
db.players.find({
    position: {
        $all : ["CF", "LW"]
    }
})

db.players.find({
    position: {
        $elemMatch : {
            $in : ["CF", "LW"]
        }
    }
})

db.players.find({
    position: {
        $size: 3
    }
})
```

#### b. Projection Operator

=> Memilih field yang akan diambil/sembunyikan pada saat query dokumen

```
// Base Syntax
db.<collection>.find(
    {}, //query
    {} //projection
)

// Projection
{
    <field1>: 1, //include
    <field2>: 0, // exclude
}
```

| No  |   Operator   |                         Description                         |
| :-: | :----------: | :---------------------------------------------------------: |
|  1  |     `$`      |       Membatasi query hanya elemen pertama pada array       |
|  2  | `$elemMatch` | Membatasi elemen query array yang memenuhi kondisi tertentu |
|  3  |   `$meta`    |          Mengembalikan informasi metadata dokumen           |
|  4  |   `$slice`   |        Mengontrol jumlah data yang ditampilkan array        |

```
db.<collection>.find(
    {}, //query
    {}, //array projection
)

// $
{
    "<field>.$": 1
}

// $elemMatch
{
    <field> : {
        $elemMatch: {
            //query
        }
    }
}
// $slice
{
    <field> : {
        $slice: 2
    }
}
```

#### c. Query Modifier

=> Memodifikasi hasil query yang telah dilakukan
=> Modifikasi : mengubah jadi jumlah, membatasi banyak query dengan pagination, dsb

| No  |    Operator     |            Description            |
| :-: | :-------------: | :-------------------------------: |
|  1  |    `count()`    | Mengambil jumlah data hasil query |
|  2  | `limit(<size>)` |      Membatasi jumlah query       |
|  3  | `skip(<size>)`  | Mengabaikan n-data pertama query  |
|  4  | `sort(<query>)` |         Mengurutkan query         |

##### Example

```
db.players.find({}).count()
db.players.find({}).limit(5)
db.players.find({}).skip(10)

db.players.find({}).limit(5).skip(10)
db.players.find({}).skip(10).limit(5) // same result

db.players.find({}).sort({
    name: 1, //ascending
    age: -1 //descending
})

```

### 3. Update Document

| No  |    Operator    |    Description     |
| :-: | :------------: | :----------------: |
|  1  | `updateOne()`  | Update a document  |
|  2  | `updateMany()` |  Update documents  |
|  3  | `replaceOne()` | Replace a document |

##### Syntax

```
db.<collection>.<updateFunction>(
    {}, // filter
    {}, // update or replacement
    {} // option
)
```

##### Example

```
db.players.updateOne(
    {
        "name": "Lionel Messi"
    },
    {
        $set: {
            "rating": 96
        }
    },
)

db.players.updateMany(
    {},
    {
        $set: {
            "isRetired": false
        }
    },
)
```

#### a. Update Operator

| No  |    Operator    |                   Description                    |
| :-: | :------------: | :----------------------------------------------: |
|  1  |     `$set`     |               Mengubah nilai field               |
|  2  |    `$unset`    |                 Menghapus field                  |
|  3  |   `$rename`    |               Mengubah nama field                |
|  4  |     `$inc`     | Menambah/mengurangi nilai pada field tipe number |
|  5  | `$currentDate` |      Mengubah field menjadi waktu saat ini       |

##### Syntax

```
// Base Syntax
db.<collection>.<updateFunc>(
    {}, // query
    {} // update
)

// $set
{
    $set: {
        <field1>: <new_value1>
    }
}

// $unset
{
    $unset: {
        <field1>: "",
        <field2>: "",
        ...
    }
}

// $rename
{
    $rename: {
        <field1>: <newField1>,
    }
}

// $inc
{
    $inc: {
        <field1>: <incValue1>,
    }
}

// $currentDate
{
    $currentDate: {
        <field1>: {
            $type: "date" // "date" or "timestamp"
        },
    }
}
```

##### Example

```
//remove isRetired field
db.players.updateMany({},
    {
        $unset: {
            isRetired: ""
        }
    }
)

// change field "name" to "fullName"
db.players.updateMany(
    {},
    {
        $rename: {
            name: "fullName"
        }
    }
)
            
// change field child name
db.players.updateMany(
    {},
    {
        $rename: {
            "user.username": "user.name"
        }
    }
)


// increment age
db.players.updateMany(
    {},
    {
        $inc: {
            age: 1
        }
    }
)

// create lastUpdate with currentDate
db.players.updateMany({}, {
    $currentDate: {
        lastModified: {
            $type: "date"
        }
    }
})
```

#### b. Array Update Operator

| No  |     Operator      |                    Description                     |
| :-: | :---------------: | :------------------------------------------------: |
|  1  |        `$`        |           Mengubah elemen pertama array            |
|  2  |       `$[]`       |            Mengubah semua elemen array             |
|  3  | `$[<identifier>]` | Mengubah elemen array yang memenuhi kondisi filter |
|  4  |     `<index>`     |       Mengubah elemen array pada index ke-i        |

```
db.<collection>.updateMany(
    {},
    $operator: {
        // option 1
        "<field>.$": <value>
        // option 2
        "<field.$[]>": <value>
        // option 3
        "<field.[3]>": <value>
    }
)
```

```
db.products.updateOne({
    ratings: 3,
},
    {$set : {
        ratings.$: 5, // mengubah rating pertama menjadi 5
        // ratings.$[]: 5, //mengubah semua ratings menjadi 5
        // ratings.2 : 5 // mengubah rating pada index ke 2 menjadi 5
    }}
)
```

| No  |  Operator   |                        Description                         |
| :-: | :---------: | :--------------------------------------------------------: |
|  1  | `$addToSet` |         Menambahkan value ke array jika belum ada          |
|  2  |   `$pop`    | Menghapus elemen pertama (-1) atau terakhir (1) pada array |
|  3  |   `$pull`   |    Menghapus semua elemen di array yang sesuai kondisi     |
|  4  |   `$push`   |                Menambahkan elemen ke array                 |
|  5  | `$pullAll`  |              Menghapus semua elemen di array               |

##### Syntax

```
// Base Syntax
db.<collection>.updateOne(
    {},
    {
        $addToSet: {
            <field>: <value>
        }
    }
)

// $pop
{
    $pop: {
        <field>: <value> // -1 first element or 1 last element
    }
}

// $pull
{
    $pull: {
        <field>: {
            // operator condition
        }
    }
}

// $pullAll
{
    $pullAll: {
        <field>: ["value"]
    }
}
```

##### Example

```
// add "promo" to field tags if not exists
db.products.updateMany(
    {},
    {
        $addToSet: {
            tags: "promo"
        }
    }
)

// remove last element on field tags
db.products.updateMany(
    {},
    {
        $pop: {
            tags: 1
        }
    }
)

// remove product ratings if greater than 100
db.products.updateMany(
    {},
    {
        $pull: {
            ratings: {
                $gt:100
            }
        }
    }
)

// Add 100 to ratings both exists or not
db.products.updateMany(
    {},
    {
        $push: {
            ratings: 100
        }
    }
)

// Remove 100 in ratings
db.products.updateMany(
    {},
    {
        $pullAll: {
            ratings: [100]
        }
    }
)

```

### 4. Delete Document

| No  |              Function               |    Description    |
| :-: | :---------------------------------: | :---------------: |
|  1  | `db.<collection>.deleteOne(query)`  | Delete a document |
|  2  | `db.<collection.deleteMany(query)>` | Delete documents  |

##### Example

```
db.players.deleteOne({
    name: "spammer"
})

db.players.deleteMany({
    isRetired: true
})

db.players.deleteMany({
    name: {
        $regex: "spammer"
    }
})
```

### 5. Bulk Write Operator

Bulk Operation Method
| No | Function | Description |
| :-: | :---------------------------------: | :---------------: |
| 1 | `db.<collection>.insertMany()` | Insert documents |
| 2 | `db.<collection>.updateMany()` | Update documents|
| 3 | `db.<collection>.deleteMany()` | Delete documents |
| 4 | `db.<collection>.bulkWrite()` | Do multiple operation |

Bulk Write Operation

- insertOne
- updateOne
- updateMany
- replaceOne
- deleteOne
- deleteMany

Bulk Write Syntax

```
db.<collection>.bulkWrite({
    {},  // operation 1
    {},  // operation 2
    {}, // operation 3
    ...
})


// insertOne
{ insertOne : { "document" : <document> } }

// updateOne or updateMany
{
    updateOne :
        {
            "filter": <document>,
            "update": <document>
        }
}

// replaceOne
{
    replaceOne :
        {
            "filter" : <document>,
            "replacement" : <document>,
        }
}

// deleteOne or deleteMany
{
    deleteOne : {
        "filter" : <document>,
    }
}
```

##### Example

```
db.players.bulkWrite([
    {
        insertOne: {
            document: {
                _id: "eko",
                full_name: "Eko"
            }
        }
    },
    {
        insertOne: {
            document: {
                _id: "kurniawan",
                full_name: "Kurniawan"
            }
        }
    },
    {
        updateMany: {
            filter: {
                _id: {
                    $in: ["eko", "kurniawan", "khannedy"]
                }
            },
            update: {
                $set: {
                    full_name: "Eko Kurniawan Khannedy"
                }
            }
        }
    }
])
```

### 6. Schema Validation

```
// create collection and schema
db.createCollection(
    <collection>, {
    validator: {
        $jsonSchema: {} //json schema
    }
})

// create schema on existing collection
db.runCommand({
    collMod: <collection>,
    validationAction: "error",
    validator: {
        $jsonSchema: {} //json schema
    }
})
```

##### Example

```
db.createCollection("merchant", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["name", "category"],
      properties: {
        name: {
          bsonType: "string",
          description: "Must be a string",
        },
        category: {
          bsonType: "string",
          description: "Must be a string",
        },
        address: {
          bsonType: "object",
          required: ["city"],
          properties: {
            city: {
              bsonType: "string",
              description: "Must be a string",
            },
            address: {
              bsonType: "string",
              description: "Must be a string",
            },
          },
        },
      },
    },
  },
});

```
