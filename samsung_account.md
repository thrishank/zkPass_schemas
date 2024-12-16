# Verification Schema

## Data Source Name

Samsung is a South Korean multinational conglomerate headquartered in Seoul. It is one of the world's largest producers of electronic devices, including smartphones, televisions, and home appliances. Samsung is also involved in various other industries such as shipbuilding, construction, and insurance.

## API Endpoint

`GET https://v3.account.samsung.com/api/v1/users`

Sample json response:

```json
{
  "type": "individual",
  "status": "active",
  "accounts": [
    {
      "type": "email",
      "value": "thrishankkalluru@gmail.com",
      "status": "NORMAL",
      "verified": true
    }
  ]
}
```

## Technical Breakdown

To verify if a user has an active Samsung account, we intercept the `GET` request to the API endpoint mentioned above. We then check the `status` field in the JSON response to ensure it is set to `"active"`.

## Schema Code

```json
{
  "issuer": "Samsung",
  "desc": "Samsung is a multinational conglomerate known for its electronics, appliances, and technology products",
  "website": "https://v3.account.samsung.com/dashboard",
  "APIs": [
    {
      "host": "v3.account.samsung.com",
      "intercept": {
        "url": "api/v1/users",
        "method": "GET"
      },
      "assert": [
        {
          "key": "status",
          "value": "active",
          "operation": "="
        }
      ],
      "nullifier": "accounts|0|value"
    }
  ],
  "HRCondition": ["Verify that you have a active samsung account"],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```

<img width="636" alt="Screenshot 2024-12-16 at 12 40 20 PM" src="https://github.com/user-attachments/assets/26fcba1d-2108-4c18-a842-6cadaad9bc05" />
