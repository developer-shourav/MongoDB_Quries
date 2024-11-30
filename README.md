## Most Useful MongoDB Queries


### `Insert`, `insertOne`, `find`, `findOne`, `field filtering`, `project` --`*Create and Read Operation*`

#### 1. `insert` 
`insert` using insert query we can add a single data to the MongoDB database . But now `insert` is deprecated.
Instead of `insert` we have to use `insertOne` query and for adding multiple data we can use `insertMany([])`

#### 2. `insertOne`
Using `insertOne` query we can add a new document to our Database. 

Example:

```js
db.test.insertOne({ name: 'shourav' , age: 23})

```

#### 3. `insertMany`
Using `insertMany` query we can add multiple document at a time in our DB. We have to insert data in an `array` formate in this query.

Example:
```js
db.test.insertMany([{name: 'Pallab Krishna Das', age:25}, {name: 'Ashim Krishna Das', age:22}])
```

#### 4. `find`
By using `find` query we can get all document of our Database. And you also can set finding rules here for getting data and getting 
specific parts of a document. 

Example:
```js
// To Get all data of a data collection of database 
db.test.find()

// To Get all data that match with the provided value / values
db.test.find({age: 23})

// To Get all data that match with the provided value / values and The document Field we want to get. (Field Filtering)
db.test.find({age: 23}, {name: 1, age: 1, email: 1, phone})


// 
```

#### 5. `findOne` --`*Read Operation*`
By using `findOne` query we can get one document form our DB that match with the provided document. 

Example: 
```js
// This query will find one document which age is 23
db.test.findOne({age: 23})

// This query will find one document with age is 23 and The document Field we want to get (Field Filtering)
db.test.findOne({age:23}, {name:1, age: 1})

```

#### 6. `field filtering` --`*Read Operation*`
When we explicitly define which field we need in the find request output it's called `field filtering`

Example: 
```js
// only give name, age and email filed form all fields
db.test.find({age: 17}, {name:1, age:1, email: 1})

// only give name, age filed form all fields
db.test.findOne({age:23}, {name:1, age: 1})

```

#### 7. `project` --`*Read Operation*`
We can use `project` method for field filtering in `find` query. `The project` does'nt work on `findOne` query

Example:
```js
// Field Filtering with project
db.test.find({gender: female}).project({name: 1, email: 1, gender: 1})
```


### `$eq`, `$ne`, `$gt`, `$lt`, `$gte`, `$lte` --`*Read Operation*`

#### 8. `$eq`
`$eq` is a comparison operator , it's means `$eq ---> equal to `. We can compare value using this operator. Which value is equal to this condition will be get.

Example:
```js
// This query will give only the document which age is equal to 12

db.test.find({age: {$eq: 12}}, {name: 1, gender: 1, age: 1})

```

#### 9. `$ne`
`$ne` is a comparison operator, it's means `$ne ---> not equal to`. We can compare value using this operator. Which value is not equal to this condition will be get/displayed or rendered. 

Example:
```js
// This query will give only the document which age is not equal to 12

db.test.find({age: {$ne: 12}}, {name: 1, gender: 1, age: 1})

```

#### 10. `gt`
`gt` means `greater than`. 

Example:
```js
// This query will give the document/documents which age is greater than 24
db.test.find({age: {$gt: 24}}, {name: 1, gender: 1, age: 1})

```

#### 11. `gte`
`gte` means `greater than equal` 

Example: 
```js
// This query will give the document / documents which age is greater then and equal 25
db.test.find({ age: {$gte: 25}}, {name:1, gender: 1, age: 1})

```
#### 12. `lt`
`lt` means `less than`. 

Example:
```js
// This query will give the document/documents which age is less than 24
db.test.find({age: {$lt: 24}}, {name: 1, gender: 1, age: 1})
```


#### 13. `lte`
`lte` means `less than equal` 

Example: 
```js
// This query will give the document / documents which age is less then and equal 25
db.test.find({ age: {$lte: 25}}, {name:1, gender: 1, age: 1})
```


### `$in`, `$nin`, `implicit and` condition --`*Read Operation*`

#### 14. `implicit and`

যখন আমরা একই field এর ভিতরে , coma ব্যবহার করে একাধিক condition / value add করা হয় তখন `implicit and` বলে ।

Example:
```js
// { $gte: 18, $lte: 30 } is implicit and
db.test.find({ age: { $gte: 18, $lte: 30 } }, { age: 1 })

// { gender: 'Female', age: { $gte: 18, $lte: 30 } } these gender and age also implicit and type
db.test.find({ gender: 'Female', age: { $gte: 18, $lte: 30 } })

```

#### 15. `sort`
Using `sort` query we can sort document based on a value. 

Example:
```js
// Here we are sorting data based on age
db.test.find({ age: { $gte: 18, $lte: 30 } }, { age: 1 }).sort({age:1})

```

