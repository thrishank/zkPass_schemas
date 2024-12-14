# Aadhar National Identity Schema Integration

## Data Source Name

Aadhar National Identity of India – a unique identification system implemented by the Government of India. It assigns a 12-digit unique identity number to Indian residents based on their biometric and demographic data, ensuring secure and centralized identity verification.

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

The schema is designed to securely verify a user's identity and residency using zkPass’s zkTLS framework. It integrates with the DigiLocker API to fetch Aadhar data, ensuring data privacy and integrity through zkPass's cryptographic tools.

### How it Verifies Indian Residency

The schema verifies Indian residency by checking if the **residentName** field in the DigiLocker API response is not empty (`residentName != ""`). Since only Indian residents can have an Aadhar card, this ensures the user has a valid Aadhar account and confirms their Indian residency, without exposing any sensitive data.

## Schema Code

```json
{
  "issuer": "Aadhar",
  "desc": "Aadhar is Indian identity card, which is a 12-digit unique identity number that can be obtained by residents of India",
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
          "key": "residentName",
          "value": " ",
          "operation": "!="
        }
      ],
      "nullifier": "residentName"
    }
  ],
  "HRCondition": ["verify you are an Indian resident"],
  "tips": {
    "message": "When you successfully log in click on the Aadhar Card and , please click the 'Start' button to initiate the verification process."
  }
}
```

## Optional - Demo/Test Case

This schema is used to verify the user’s Indian residency by ensuring they possess a valid Aadhar card, which is required for various services like KYC compliance, government benefits, and more.

#### Test Case Steps

1. **Login to DigiLocker:**
   Users must first log in to their DigiLocker account linked to their Aadhar number.

2. **Initiate the Verification Process:**
   After logging in, the user must click the "Start" button to trigger the Aadhar verification through zkPass.

3. **Assertion Validation:**
   The schema checks that the **residentName** field is not empty (`residentName != ""`). If this field contains a valid name, the user is confirmed to have a valid Aadhar card, thus verifying their Indian residency.

4. **Output:**
   The verification process will either pass or fail based on the **residentName**. If the user is a valid Indian resident with a registered Aadhar number, the test will pass.

#### Screenshot of Schema Validation

Here’s a screenshot of the schema validation by zkpass schema validator extension, showing that the verification was successful:

<img width="1036" alt="Screenshot 2024-12-14 at 2 49 36 PM" src="https://github.com/user-attachments/assets/03184fac-0c44-498b-94f2-abd117c2284b" />

#### Real-World Use Cases

- **Eligibility Verification for Government Schemes:**
  Users can prove their eligibility for subsidies or welfare schemes tied to Indian residency.
- **KYC Compliance for Financial Services:**
  Financial institutions can leverage this schema to verify Indian residency during onboarding.
- **Location-Specific Access:**
  Applications can restrict access to services or resources to users residing in India.

This approach adheres to zkPass's principles of secure, privacy-preserving identity verification.
