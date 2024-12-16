# Verification Schema

## Data Source Name

Samsung is a South Korean multinational conglomerate headquartered in Seoul. It is one of the world's largest producers of electronic devices, including smartphones, televisions, and home appliances. Samsung is also involved in various other industries such as shipbuilding, construction, and insurance.

## API Endpoint

`GET https://www.samsung.com/aemapi/v6/mysamsung/in/scv/newproducts`

```json
"statusCode": 200,
    "statusMessage": "OK",
    "resultData": {
        "myProducts": {
            "basicInfo": {
                "guid": "hieyuhvyth",
                "productCnt": "1"
            },
```

## Technical Breakdown

To verify if a user has at least one Samsung device registered to their account, we intercept the `GET` request to the API endpoint. And in the json response if the value of `productCnt` is greater than `0`, it confirms that the user has at least one registered Samsung device.

## Schema Code

```json
{
  "issuer": "Samsung",
  "desc": "Samsung is a multinational conglomerate known for its electronics, appliances, and technology products.",
  "website": "https://www.samsung.com/in/mypage/myproducts/",
  "APIs": [
    {
      "host": "www.samsung.com",
      "intercept": {
        "url": "aemapi/v6/mysamsung/in/scv/newproducts",
        "method": "GET"
      },
      "assert": [
        {
          "key": "resultData|myProducts|basicInfo|productCnt",
          "value": "0",
          "operation": ">"
        }
      ],
      "nullifier": "resultData|myProducts|basicInfo|guid"
    }
  ],
  "HRCondition": [
    "Verify that you have at least one Samsung device registered to your account."
  ],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
```
<img width="643" alt="Screenshot 2024-12-16 at 12 39 00 PM" src="https://github.com/user-attachments/assets/38b3b590-6706-4cde-923a-6eb98cff5f45" />

