# CoinDCX Account Verification Schema Integration

## Data Source Name

CoinDCX – India's prominent cryptocurrency exchange platform providing digital asset trading and financial services. This schema enables verification of a user's CoinDCX account existence.

## API Endpoint URL

`GET https://api.coindcx.com/api/v1/user_details`  
This endpoint facilitates access to basic user account information, confirming the existence of a valid CoinDCX account.

**Sample JSON Response:**

```json
{
  "coindcx_id": "USER12345",
  "first_name": "trader_name",
  "status": "kyc_verified"
}
```

## Technical Breakdown

The schema is designed to securely verify a user's CoinDCX account using zkPass's zkTLS framework. It integrates with the CoinDCX API to fetch user details, ensuring data privacy and account validation through cryptographic tools.

### How it Verifies CoinDCX Account

The schema verifies account existence by checking if the **coindcx_id** field is not empty (`coindcx_id != ""`). This ensures the user has a registered account on the CoinDCX platform without exposing sensitive account details.

## Schema Code

```json
{
  "issuer": "COINDCX",
  "desc": "verify",
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
          "key": "coindcx_id",
          "value": " ",
          "operation": "!="
        }
      ],
      "nullifier": "coindcx_id"
    }
  ],
  "HRCondition": ["Verify you have COINDCX account"],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```



## Optional - Demo/Test Case

This schema is used to verify the user's CoinDCX account existence, which is crucial for accessing platform-specific services and features.

#### Test Case Steps

1. **Login to CoinDCX:**
   Users must first log in to their CoinDCX account.

2. **Initiate the Verification Process:**
   After logging in, the user must click the "Start" button to trigger account verification through zkPass.

3. **Assertion Validation:**
   The schema checks that the **coindcx_id** field is not empty (`coindcx_id != ""`). If this field contains a valid ID, the user is confirmed to have an active CoinDCX account.

4. **Output:**
   The verification process will either pass or fail based on the **coindcx_id**. If the user has a registered CoinDCX account, the test will pass.

<img width="1005" alt="Screenshot 2024-12-14 at 7 02 12 PM" src="https://github.com/user-attachments/assets/0430bca4-959a-40e1-a316-484cf1540615" />

#### Real-World Use Cases

- **Platform Access Verification:**
  Confirm user's registered status on the CoinDCX platform.
- **Service Eligibility:**
  Validate account existence for specific crypto trading or financial services.

This approach adheres to zkPass's principles of secure, privacy-preserving identity verification.
