---
title: "Getting Started"
weight: 11
---

This workshop will walk you through deploying and testing the **AWS Payment Accelerator React App** — a modern, user-friendly interface for initiating and tracking payment transactions.

---

## What You'll Learn

- Set up and run the app locally
- Integrate the payment API
- Deploy to AWS Amplify
- Monitor successful payments using Aplon Hub

---

## Folder Structure

This project includes the following key folders and files:

- **static/** – Static assets such as images and screenshots.
- **content/** – Workshop markdown content displayed in the browser sidebar.
- **assets/** – Media assets used within the workshop (like screenshots of the app).
- **contentspec.yaml** – Holds reusable parameter values like app name and URLs.
- **preview_build.exe** – Used to launch the workshop locally for preview.

---

## Prerequisites

Before starting, ensure you have the following:

- [Node.js](https://nodejs.org/) (v16+ recommended)
- [Git](https://git-scm.com/)
- A modern code editor (e.g., [VS Code](https://code.visualstudio.com/))
- Access to your GitHub repo:  
  👉 **[https://github.com/brillio-PES/aws-payment-gateway](https://github.com/brillio-PES/aws-payment-gateway)**

---

## Run the Local Preview

You can preview this workshop locally using the AWS Workshop Studio preview build tool:

```powershell
PS> & "$env:USERPROFILE\Downloads\preview_build.exe"
```
