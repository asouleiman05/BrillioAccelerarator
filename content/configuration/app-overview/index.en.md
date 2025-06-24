---
title: "App Overview"
weight: 30
---

The **AWS Payment Gateway Accelerator App** is a React-based single-page application that allows users to log in, initiate credit transfer payments, and receive confirmation via the [Aplon Hub](https://aplonhub-brillio.pc14.eu/).

This section outlines the main user flows and components.

---

## 🔐 1. Login Screen

Users begin by logging in to access the payment interface.

- **Fields:** Username and password
- **Validation:** Basic client-side validation
- **Routing:** On login, the user is redirected to the `/transfer` route

**Screenshot:**  
![Login Screen](/static/images/login-screen.png)

---

## 💸 2. Credit Transfer Form

This is the core feature of the app. It allows users to initiate a credit transfer by filling out:

- **Amount (EUR)**
- **Payment description**
- **Debtor name and IBAN**
- **Creditor name and IBAN**

On clicking **Send**:

- A `PUT` request is sent to the CBPR+ Credit Transfer API
- A transaction ID and UETR are generated in the frontend
- On successful response, the user is navigated to the success screen

**Cancel** resets the form.

**Screenshot:**  
![Send Payment Form](/static/images/send-payment.png)

---

## ✅ 3. Success Confirmation

After submitting a transfer:

- The user is routed to the `/success` screen
- This screen displays:
  - A success message
  - Transaction details (passed via router state)
  - Optional links or confirmation info

**Screenshot:**  
![Transaction Success Screen](/static/images/success-screen.png)

---

## 🧩 Component Structure (React)

```plaintext
src/
├── components/
│   ├── Login/
│   │   └── Login.jsx
│   ├── CreditTransferForm/
│   │   └── CreditTransferForm.jsx
│   └── SuccessScreen/
│       └── SuccessScreen.jsx
├── App.js
└── index.js
```
