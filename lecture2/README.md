# MongoDB Shell basics

## Connect to a MongoDB instance

If you install MongoDB on your local machine without Docker, then simply type in terminal the following command (assuming that your run MongoDB on `localhost` on port `27017`)
```shell
mongosh
```

Docker-way:

```shell
docker-compose exec mongodb mongosh
```

If you run MongoDB on different host or port, then run the following command:


```shell
mongosh "mongodb://localhost:27017"
```

## Basic shell commands

```shell
help
```

```shell
use mydb
```

### Inserting

```javascript
db.movies.insertOne(
  {
    title: "The Favourite",
    genres: [ "Drama", "History" ],
    runtime: 121,
    rated: "R",
    year: 2018,
    directors: [ "Yorgos Lanthimos" ],
    cast: [ "Olivia Colman", "Emma Stone", "Rachel Weisz" ],
    type: "movie"
  }
)
```

```javascript
db.find()
```

```javascript
db.movies.insertMany([
   {
      title: "Jurassic World: Fallen Kingdom",
      genres: [ "Action", "Sci-Fi" ],
      runtime: 130,
      rated: "PG-13",
      year: 2018,
      directors: [ "J. A. Bayona" ],
      cast: [ "Chris Pratt", "Bryce Dallas Howard", "Rafe Spall" ],
      type: "movie"
    },
    {
      title: "Tag",
      genres: [ "Comedy", "Action" ],
      runtime: 105,
      rated: "R",
      year: 2018,
      directors: [ "Jeff Tomsic" ],
      cast: [ "Annabelle Wallis", "Jeremy Renner", "Jon Hamm" ],
      type: "movie"
    }
])
```

### Updating

`db.collection.updateOne({filter}, {update operator})`

```javascript
db.movies.updateOne( { title: "Tag" },
{
  $set: {
    plot: "One month every year, five highly competitive friends hit the ground running for a no-holds-barred game of tag"
  },
  { $currentDate: { lastUpdated: true } }
})
```

```javascript
db.listingsAndReviews.updateMany(
  { security_deposit: { $lt: 100 } },
  {
    $set: { security_deposit: 100, minimum_nights: 1 }
  }
)
```

```javascript
db.accounts.replaceOne(
  { account_id: 371138 },
  { account_id: 893421, limit: 5000, products: [ "Investment", "Brokerage" ] }
)
```

### Deleting

```javascript
db.movies.deleteMany({})
```

```javascript
db.movies.deleteOne( { cast: "Brad Pitt" } )
```

```shell
cat ./assets/netflix_titles.csv | mongoimport -c test -d test --type=csv --headerline
```

```shell
docker-compose exec mongodb mongoimport -c test -d test --type=csv --headerline --file=/assets/netflix_titles.csv
```

```shell
cat ./assets/YouTubeDataset_withChannelElapsed.json | docker-compose exec -T mongodb mongoimport -c test -d test_new --jsonArray
```

```shell
docker-compose exec mongodb mongoimport -c test -d test_new --jsonArray --file=/assets/YouTubeDataset_withChannelElapsed.json
```

```javascript
db.test.find().limit(1).skip(10)
```

```javascript
db.test.find().count()
```

## MongoDB Compass
