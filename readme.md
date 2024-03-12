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

- **API Calls and Responses:**
  - The application utilizes APIs to interact with the server for data retrieval, updates, and processing.
  - API calls are made to perform actions such as device CRUD operations, SIM card activation/deactivation, billing status updates, and KYC procedures.
  - Responses from the server are handled accordingly, with error handling mechanisms in place to manage exceptions and provide feedback to users.

## 4. Demo to App:
- **Getting Started:**
  - Users can download the IOT device management application from the designated platform.
  - Upon installation, users can sign up for a new account or log in with existing credentials.

- **Using the App:**
  - Admin users can access all functionalities related to device management, SIM card activation, billing status management, and more.
  - User accounts have limited access to view device details and manage billing status.
  - Production Line operators can add devices to the database and activate SIM cards in test mode.

- **Troubleshooting:**
  - In case of any issues or errors, users can access the help section within the application for assistance.
  - Common troubleshooting steps may include contacting support or referring to documentation for guidance.

## 5. Future Scope:
- Future enhancements may include expanding user roles and access levels, implementing additional functionalities for User and Production Line operators, and enhancing the user interface for improved usability.
- Integration with third-party services for automated billing management, advanced analytics, and reporting capabilities could also be considered as part of the future scope.
