# Functional Specification Document

## 1. Summary:
- This functional specification document outlines the features and functionalities of the IOT device management application. It serves as a guide for the development team to understand the project requirements and deliverables.

## 2. Business Requirement:
- The IOT device management application aims to centralize the handling of device details, including Device QR Code, Serial number, IMEI Number, SIM Number, Device Model name, client name, and client address.
- Key functionalities include activating, deactivating, and suspending SIM cards, managing billing status and payments for SIM cards, conducting KYC procedures for SIM cards, and implementing CRUD operations for devices in the database.
- Authorization levels are defined for three types of operators: Admin, User, and Production Line, with varying levels of access to the application's functionalities.

## 3. Application Flow:
- **User Registration and Authentication:**
  - Users can register for an account with the IOT device management application.
  - Upon registration, users receive a verification email to activate their account.
  - Users can log in securely using their credentials.

- **Main Application Interface:**
  - Upon logging in, users are directed to the main dashboard.
  - The dashboard displays relevant information based on the user's role (Admin, User, or Production Line).
  - Navigation within the application is facilitated through a user-friendly interface with access to different functionalities based on the user's role.

- **Functionality for Admin:**
  - Admin users have access to all functionalities related to device management, including CRUD operations for devices, SIM card activation, deactivation, suspension, billing status management, and SIM card KYC procedures.

- **Functionality for Users:**
  - User accounts have restricted access compared to Admin accounts.
  - Users can view device details and access billing status information for SIM cards associated with their account.
  - Payment processing functionalities are available for users to update billing status based on monthly or yearly plans.

- **Functionality for Production Line:**
  - Production Line operators have limited access to specific functionalities for adding devices to the database and activating SIM cards in test mode for initial testing purposes.

- **API Integration:**
  - The application integrates with external APIs to perform various actions such as user registration, login, forgot password, email verification, device management, etc.
  - Detailed specifications for each API endpoint are provided below:

## 4. API Integration Details:
### Register API:
- **Base URL:** `https://config.iot.mrmprocom.com/php-admin/register.php`
- **Access Control:**
  - Allow-Origin: `https://config.iot.mrmprocom.com, https://test.mrmprocom.com `
  - Allow-Methods: `POST`
- **Request Data:**
  - `name`
  - `email`
  - `password`
- **Error Handling:**
  - If request type is not POST:
    - JSON Response: ` {"success": 0, "status": 404, "message": "Invalid request type"} `
  - If empty or missing fields:
    - JSON Response: ` {"success": 0, "status": 444, "message": "Missing or empty fields", "fields": [“name”, "email", "password"]} `
  - If invalid email:
    - JSON Response: ` {"success": 0, "status": 422, "message": "Invalid email address"} `
  - If password length is not between 8 and 16:
    - JSON Response: ` {"success": 0, "status": 422, "message": "Invalid password length"} `
  - If name length is not between 3 and 15:
    - JSON Response: ` {"success": 0, "status": 422, "message": "Invalid name length"} `
  - If email is already registered:
    - JSON Response: ` {"success": 0, "status": 421, "message": "Email already registered"} `
  - If verification email not sent:
    - JSON Response: ` {"success": 0, "status": 412, "message": " Verification email not sent"} `
- **Success Response:**
  - If verification email sent successfully:
    - JSON Response: ` {"success": 1, "status": 200, "message": "Verification email sent successfully"} `
- **Failure Response:**
  - If any exception occurs:
    - JSON Response: ` {"success": 0, "status": 500, "message": "Internal server error"} `

### Login API:
- **Base URL:** `https://config.iot.mrmprocom.com/php-admin/login.php`
- **Access Control:**
  - Allow-Origin: `https://config.iot.mrmprocom.com, https://test.mrmprocom.com `
  - Allow-Methods: `POST`
- **Request Data:**
  - `email`
  - `password`
- **Error Handling:**
  - If request type is not POST:
    - JSON Response: ` {"success": 0, "status": 404, "message": "Invalid request type"} `
  - If empty or missing fields:
    - JSON Response: ` {"success": 0, "status": 444, "message": "Missing or empty fields", "fields": ["email", "password"]} `
  - If invalid email:
    - JSON Response: ` {"success": 0, "status": 422, "message": "Invalid email address"} `
  - If password length is not between 8 and 16:
    - JSON Response: ` {"success": 0, "status": 422, "message": "Invalid password length"} `
  - If email is not registered:
    - JSON Response: ` {"success": 0, "status": 423, "message": "Email not registered"} `
  - If password verification fails:
    - JSON Response: ` {"success": 0, "status": 413, "message": "Incorrect password"} `
  - If email is not verified:
    - JSON Response: ` {"success": 0, "status": 415, "message": "Email not verified"} `
- **Success Response:**
  - If login successful:
    - JSON Response: ` {"success": 1, "message": "Login successful", "token": $token} `
- **Failure Response:**
  - If any exception occurs:
    - JSON Response: ` {"success": 0, "status": 500, "message": "Internal server error"} `

### Forgot Password API:
- **Base URL:** `https://config.iot.mrmprocom.com/php-admin/forgetPass.php`
- **Access Control:**
  - Allow-Origin: `https://config.iot.mrmprocom.com, https://test.mrmprocom.com `
  - Allow-Methods: `POST`
- **Request Data:**
  - `email`
- **Error Handling:**
  - If request type is not POST:
    - JSON Response: ` {"success": 0, "status": 404, "message": "Invalid request type"} `
  - If empty or missing fields:
    - JSON Response: ` {"success": 0, "status": 444, "message": "Missing or empty fields", "fields": ["email"]} `
  - If invalid email:
    - JSON Response: ` {"success": 0, "status": 422, "message": "Invalid email address"} `
  - If email is not registered:
    - JSON Response: ` {"success": 0, "status": 423, "message": "Email not registered"} `
  - If password reset email not sent:
    - JSON Response: ` {"success": 0, "status": 412, "message": " Password reset email not sent"} `