#### 16. `in`
Using `in` operator we can get document if the any of the value of the filed `match` with value array. 

Example:
```js
// This is the example of `in` operator
db.test.find({ gender: "Female" , age: {$in : [18, 20, 22, 24, 26, 28, 30]} }, { age: 1, gender: 1})

```

#### 17. `nin`
Using `nin` operator we can get document if the any of the value of the filed `do not match` with value array. 

Example:
```js
// This is an example of `nin` operator
db.test.find({ gender: "Female" , age: {$nin : [18, 20, 22, 24, 26, 28, 30]} }, { age: 1, gender: 1})
```


### explicit `$and`, `$or` operator --`*Read Operation*`

#### 18. `$and`
যখন আমরা `$and` operator ব্যাবহার করে নিজে থেকে বলে দেই একাধিক condition / value হবে সেটাকে বলা হয় explicit and. 

Example:
```js
 // Explicit `$and` operator / সব গুলো ভ্যালু থাকতে হবে। 
 db.test.find({
     $and : [
     {gender: 'Female'},
     {age: {$ne: 15}},
     {age: {$lte: 30}}
     ]
     
 }).project({age: 1, gender:1,  email:1})
```

#### 19. `$or` 

`$or` operator ব্যাবহার করে বলে দেওয়া হয় যে কোন একটি Value থাকলেই document টি নিয়ে আসবে। 

Example:
```js
 // Explicit `$or` operator / যেকোন একটি value থাকলেই হবে। 
db.test.find({
    $or: [
     {"skills.name" : 'JAVASCRIPT'},
     {"skills.name" : 'PYTHON'}
     
    ]
    
}).project({age: 1, skills: 1}).sort({ age:1 })
   
```

#### 20. `implicit or` using `in` query

Example:
```js
 // Implicit or operator / যেকোন একটি value থাকলেই হবে। 
db.test.find({
    "skills.name": {$in: ['JAVASCRIPT', 'PYTHON']}
    
}).project({age: 1, skills: 1}).sort({ age:1 })
   
```

### `$exists`, `$type`, `$size` --`*Read Operation*`

#### 21. `$exists` 
কোন field সব গুলো document এর মধ্যে আছে কি না `$exists` ব্যাবহার করে আমরা দেখতে পারি । `$exists` এর value boolean
দিতে হয়। 

Example:
```js
// যে সব document এ age field আছে সেগুলো দেখাবে
db.test.find({age: {$exists: true}})

// যে সব document এ phone field নেই সেগুলো দেখাবে
db.test.find({phone: {$exists: false}}) 

/* Note: exists ব্যাবহার করলে field থাকলেই result এ document টা দেখাবে সেক্ষেত্র field এর value null, undefined, empty, empty string,
 empty array, empty object যাই হোক না কেন */
```

#### 22. `$type`
`$type` ব্যবহার করে field এর value type বলে দেওয়া হয়। Type মিলে গেলে সেই document টা দেখাবে। 


Example:
```js
db.test.find({friends: {$type: 'array'}}, {name: 1, age: 1})
```

#### 23. `$size`
`$size` is an array method. একটি array এর মধ্যে কত গুলো element আছে তা জানা যায় এই `$size` এর ব্যাবহার করে। 

Example:
```js
// size এর value যা দেওয়া হবে Query করে তত গুলো element ওয়ালা document গুলো নিয়ে আসবে। 
db.test.find({ friends: { $size: 4 } }).project({ friends: 1 })


```

### `array value`, `$all` , `$elemMatch` --`*Read Operation*`

#### 24. `array vale syntax` such as `arrayName: "value"`
For reading specific `array`  value we can use  `arrayName: "value"` syntax 

Example:
```js
// সব Document এর মধ্যে যে গুলোর interests array এর মধ্যে Cooking ভ্যালু আছে সব গুলো দেখাবে
db.test.find({interests: "Cooking"}).project({interests: 1})

```

#### 25. `array index syntax` such as `"arrayName.index": "value"`, `"friends.0": "Shourav"` , `"friends.2": "Niloy"` 

Example: 
```js
// এখানে যে সব document এর interests array এর 3rd index এর ভ্যালু "Cooking" সেগুলো দেখাবে। 
db.test.find({"interests.2": "Cooking"}).project({interests: 1})
```

#### 25. `array index and value exactly match` 

Example:
```js
// এখানে যে সব document এর interests array এর value [ "Gardening", "Gaming", "Cooking" ] সেগুলই দেখাবে
db.test.find({interests: [ "Gardening", "Gaming", "Cooking" ]}).project({interests: 1})

/* ----Note: এই Syntax এ শুধু ভ্যালু গুলো থাকলেই হবে না তাদের index ও একই হতে হবে। ------  */
```

#### 26. `$all` 
`$all` array query syntax accepts an array of value and It returns all the document matches the values

