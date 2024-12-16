# Indian State Schema

## Data Source Name

**Digilocker**, a digital platform by the Government of India that provides access to various documents, including Aadhar. It allows citizens to access their Aadhar information, which is a unique 12-digit identification number issued to residents of India based on biometric and demographic data.

## API Endpoint URL

`POST https://ids.digilocker.gov.in/api/2.0/metadata`

**Sample JSON Response:**

```json
{
  "residentName": "K Thrishank",
  "state": "Andhra Pradesh",
  "dateOfBirth": "2000-01-01",
  "gender": "M",
}
```

## Technical Breakdown

The schema is designed to verify the user’s residency within a state(ex. Andhra Pradhesh) of India. It checks the state field in the response from the DigiLocker API to ensure the user is a resident of the specified state.

## Schema Code

```json
{
  "issuer": "Digilocker",
  "desc": "Aadhar is an India identity card, which is a 12-digit unique identity number that can be obtained by residents of India, based on their biometric and demographic data.",
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
          "key": "state",
          "value": "Andhra Pradesh",
          "operation": "="
        }
      ]
    }
  ],
  "HRCondition": [
    "verify you belong to the state of Andhra Pradesh"
  ],
  "tips": {
    "message": "If you are already logged in to Digilocker, please log out and log back in. When you successfully log in, please click on the Aadhar Document, and then click the 'Start' button to initiate the verification process."
  }
}
```

Tested with the zkpass validator extension 

<img width="650" alt="Screenshot 2024-12-16 at 12 24 15 PM" src="https://github.com/user-attachments/assets/35af56ed-e336-449d-b943-f6f1685c7684" />
