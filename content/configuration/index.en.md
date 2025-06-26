---
title: Deploying the Payment Transfer App
description: Instructions to deploy the React-based CBPR+ Payment Transfer app using AWS Amplify.
---

In this section, you’ll deploy your **React-based CBPR+ Payment Transfer** application to the cloud using **AWS Amplify**. Once deployed, the app will be accessible through a public web URL and ready to initiate real payment transfers through the aplonHUB Brillio API.

---

## ✅ Prerequisites

Before you begin:

- ✅ AWS account with admin permissions
- ✅ Build artifacts for your application
- ✅ Application built with [React](https://reactjs.org/)
- ✅ API environment ready (e.g. `https://aplonhub-brillio.pc14.eu`)

---

### 📦 **Deploy via S3 (Build Folder Upload)**

This approach is useful when you don't want to connect a Git provider. If you have a build folder ready from running npm run build, you can:

### 🔗 Step 1: Upload your React app build folder to an S3 bucket. [Download Build](/assets/build.zip)

### 🔗 Step 2: Go to AWS Amplify Console > Create New App > Deploy without Git > Click **"Next"**.

![Amplify5 Screen](/static/images/amplify5-screen.png)

### 🔗 Step 3: Provide App name and Choose "Amazon S3" as the method.

### 🔗 Step 4: Click on Browse S3 and Provide S3 location of objects to host by Selecting the S3 bucket containing your build output.

![Amplify6 Screen](/static/images/amplify6-screen.png)

### 🔗 Step 5: Click Save and Deploy.

### 🌍 Step 6: Access Your Application

Once deployment is complete, you’ll get a live URL like:

https://staging.<your-app-id>.amplifyapp.com

Visit this URL to open your deployed payment transfer application.

### 🧪 Step 7: Verify Functionality

Check the following:

✅ App loads without errors

✅ Payment form renders correctly

✅ Submitting the form triggers the API call

✅ Success screen is shown after response

Post-Deployment Checklist
Once deployed:

✅ Your app should be accessible via a public Amplify URL

✅ Confirm API calls are working using browser DevTools

✅ Use the app to simulate or initiate test payment transfers

```

```
