# Database-Assignment_3

## Queries & Output

**1. How many Twitter users are in the database?**

```
pp(len(tweets.distinct('user')))
```
---
```
659774
```

**2. Which Twitter users link the most to other Twitter users? (Provide the top ten.)**

```
ppall(db.tweets.aggregate([
        {
        '$match': {
            'text': {
                '$regex': "@"
            }
        }
        },
        {
        '$group': {
            '_id': '$user',
            'count': {
                '$sum': 1
                }
        }
        },
        {
        '$sort': {
            'count': -1
        }
        },
        {
        '$limit': 10
        }
    ]))
```
---
```
lost_dog        — 549
tweetpet        — 310
VioletsCRUK     — 251
what_bugs_u     — 246
tsarnick        — 245
SallytheShizzle — 229
mcraddictal     — 217
Karen230683     — 216
keza34          — 211
TraceyHewins    — 202
```

**4.Who are the most active Twitter users (top ten)?**

```
ppall(db.tweets.aggregate([
        {
        '$group': {
            '_id': '$user',
            'count': {
                '$sum': 1
                }
        }
        },
        {
        '$sort': {
            'count': -1
        }
        },
        {
        '$limit': 10
        }
    ]))
```
---
```
lost_dog        — 549
webwoke         — 345
tweetpet        — 310
SallytheShizzle — 281
VioletsCRUK     — 279
mcraddictal     — 276
tsarnick        — 248
what_bugs_u     — 246
Karen230683     — 238
DarkPiano       — 236
```

**5. Who are the five most grumpy (most negative tweets) and the most happy (most positive tweets)? (Provide five users for each group)**

```
ppall(db.tweets.aggregate([
        {
        '$match': {
            'polarity': 0
        }
        },
        {
        '$group': {
            '_id': '$user',
        }
        },
        {
        '$sort': {
            'count': -1
        }
        },
        {
        '$limit': 5
        }
    ]))

ppall(db.tweets.aggregate([
        {
        '$match': {
            'polarity': 4
        }
        },
        {
        '$group': {
            '_id': '$user',
        }
        },
        {
        '$sort': {
            'count': -1
        }
        },
        {
        '$limit': 5
        }
    ]))
```
---
```
grumpy: lost_dog    – 549
        tweetpet    – 310
        webwoke     – 264
        mcraddictal – 210
        wowlew      – 210
            
happy:  what_bugs_u – 246
        DarkPiano   – 231
        VioletsCRUK – 218
        tsarnick    – 212
        keza34      – 211
```

## Modeling

I uploaded a word document with the table and brief arguments for each of the factors I deemed worthy