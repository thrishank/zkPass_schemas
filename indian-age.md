# Age of Indian Verfication Schema

## Data Source Name

Digilocker, a digital platform by the Government of India that provides access to various documents, including Aadhar. It allows citizens to access their Aadhar information, which is a unique 12-digit identification number issued to residents of India which contains their biometric and demographic data.

## API Endpoint URL

`POST https://ids.digilocker.gov.in/api/2.0/metadata`

Sample JSON Response:

```json
{
  "residentName": "K Thrishank",
  "state": "Andhra Pradesh",
  "dateOfBirth": "2000-01-01",
  "gender": "M"
}
```

## Technical Breakdown

The Schema is designed to verify whether the person is over 18 years of age or not.
We verify this from the date of birth field in the response. And compare it with the current date.

## Schema Code

````json
{
  "issuer": "Aadhar National Identity of India",
  "desc": "Aadhar is a Indian identity card, which is a 12-digit unique identity number that can be obtained by residents of India, based on their biometric and demographic data.",
  "website": "https://www.digilocker.gov.in/login",
  "APIs": [
    {
      "host": "ids.digilocker.gov.in",
      "intercept": {
        "url": "api/2.0/issueddocs",
        "method": "POST"
        },
      "nullifier": "user_id"
    },
    {
      "host": "ids.digilocker.gov.in",
      "intercept": {
        "url": "api/2.0/metadata",
        "method": "POST"
      },
      "assert": [
        {
          "key": "dateOfBirth",
          "value": "2007-01-01",
          "operation": "<"
        }
      ]
    }

  ],
  "HRCondition": ["verify you are over 18 years old"],
  "tips": {
    "message": "When you successfully log in, please click the 'Start' button to initiate the verification process."
  }
}
````
