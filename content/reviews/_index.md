Reviews submitted through Veritas are automatically added to Britevue and
distinguished as a Verified Review. If the receipt contains an issued reward,
the reward is issued to the user and is redeemed when the user signs up for an
account on Britevue. If the email is already linked to a Britevue account, then
the reward is sent directly to the Handcash wallet associated with the user. 

### Submit Review


`[POST] /veritas/review`

Request Body:
```
{
  "receiptID": "c859b888d3e20a2d6132cbdb732617e1a2701e7bb63029d752a0a6c1d35beba2",
  "receiptSecret: "c4ab3985ab32ef3e34ee5",
  "reviewBody": "I loved it! This is an incredible place to get drinks, and Ashley was terrific!",
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
