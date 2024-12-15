# Credit Score Verification Schema

## Data Source Name

**CRIF High Mark** - A credit bureau in India providing credit scores and reports to individuals

## API Endpoints

### 1. Order History Endpoint

`GET https://cir.crifhighmark.com/b2cInquiry/dashboard/creditProfile/135256303/12243464379`  
Sample JSON Response

```json
{
  "userId": "135256303",
  "inquiryId": 12243464379,
  "inquiryDate": "13 Dec 2024",
  "totalLoanAmount": "0",
  "creditScore": 761,
  "alertLender": 0
}
```

## Technical Breakdown

The schema is designed to securely verify a user's credit score using zkTLS
The data is verified from the dashboard/creditProfile GET request api. The creditScore field is checked to be greater than 700 to validate the credit score.

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
        "url": "b2cInquiry/dashboard/creditProfile/?=?/?=?",
        "method": "GET"
      },
      "assert": [
        {
          "key": "creditScore",
          "value": "700",
          "operation": ">"
        }
      ],
      "nullifer": "inquiryId"
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
