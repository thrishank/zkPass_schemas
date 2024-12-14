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
  ...
}
```

## Technical Breakdown

The schema is designed to verify the user’s residency within a state(ex. Andhra Pradhesh) of India. It checks the state field in the response from the DigiLocker API to ensure the user is a resident of the specified state.

## Schema Code

```json
{
  "issuer": "Digilocker",
  "desc": "Aadhar is a India identity card, which is a 12-digit unique identity number that can be obtained by residents of India, based on their biometric and demographic data.",
  "website": "https://www.digilocker.gov.in/login",
  "APIs": [
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
      ],
      "nullifier": "residentName"
    }
  ],
  "HRCondition": ["verify you are belong to the state of Andhra Pradesh"],
  "tips": {
    "message": "When you successfully log in and click on the Aadhar, please click the 'Start' button to initiate the verification process."
  }
}
```

## proof

<img width="1047" alt="Screenshot 2024-12-14 at 3 08 45 PM" src="https://github.com/user-attachments/assets/0a75b28f-d383-426e-aa2e-bf08949bb949" />
