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
