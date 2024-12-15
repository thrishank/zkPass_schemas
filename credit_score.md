# Credit Score Verification Schema

## Data Source Name

**CRIF High Mark** - A credit bureau in India providing credit scores and reports to individuals

## API Endpoints

### 1. Order History Endpoint

`https://cir.crifhighmark.com/b2cInquiry/orderHistory/?=?`

```json
{
  "PERSONAL_REPORT": [
    {
      "userId": "135256303",
      "reportId": "FCR241213CR803069988",
      "reportDate": "13 DEC 2024",
      "reportTime": "09:57 PM",
      "inquiryName": "Name",
      "displayStatus": "002",
      "productType": "B2C-CONSUMER-SCORE"
    }
  ]
}
```

### 2. Performance Dashboard Endpoint

`https://cir.crifhighmark.com/b2cInquiry/dashboard/performance/?=?`

```json
[
  {
    "inquiryId": "12243464379",
    "creditScore": 761,
    "inquiryDate": "13 Dec 2024",
    "reportId": null
  }
]
```

## Technical Breakdown

The schema is designed to securely verify a user's credit score using zkTLS
The data is verified from the dashboard/performance GET request api. The creditScore field is checked to be greater than 700 to validate the credit score.

## Schema Code

```json
{
  "issuer": "CRIF High Mark",
  "desc": "Credit bureau providing credit scores and reports in India",
  "website": "https://cir.crifhighmark.com/dashboard/personal/home",
  "APIs": [
    {
      "host": "cir.crifhighmark.com",
      "intercept": {
        "url": "b2cInquiry/orderHistory/?=?",
        "method": "POST"
      },
      "nullifer": "PERSONAL_REPORT|0|userId"
    },
    {
      "host": "cir.crifhighmark.com",
      "intercept": {
        "url": "b2cInquiry/dashboard/performance/?=?",
        "method": "GET"
      },
      "assert": [
        {
          "key": "0|creditScore",
          "value": "700",
          "operation": ">"
        }
      ]
    }
  ],
  "HRCondition": ["Verify that you have a credit score of more than 700"],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```

## Verification Process

1. Login to CRIF High Mark portal
2. Initiate verification
3. Automatically validate credit score
