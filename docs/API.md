# API Instruction

[1. /api/stats] (#user-content-1-apistats)

[2. /api/miners] (#user-content-2-apiminers)

[3. /api/blocks] (#user-content-3-apiblocks)

[4. /api/payments] (#user-content-4-apipayments)

[5. /api/accounts/your_account] (#user-content-5-apiaccountsyour_account)


## 1. /api/stats

You can get current hashrate using `/api/stats` endpoint

> URL: http://your-example-url.com/api/stats

e.g. Result:

```
{
    "candidatesTotal": 1,
    "hashrate": 5581395,
    "immatureTotal": 11,
    "maturedTotal": 4,
    "minersTotal": 1,
    "nodes": [
        {
            "difficulty": "7441444283",
            "height": "116753",
            "lastBeat": "1532718838",
            "name": "main"
        }
        ...
    ],
    "now": 1532718841545,
    "stats": {
        "lastBlockFound": 1531411472,
        "roundShares": 9000000000
    }
}
```

## 2. /api/miners

You can get current miners using `/api/miners` endpoint

> URL: http://your-example-url.com/api/miners

e.g. Result:

```
{
    "hashrate": 7185628,
    "miners": {
        "0x00...": {
            "lastBeat": 1532718100,
            "hr": 7185628,
            "offline": false
        }
        ...
    },
    "minersTotal": 1,
    "now": 1532718506242
}
```

## 3. /api/blocks

You can get current blocks using `/api/blocks` endpoint

> URL: http://your-example-url.com/api/blocks

e.g. Result:

```
{
    "candidates": [
        {
            "height": 32656,
            "timestamp": 1531411472,
            "difficulty": 1866528847,
            "shares": 4000000000,
            "uncle": false,
            "uncleHeight": 0,
            "orphan": false,
            "hash": "",
            "reward": ""
        },
        ...
    ],
    "candidatesTotal": 1,
    "immature": [
        {
            "height": 32627,
            "timestamp": 1531411134,
            "difficulty": 1846607570,
            "shares": 600000000,
            "uncle": false,
            "uncleHeight": 0,
            "orphan": false,
            "hash": "0xe7149539c505a5873eddf33e0fd647557ca12280d9fa3a036f6b0e9890f773b4",
            "reward": "5000000000000000000"
        },
        ...
    ],
    "immatureTotal": 11,
    "luck": {
        "15": {
            "luck": 0.5823508296780175,
            "orphanRate": 0,
            "uncleRate": 0
        }
        ...
    },
    "matured": [
        {
            "height": 32532,
            "timestamp": 1531410192,
            "difficulty": 1767293442,
            "shares": 1400000000,
            "uncle": false,
            "uncleHeight": 0,
            "orphan": false,
            "hash": "0x6e0dc56bef6fdc1d185e64f0fdde8aea06e0961505658da0a492732cfbd33080",
            "reward": "5000000000000000000"
        },
        ...
    ],
    "maturedTotal": 4
}
```

## 4. /api/payments

You can get payments information using `/api/payments` endpoint

> URL: http://your-example-url.com/api/payments

e.g. Result:

```
{
    "payments": [
        {
            "address": "0x...",
            "amount": 15000000000,
            "timestamp": 1531411438,
            "tx": "0x532f726f330999ecc876912399054edf871874d0453f3fe088c1ed49442f6134"
        }
        ...
    ],
    "paymentsTotal": 1
}
```

## 5. /api/accounts/your_account

You can get hashrate and payments information of `your_account` using `/api/accounts/<your_account>` endpoint

> URL: http://your-example-url.com/api/accounts/0x...

e.g. Result:

```
{
    "currentHashrate": 194444444,
    "hashrate": 180996345,
    "pageSize": 30,
    "payments": [
        {
            "amount": 93697916667,
            "timestamp": 1533090580,
            "tx": "0xafd06fde7c1d045d3589fa6059ca78ebfebd8792dd8dda3eabde9d153f119586"
        },
        ...
    ],
    "paymentsTotal": 92,
    "roundShares": 4000000000,
    "stats": {
        "balance": 0,
        "blocksFound": 866,
        "immature": 244256944446,
        "lastShare": 1533090585,
        "paid": 3907947595662,
        "pending": 0
    },
    "workers": {
        "NABIRU": {
            "lastBeat": 1533090585,
            "hr": 194444444,
            "offline": false,
            "hr2": 180996345
        }
    },
    "workersOffline": 0,
    "workersOnline": 1,
    "workersTotal": 1
}
```
