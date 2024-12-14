# CoinDCX Futures Wallet Balance Verification Schema

## Data Source Name

CoinDCX – A leading cryptocurrency trading platform in India, providing comprehensive wallet and trading infrastructure for digital asset transactions.

## API Endpoint URL

`GET https://api.coindcx.com/api/v1/derivatives/futures/wallets`  
This endpoint retrieves detailed information about the user's wallet balances and financial account status.

**Sample JSON Response:**

```json
[
  {
    "id": "ea195e2b-43cd-4615-82be-b84b4d0222e9",
    "currency_short_name": "INR",
    "balance": "0.0",
    "locked_balance": "0.0",
    "cross_order_margin": "0.0",
    "cross_user_margin": "0.0"
  }
]
```

## Technical Breakdown

The schema is designed to securely verify a user's wallet balance using zkPass's zkTLS framework. It validates the user's financial account details through a privacy-preserving verification process.

### Verification Mechanism

The schema checks the wallet balance and ensures financial account authenticity without exposing sensitive account information.

## Schema Code

```json
{
  "issuer": "COINDCX",
  "desc": "coindcx is the largest cryptocurrency exchange in india",
  "website": "https://coindcx.com/portfolio",
  "APIs": [
    {
      "host": "api.coindcx.com",
      "intercept": {
        "url": "api/v1/derivatives/futures/wallets",
        "method": "GET"
      },
      "assert": [
        {
          "key": "0|balance",
          "value": "10000.0",
          "operation": ">"
        }
      ],
      "nullifier": "0|id"
    }
  ],
  "HRCondition": [
    "Verify you have a balance of more than 10000 in your COINDCX account"
  ],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```

## Verification Process

1. **Login to CoinDCX:**
   Access your CoinDCX trading account

2. **Initiate Verification:**
   Click "Start" to trigger the wallet balance verification

3. **Balance Validation:**
   Automatically checks if your wallet balance exceeds 10,000

This approach ensures secure, privacy-preserving financial verification.
![image](https://github.com/user-attachments/assets/95b3c013-bfbf-4ca3-9449-45e6dc08b545)