- **Success Response:**
  - If password reset email sent successfully:
    - JSON Response: ` {"success": 1, "status": 200, "message": "Password reset email sent successfully"} `
- **Failure Response:**
  - If any exception occurs:
    - JSON Response: ` {"success": 0, "status": 500, "message": "Internal server error"} `

### Send Email Verification API:
- **Base URL:** `https://config.iot.mrmprocom.com/php-admin/sendVerificationLink.php`
- **Access Control:**
  - Allow-Origin: `https://config.iot.mrmprocom.com, https://test.mrmprocom.com `
  - Allow-Methods: `POST`
- **Request Data:**
  - `email`
- **Error Handling:**
  - If request type is not POST:
    - JSON Response: ` {"success": 0, "status": 404, "message": "Invalid request type"} `
  - If empty or missing fields:
    - JSON Response: ` {"success": 0, "status": 444, "message": "Missing or empty fields", "fields": ["email"]} `
  - If invalid email:
    - JSON Response: ` {"success": 0, "status": 422, "message": "Invalid email address"} `
  - If email is not registered:
    - JSON Response: ` {"success": 0, "status": 423, "message": "Email not registered"} `
  - If email is already verified:
    - JSON Response: ` {"success": 0, "status": 424, "message": "Email already verified"} `
  - If verification email not sent:
    - JSON Response: ` {"success": 0, "status": 412, "message": " Verification email not sent"} `
- **Success Response:**
  - If verification link sent successfully:
    - JSON Response: ` {"success": 1, "status": 200, "message": "Verification link sent successfully"} `

### Email Verification API:
- **Base URL:** `https://config.iot.mrmprocom.com/php-admin/verifyEmail.php`
- **Access Control:**
  - Allow-Origin: `https://config.iot.mrmprocom.com, https://test.mrmprocom.com `
  - Allow-Methods: `GET`
- **Request Data:**
  - `email`
  - `code`
- **Error Handling:**
  - If request type is not POST:
    - JSON Response: ` {"success": 0, "status": 404, "message": "Invalid request type"} `
  - If empty or missing fields in URL:
    - JSON Response: ` {"success": 0, "status": 444, "message": "Missing or empty fields", "fields": ["email", “code”]} `
  - If email does not exist in the database:
    - JSON Response: ` {"success": 0, "status": 423, "message": "Email not registered"} `
  - If email is already verified:
    - JSON Response: ` {"success": 0, "status": 424, "message": "Email already verified"} `
- **Success Response:**
  - If email verification successful:
    - JSON Response: ` {"success": 1, "status": 200, "message": "Email verification successful"} `

### Get Device API:
- **Base URL:** `https://config.iot.mrmprocom.com/php-admin/getDevices.php`
- **Access Control:**
  - Allow-Origin: `https://config.iot.mrmprocom.com, https://test.mrmprocom.com `
  - Allow-Methods: `GET`
- **Request Data:**
  - `deviceSerialNo`
- **Error Handling:**
  - [Error handling details...]
- **Success Response:**
  - [Success response details...]
- **Failure Response:**
  - [Failure response details...]

### Add Device API:
- **Base URL:** `https://config.iot.mrmprocom.com/php-admin/addDevices.php`
- **Access Control:**
  - Allow-Origin: `https://config.iot.mrmprocom.com, https://test.mrmprocom.com `
  - Allow-Methods: `POST`
- **Request Data:**
  - [Request data details...]
- **Error Handling:**
  - [Error handling details...]
- **Success Response:**
  - [Success response details...]
- **Failure Response:**
  - [Failure response details...]

### Delete Device API:
- **Base URL:** `https://config.iot.mrmprocom.com/php-admin/deleteDevices.php`
- **Access Control:**
  - Allow-Origin: `https://config.iot.mrmprocom.com, https://test.mrmprocom.com `
  - Allow-Methods: `POST`
- **Request Data:**
  - `deviceSerialNo`
- **Error Handling:**
  - [Error handling details...]
- **Success Response:**
  - [Success response details...]
- **Failure Response:**
  - [Failure response details...]

### Edit Device API:
- **Base URL:** `https://config.iot.mrmprocom.com/php-admin/editDevices.php`
- **Access Control:**
  - Allow-Origin: `https://config.iot.mrmprocom.com, https://test.mrmprocom.com `
  - Allow-Methods: `POST`
- **Request Data:**
  - [Request data details...]
- **Error Handling:**
  - [Error handling details...]
- **Success Response:**
  - [Success response details...]
- **Failure Response:**
  - [Failure response details...]

## 5. Demo to App:
- **Getting Started:**
  - Users can download the IOT device management application from the designated platform.
  - Upon installation, users can sign up for a new account or log in with existing credentials.

## 6. Future Scope:
- Implementation of additional features such as [list potential future features...].
- Integration of Airtel APIs for [specific functionalities...] as per requirements.

---

### Error Codes:
- **200:** Success
- **404:** Invalid request type
- **406:** Entries not found
- **407:** Device not found
- **408:** Device already exists
- **409:** Device not deleted
- **410:** Device not added
- **411:** Device info not edited
- **412:** Verification email not sent
- **413:** Incorrect Password
- **414:** Password reset email not sent
- **415:** Email not verified
- **421:** Email already registered
- **422:** Invalid Email Address/ Invalid Password Length/Invalid Name Length/ Invalid device serial number length/ Invalid device QR code length/ Invalid device IMEI length/ Invalid SIM number length
- **423:** Email not registered
- **424:** Email already verified
- **444:** Missing or empty fields
- **500:** Internal server error
