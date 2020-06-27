After we have `use` a database, there's a special variable available
The variable is called `db`

# Find documents
Show all documents in a collection (but only the first ten)
```
db.listingsAndReviews.find().limit(10)
```

Beautify the output with the `.pretty()` function
```
db.listingsAndReviews.find().pretty().limit(10)
```

```
db.listingsAndReviews.find({
    'beds':3
}).pretty().limit(10)
```

# With projections
```
db.listingsAndReviews.find({
    'beds':3
},{
    'name':1,
    'beds':1
}).pretty().limit(10)
```
# With more than one criteria (first part shows criteria, second part shows how many to show)
```
db.listingsAndReviews.find({
    'beds':3,
    'bedrooms':3
}, {
    'name':1,
    'beds':1,
    'bedrooms':1
}).pretty().limit(10)
```

# Get number of results (count)
```
db.listingsAndReviews.find({
    'beds':3,
    'bedrooms':3
}, {
    'name':1,
    'beds':1,
    'bedrooms':1
}).count()
```

# Comparison (greater than) vs $lt
```
db.listingsAndReviews.find({
    'beds': {
        '$gt': 4
    }
}, {
    'name':1,
    'beds':1
})
```

# Comparison (greater than or equal) vs $lte
```
db.listingsAndReviews.find({
    'beds': {
        '$gte': 4
    }
}, {
    'name':1,
    'beds':1
})
```

# Find by range (greater than or equal to 4 and lesser than or equal to 8)
db.listingsAndReviews.find({
    'beds': {
        '$gte': 4,
        '$lte': 8
    }
}, {
    'name':1,
    'beds':1
})