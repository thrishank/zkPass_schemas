# CoinDCX KYC Verification Schema

## Overview

This zkPass schema is designed to verify a user's KYC (Know Your Customer) status on CoinDCX, India's largest cryptocurrency exchange. The schema provides a privacy-preserving method to confirm that a user has completed the KYC verification process without exposing sensitive personal information.

## Schema Description

### Issuer

- **Name**: CoinDCX
- **Description**: India's largest cryptocurrency exchange platform

### Verification Goal

Verify whether the user has successfully completed the KYC process on CoinDCX.

### Technical Details

#### API Integration

- **Host**: `api.coindcx.com`
- **Endpoint**: `/api/v1/user_details`
- **Method**: `GET`
#### Sample JSON response 
```json
 ....,  
    "signed_up_at": "2024-08-16T08:44:49.600Z",
    "status": "kyc_verified",
....
```

#### Verification Mechanism

The schema checks the user's KYC status by asserting that the `status` field equals `kyc_verified`.

#### Nullifier

- Uses `coindcx_id` as a unique identifier to maintain user privacy

## Usage Instructions

1 Log in to your CoinDCX account 2. Navigate to the profile section 3. Click the "Start" button to initiate the verification process

## Potential Use Cases

- Proving KYC compliance for cryptocurrency trading
- Accessing platform-specific features requiring verified status
- Streamlining user onboarding for financial services

## Privacy Considerations

This schema leverages zkPass's zero-knowledge proof technology to:

- Verify KYC status without revealing personal details
- Protect user privacy during verification
- Ensure secure and transparent identity validation

## Schema JSON

```json
{
  "issuer": "COINDCX is india's largest crytpo currency exchange",
  "desc": "",
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

## Requirements

- Active CoinDCX account
- Completed KYC verification
- Access to zkPass verification platform

### schema validation proof
<img width="1013" alt="Screenshot 2024-12-14 at 3 29 17 PM" src="https://github.com/user-attachments/assets/31027ad9-b2eb-4d2d-902f-d1ac52d6a28a" />
