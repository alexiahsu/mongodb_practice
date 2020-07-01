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

# Find in a field that is an array
## e.g. find all listings that have "Hot Tub"
```
db.listingsAndReviews.find({
    'amenities': 'Cable TV'
}, {
    'name': 1,
    'amenities': 1
}).pretty()
```

# Find in a field that is an array, multiple segments
## e.g. find all listings that have wifi and laptop friendly workspace
```
db.listingsAndReviews.find({
    'amenities': {
        '$all': ['Wifi', 'Laptop friendly workspace']
    }
}, {
    'name': 1,
    'amenities': 1
}).pretty()
```

## e.g. find all listings that have doorman OR 'Host greets you'
```
db.listingsAndReviews.find({
    'amenities': {
        '$in': ['Doorman', 'Host greets you']
    }
}, {
    'name': 1,
    'amenities': 1,
}).pretty()
```

# Find all listings in Canada
```
db.listingsAndReviews.find({
    'address.country': 'Canada'
}, {
    'name': 1,
    'address.country': 1
}).pretty()
```

# Find all listings that are in Canada or in Brazel
```
db.listingsAndReviews.find({
    'address.country': {
        '$in': ['Canada', 'Brazil']
    }
}, {
    'name': 1,
    'address.country': 1
}).pretty()
```

# Find by one of the criteria:
## either listing is from Canada and have >= 5 bedrooms
## OR listing is in Brazil
```
db.listingsAndReviews.find({
    '$or': 
    [
        {
        'address.country': 'Canada', 
        'bedrooms': {
            '$gte': 3
        }
        },
        {
            'address.country': 'Brazil'
        }
    ]
}, {
    'name': 1,
    'bedrooms': 1,
    'address.country': 1
}).pretty()
```