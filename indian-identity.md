# Aadhar National Identity Schema Integration

## Data Source Name

Aadhaar is India's digital identity card, established by the Government of India. It provides a 12-digit unique identification number to Indian residents, linking their biometric and demographic data for secure and centralized identity verification.

Aadhaar is integrated with DigiLocker, a cloud-based platform provided by the Indian government. DigiLocker allows individuals to store and access important documents, such as Aadhaar, PAN, and driving licenses, in a secure digital format. This integration simplifies document verification and reduces the need for physical copies, making processes more efficient and convenient.

## API Endpoint URL

`POST https://ids.digilocker.gov.in/api/2.0/metadata`  
This endpoint facilitates access to Aadhar-linked data via DigiLocker, returning detailed demographic information, including resident name, date of birth, gender, and address.

**Sample JSON Response:**

```json
{
  "residentName": "K Thrishank",
  "dateOfBirth": "2000-01-01",
  "gender": "M",
  "address": {
    "street": "12th Main Road",
    "city": "Banglore",
    "state": "Karnataka",
    "pincode": "517501"
  },
  "aadharNumber": "XXXX-XXXX-1234"
}
```

## Technical Breakdown

To implement a zero-knowledge proof (ZKP) using the Aadhaar API, we intercept the POST request to the DigiLocker metadata endpoint to validate the response without exposing sensitive data. The intercepted response is checked for the presence of key fields, such as residentName, to ensure it is not empty (residentName != " "). This assertion confirms that the data returned by the API is valid. A cryptographic proof is generated based on these validations, enabling secure identity verification without disclosing any personal information during the process. This ensures a privacy-preserving and tamper-proof verification method leveraging zkPass principles.

## Schema Code

```json
{
  "issuer": "Digilocker",
  "desc": "Aadhar is an Indian identity card, which is a 12-digit unique identity number that can be obtained by residents of India.",
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
          "key": "residentName",
          "value": " ",
          "operation": "!="
        }
      ]
    }
  ],
  "HRCondition": [
    "verify you are an Indian resident"
  ],
  "tips": {
    "message": "If you are already logged in to Digilocker, please log out and log in again. When you successfully log in, please click on the Aadhar Document and then click the 'Start' button to initiate the verification process."
  }
}
```

#### Screenshot of Schema Validation

Here’s a screenshot of the schema validation by zkpass schema validator extension, showing that the verification was successful:

 <img width="637" alt="Screenshot 2024-12-16 at 12 36 37 PM" src="https://github.com/user-attachments/assets/2667f1e3-0ffa-40cf-a76c-d15eba15b2ce" />

