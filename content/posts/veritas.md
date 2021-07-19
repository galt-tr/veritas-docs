# Veritas API

## Receipts

Veritas Receipts are used as a unique object issued to the purchaser that can be linked at a later time to a review. The receipt is encrypted onto the blockchain and is only visible to the issuers of the receipt. Issuers can also lock up redeemable rewards into the receipt, allowing reviewers to redeem the reward upon leaving a verified review.

### Issue Receipt

`[POST] /api/receipt`

Request Body:
```
NOTE: id is Google Place ID. Optional in the request, but if not included then placeMeta must contain data.
NOTE: meta is entirely extensible
{
  "id": "ChIJBY0_1XBTBogRonhPkB-U82w",
  "customerId": "barpay",
  "placeMeta": {
      "address": "368 College Ave, Clemson, SC 29631",
      "name": "Tiger Town Tavern",
      "phone": "(864) 654-5901"
  },
  "email": "connor@britevue.com",
  "meta": {
      "food": "salad",
      "drink": "heineken",
      "server": "Ashley",
      "total": "$15.25",
      "totalTip": "$20.25"
  },
  "reward": {
      "type": "BSV",
      "amount": "100"
  }
}
```

Response:
```
{
  "receiptID": "c859b888d3e20a2d6132cbdb732617e1a2701e7bb63029d752a0a6c1d35beba2",
  "receiptSecret": "c4ab3985ab32ef3e34ee5",
  "url": "https://britevue.com/new-review?customer=barpay&place-id=ChIJBY0_1XBTBogRonhPkB-U82w&receipt-id=c859b888d3e20a2d6132cbdb732617e1a2701e7bb63029d752a0a6c1d35beba2&receipt-secret=c4ab3985ab32ef3e34ee5"
}
```

### Get Receipt Info

`[GET] /api/receipt/<id>`

Response:
```
{
  "id": "12345", 
  "email": "connor@britevue.com",
  "meta": {
      "food": "salad",
      "drink": "heineken",
      "server": "Ashley",
      "total": "$15.25",
      "totalTip": "$20.25"
  },
  "reward": {
      "type": "BSV",
      "amount": "100"
  },
  "hashedSecret": "ccc5c62a6488de5cced457f5efb7e456"
}
```

### Get Receipts for Place

`[GET] /api/receipts?filter=place&id=ChIJBY0_1XBTBogRonhPkB-U82w`

Response:

```
[
  {
    "id": "ChIJBY0_1XBTBogRonhPkB-U82w", 
    "email": "connor@britevue.com",
    "meta": {
        "food": "salad",
        "drink": "heineken",
        "server": "Ashley",
        "total": "$15.25",
        "totalTip": "$20.25"
    },
    "reward": {
        "type": "BSV",
        "amount": "100"
    },
    "hashedSecret": "ccc5c62a6488de5cced457f5efb7e456"
  },
  {
    "id": "12345", 
    "email": "connor@britevue.com",
    "meta": {
        "food": "salad",
        "drink": "heineken",
        "server": "Ashley",
        "total": "$15.25",
        "totalTip": "$20.25"
    },
    "reward": {
        "type": "BSV",
        "amount": "100"
  },
  "hashedSecret": "ccc5c62a6488de5cced457f5efb7e456"
  }
]
```

## Reviews

Reviews submitted through Veritas are automatically added to Britevue and distinguished as a Verified Review. If the receipt contains an issued reward, the reward is issued to the user and is redeemed when the user signs up for an account on Britevue. If the email is already linked to a Britevue account, then the reward is sent directly to the Handcash wallet associated with the user. 

### Submit Review


`[POST] /api/veritas`

Request Body:
```
{
  "receiptID": "c859b888d3e20a2d6132cbdb732617e1a2701e7bb63029d752a0a6c1d35beba2",
  "receiptSecret: "c4ab3985ab32ef3e34ee5",
  "review": "I loved it! This is an incredible place to get drinks, and Ashley was terrific!",
  "ratings": {
    "quality": 4.5,
    "experience": 3.0,
    "value": 4.5
  }
}
```

Response:
```
NOTE: If token has an unlockable reward, the reward is issued to the user
NOTE: rewardID and rewardSecret are optional
{
  "reviewID": "f31bfd0b8bdd25bfe0dcbc62aea3ef45c0dcaa815832fb75b7d58c187645d067",
  "rewardID": "c859b888d3e20a2d6132cbdb732617e1a2701e7bb63029d752a0a6c1d35beba2",
  "rewardSecret": "c4ab3985ab32ef3e34ee5"
}
```

## Rewards

Rewards issued through Veritas are issued directly to the user if there is a Britevue account associated with the email address in the receipt/review, or they are issued and redeemable via a unique URL that is used when signing up for Britevue.

### Redeem Reward
`[POST] /api/reward`

Request Body:
```
{
  "rewardID": "c859b888d3e20a2d6132cbdb732617e1a2701e7bb63029d752a0a6c1d35beba2",
  "rewardSecret": "c4ab3985ab32ef3e34ee5",
  "url": "https://britevue.com/sign-up?reward-id=c859b888d3e20a2d6132cbdb732617e1a2701e7bb63029d752a0a6c1d35beba2&reward-secret=c4ab3985ab32ef3e34ee5"
}
```

Response:
```
{
  "txId: "c859b888d3e20a2d6132cbdb732617e1a2701e7bb63029d752a0a6c1d35beba2"
}
```


