# CoinDCX KYC Verification Schema

## Data Source Name

CoinDCX is one of India’s leading cryptocurrency exchanges, offering a secure platform for trading Bitcoin, Ethereum, and other digital assets. Founded in 2018, it aims to simplify crypto investing and promote adoption with features like staking, lending, and educational initiatives.

## API Endpoint URL
`GET https://api.coindcx.com/api/v1/user_details`

Sample JSON response 
```json
{
    "signed_up_at": "2024-08-16T08:44:49.600Z",
    "status": "kyc_verified",
     ........
}
```

#### Verification Mechanism

The schema checks the user's KYC status by asserting that the `status` field equals `kyc_verified`.

#### Nullifier

- Uses `coindcx_id` as a unique identifier to maintain user privacy

## Usage Instructions

- Log in to your CoinDCX account  
- Navigate to the profile section  
- Click the "Start" button to initiate the verification process

## Potential Use Cases

- Proving KYC compliance for cryptocurrency trading
- Accessing platform-specific features requiring verified status
- Streamlining user onboarding for financial services

## Schema JSON

```json
{
  "issuer": "CoinDCX",
  "desc": "COINDCX is india's largest crytpo currency exchange",
  "website": "https://coindcx.com/profile",
  "APIs": [
    {
      "host": "api.coindcx.com",
      "intercept": {
        "url": "api/v1/user_details",
        "method": "GET"
      },
      "assert": [
        {
          "key": "status",
          "value": "kyc_verified",
          "operation": "="
        }
      ],
      "nullifier": "coindcx_id"
    }
  ],
  "HRCondition": [
    "Verify whether the KYC process has been successfully completed on coinDCX"
  ],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```
### schema validation proof
<img width="1013" alt="Screenshot 2024-12-14 at 3 29 17 PM" src="https://github.com/user-attachments/assets/31027ad9-b2eb-4d2d-902f-d1ac52d6a28a" />
