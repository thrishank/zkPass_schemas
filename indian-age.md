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
  "issuer": "Digilocker",
  "desc": "Aadhar is an Indian identity card, which is a 12-digit unique identity number that can be obtained by residents of India, based on their biometric and demographic data.",
  "website": "https://www.digilocker.gov.in/login",
  "APIs": [
    {
      "host": "api-delhi-accounts-10001.digitallocker.gov.in",
      "intercept": {
        "url": "users/profile",
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
  "HRCondition": [
    "verify you are over 18 years old"
  ],
  "tips": {
    "message": "If you are already logged in to Digilocker, please logout and log in again. When you successfully log in, click on the Aadhar Document, and then click the 'Start' button to initiate the verification process."
  }
}
````

Tested with the zkPass validator extension and succuessfullly got the validator json response 
<img width="611" alt="Screenshot 2024-12-16 at 12 32 39 PM" src="https://github.com/user-attachments/assets/89629982-a4d6-4f3a-af1b-19b3558be153" />
