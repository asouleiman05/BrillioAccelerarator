---
title: "Credit Transfer API Integration"
weight: 40
---

This section explains how the React app integrates with the AplonHub CBPR+ API to initiate a **credit transfer**.

---

## 🔗 API Endpoint

PUT {{url}}/aplon-hub-api/cbpr/customer/credit/transfer

This endpoint is used to create an outgoing CBPR+ payment.

---

## 📤 Request Body

The app dynamically fills certain values like `txId`, `uetr`, and `interbankSettlementDate` before submitting the request:

```json
{
  "settlementInfo": {
    "settlementMethod": "CLRG"
  },
  "chargeBearer": "DEBT",
  "interbankSettlementDate": "{{intrBkSttlmtDt}}",
  "interbankSettlementAmount": {
    "currencyCode": "EUR",
    "value": 45.98
  },
  "paymentIdentification": {
    "endToEndIdentification": "NOTPROVIDED",
    "transactionIdentification": "{{txId}}",
    "instructionIdentification": "{{txId}}",
    "uetr": "{{uetr}}"
  },
  "instructingAgent": {
    "financialInstitutionIdentification": {
      "bicfi": "BANKSBIC"
    }
  },
  "instructedAgent": {
    "financialInstitutionIdentification": {
      "bicfi": "TESTBICA"
    }
  },
  "debtor": {
    "name": "Giannis",
    "postalAddress": {
      "addressLine": ["New Saints 23"]
    }
  },
  "debtorAccount": {
    "identification": {
      "iban": "GR1601101250000000012400695"
    }
  },
  "debtorAgent": {
    "financialInstitutionIdentification": {
      "bicfi": "BANKSBIC"
    }
  },
  "creditor": {
    "name": "Jim",
    "postalAddress": {
      "addressLine": ["Pelasgias 54"]
    }
  },
  "creditorAccount": {
    "identification": {
      "iban": "GR1601101250000000012300695"
    }
  },
  "creditorAgent": {
    "financialInstitutionIdentification": {
      "bicfi": "TESTBICA"
    }
  },
  "remittanceInformation": {
    "unstructured": ["I want to pay an invoice"]
  }
}
```

## Sample Success Response
{
"status": "OK",
"payload": 4,
"errorCode": null,
"errors": null
}