Example:
```js
/* 
এখানে যে সব document এর interests array এর value ["Gardening", "Gaming"] আছে সব গুলো দেখাবে
যদি কোন document এ  interests array এর value এর ২ টার বাইরে আরো থাকে তাহলেও দেখাবে। মূলত এই ২ টি থাকলেই হবে। 
Same to same match হতে হবে না। 
*/
db.test.find({ interests: {$all: ["Gardening", "Gaming"]}}).project({interests: 1})

```

#### 26. `$elemMatch` object syntax

`$elemMatch` Query ব্যাবহার করে object এর ভিতরে থেকে নির্দিষ্ট ভ্যালু আছে সে সব document বের করা যায়

Example: 
```js
db.test.find({skills: {$elemMatch: {name: "JAVASCRIPT", level: "Intermidiate"}}}, {skills: 1})

```


### `$set`, `$addToSet`, `each`, `$push` `*Update Operations*`

#### 27. `$set` 
`$set` using this query we can `update a document` value. But it has a problem , it works nicely in primitive data type 
but in the not primitive data type like `array` , `object` this query totally replace all values. We can use it in `array`
, `object` type for entirely change the object. 

Example:
```js
db.test.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000065") },
    { $set: {age: 99} } )

```

#### 28. `$addToSet`
Using `$addToSet` Query we can add an element or multiple element into an array of a document. It used for document update. 

Example:
```js
// Here Friends is an array , we are updating the document . adding `Krishna` to the friends array.
db.test.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000065") },
    {
        $addToSet: {
            friends: "Krishna"
        }
    }

)
```


#### 29. `$addToSet` and `$each` Queries
Using `$each` query with the `$addToSet` query we can add multiple elements in a array at a time. But it ignore the `duplicate value`. If an array element already exist and we want to add the same element using `$addToSet` then it will do not add again.   

Example: 
```js
(
    { _id: ObjectId("6406ad63fc13ae5a40000065") },
    {
        $addToSet: {
            friends: {$each: ['Krishna', 'Gouranggo', 'Nittanondo']}
        }
    }

)
```

#### 30. `$push`
Using `$push` we can do same operation like `$addToSet`. But there is more with `$push` , `$addToSet` doesn't allow 
adding duplicate element but using `$push` we can add same element multiple times in an array.

Example: 
```js
(
    { _id: ObjectId("6406ad63fc13ae5a40000065") },
    {
        $push: {
            friends: {$each: ['Krishna', 'Gouranggo', 'Nittanondo']}
        }
    }

)
```

### `$unset`, `$pop`, `$pull`, `$pullAll` --`*Delete Operations*`

#### 31. `$unset`
Using `$unset` query we can `delete / remove` property form document 

Example: 
```js
db.test.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000065") },
    { $unset: { age: 1 }}
    )

```

#### 32. `$pop`
Using `$pop` query we can remove array last and first element. 

Example:
```js
// For Removing Array Last Element
db.test.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000065") },
    { $pop: { skills: 1 }}
    )

// For Removing Array First Element

db.test.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000065") },
    { $unset: { skills: -1 } }
    )

```

#### 33. `$pull`
Using `$pull` query we can remove specific element of an array using it's value or condition

Example: 
```js
// For remove cooking from interests array "interests" : [ "Cooking" "Writing", "Reading" ]`
db.test.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000065") },
    { $pull: { interests: "Cooking" } }
)

// Array after pull: "interests" : [ "Writing", "Reading" ]
```

#### 34. `$pullAll`
Using `$pullAll` query we can remove multiple document from an array. 

Example: 
```js
db.test.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000065") },
    { $pullAll: { languages: ["Catalan", "German"] } }
)

// It will remove "Catalan", "German" element form languages array
```

###  More about `$set`, `set in object` --`*Update Operation*`

#### 35. `$set` for object and array of object
Using `$set` we can also update / Replace object and array of object's value 

Syntax: `arrayName.$.objectPropertyName`: `"newValue"`

*Note: [`$` symbol is mandator here. It grab the first match one.]*

Example:
```js
db.test.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000065"), "name.lastName": 'Datta' },
    { $set:{ "education.$.major": 'SSC'}}
    
)
```

#### 36. `$inc`

Using this query we can increase a number filed value

Example:
```js
db.test.updateOne(
    { _id: ObjectId("6406ad63fc13ae5a40000065"), "name.lastName": 'Datta'},
    {$inc: {age: 5}}
    )

// Now it will increase age 5 years
```

### `delete documents`, `drop collection`  --`*Delete Operation*`

#### 37. `deleteOne`
For deleting a document

Example:
```js
db.test.deleteOne({_id : ObjectId("6406ad64fc13ae5a4000008a"),})
```

#### 38. `delete collection`
For deleting a Data Base collection

Syntax: `db.<collectionName>.drop( { writeConcern: { w: 1 } } )`
Example:
```js
db.extraTest.drop( { writeConcern: { w: 1 } } )
```



