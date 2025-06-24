---
title: Deploying the Payment Transfer App
description: Instructions to deploy the React-based CBPR+ Payment Transfer app using AWS Amplify.
---

In this section, you’ll deploy your **React-based CBPR+ Payment Transfer** application to the cloud using **AWS Amplify**. Once deployed, the app will be accessible through a public web URL and ready to initiate real payment transfers through the Aplonhub Brillio API.

---

## ✅ Prerequisites

Before you begin:

- ✅ AWS account with admin permissions
- ✅ GitHub repository with your application code or build artifacts for your application
- ✅ Application built with [React](https://reactjs.org/)
- ✅ API environment ready (e.g. `https://aplonhub-brillio.pc14.eu`)
- ✅ Environment variable: `REACT_APP_API_BASE_URL=https://aplonhub-brillio.pc14.eu`

---

## 🧭 Deployment Approaches

This workshop supports multiple ways to deploy your React app using AWS Amplify. Choose the one that fits your setup:

---

### 🔗 **Approach 1: Deploy via GitHub Repository**

## 🧭 Step-by-Step Deployment Guide

### 🔗 Step 1: Connect Repository to AWS Amplify

1. Go to [AWS Amplify Console](https://console.aws.amazon.com/amplify/home).
2. Click **"Create new app"**.
3. Choose source code provider (e.g., GitHub). Click **"Next"** and authorize Amplify.
   ![Amplify1 Screen](/static/images/amplify1-screen.png)
4. Select your repo and branch (e.g., `main`).
   ![Amplify2 Screen](/static/images/amplify2-screen.png)
5. Click **"Next"**.

---

### ⚙️ Step 2: App Settings - Advanced Settings

Add Environment Variable

1. Go to App Settings → Environment Variables.
2. Add the following:
   REACT_APP_API_BASE_URL=https://aplonhub-brillio.pc14.eu
3. Click **"Next"**.
   ![Amplify Screen3](/static/images/amplify3-screen.png)

This environment variable is used in your app to connect to the Aplonhub CBPR+ API.

### 🚀 Step 4: Deploy the App

1. After Review click **"Save and Deploy"**.
   ![Amplify Screen4](/static/images/amplify4-screen.png)

2. Amplify will:

- Clone your repo
- Install dependencies
- Build the app
- Host it on a public URL

This process may take a few minutes.

### 🌍 Step 5: Access Your Application

Once deployment is complete, you’ll get a live URL like:

https://main.<your-app-id>.amplifyapp.com

Visit this URL to open your deployed payment transfer application.

### 🔁 Step 6: Continuous Deployment

Every push to the connected Git branch (e.g. main) will:

- Automatically trigger a rebuild
- Redeploy the latest version of your app
- No need to redeploy manually for every change!

### 📦 **Approach 2: Deploy via S3 (Build Folder Upload)**

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

### 📦 **Approach 3: Deploy via S3 + AWS CloudFormation Template**

This approach is useful when setting up infrastructure as code (IaC) for reproducible environments. You can automate your deployment by uploading a source ZIP + CloudFormation template to S3, then launching a stack in the CloudFormation Console.

### 🔗 Step 1: Upload the following to an S3 bucket:

react-app-source.zip (excluding node_modules) [Download Source Code](/assets/source-code.zip)

template.yaml (CloudFormation template that references the ZIP) [Download cloudformation-template.yaml](/assets/cloudformation-template.yaml)

<details>

```yaml
AWSTemplateFormatVersion: "2010-09-09"
Description: >
  Create CodeCommit repo from S3, deploy to AWS Amplify, and inject an environment variable.

Parameters:
  AppName:
    Type: String
    Description: Name for the Amplify App and CodeCommit Repo

  S3Bucket:
    Type: String
    Description: The S3 bucket containing the ZIP archive

  S3Key:
    Type: String
    Description: The ZIP file key in the S3 bucket (e.g., my-app.zip)

  RepoBranch:
    Type: String
    Default: main
    Description: Name of the branch in CodeCommit

  APIBaseURL:
    Type: String
    Default: https://aplonhub-brillio.pc14.eu
    Description: Value of the environment variable (REACT_APP_API_BASE_URL)

Resources:
  AppRepository:
    Type: AWS::CodeCommit::Repository
    Properties:
      RepositoryName: !Ref AppName
      Code:
        S3:
          Bucket: !Ref S3Bucket
          Key: !Ref S3Key
        BranchName: !Ref RepoBranch

  AmplifyApp:
    Type: AWS::Amplify::App
    DependsOn: AppRepository
    Properties:
      Name: !Ref AppName
      Repository: !Sub https://git-codecommit.${AWS::Region}.amazonaws.com/v1/repos/${AppName}
      Platform: WEB
      BuildSpec: |
        version: 1
        frontend:
          phases:
            preBuild:
              commands:
                - npm ci
            build:
              commands:
                - echo "Building with MY_ENV_VAR=$MY_ENV_VAR"
                - npm run build
          artifacts:
            baseDirectory: build
            files:
              - '**/*'
          cache:
            paths:
              - node_modules/**/*
      EnvironmentVariables:
        - Name: REACT_APP_API_BASE_URL
          Value: !Ref APIBaseURL

  AmplifyBranch:
    Type: AWS::Amplify::Branch
    Properties:
      AppId: !GetAtt AmplifyApp.AppId
      BranchName: !Ref RepoBranch
      EnableAutoBuild: true

Outputs:
  AmplifyAppId:
    Description: The ID of the Amplify App
    Value: !GetAtt AmplifyApp.AppId

  AmplifyBranchName:
    Description: The name of the Amplify branch deployed
    Value: !Ref AmplifyBranch
```

</details>

### 🔗 Step 2: Go to AWS CloudFormation Console > Click on Create Stack

![Create Stack Screen](/static/images/create-stack.png)

### 🔗 Step 3: In Create Stack > Choose an existing template

### 🔗 Step 4: In Specify template > "Amazon S3 URL" and provide the path to your template. Click "Next"

![Create Stack1 Screen](/static/images/stack-step1.png)

### 🔗 Step 5: In Specify stack details > Provide a stack name. In Parameters > Provide APIBaseURL, AppName, RepoBranch, S3Bucket and S3Key (Refer Screenshot). Click "Next"

![Specify Stack1 Screen](/static/images/stack-step2.png)

![Specify Stack2 Screen](/static/images/stack-step3.png)

### 🔗 Step 6: Review and create stack. After successful stack creation, go to Amplify Console > All apps > Hosting: Build settings > Edit build spec (Refer Screenshot). Click "Save"

![Build Screen](/static/images/build-setting.png)

### 🔗 Step 7: Select the newly created Amplify environment and finish deployment.

![CF Screen](/static/images/cf-deployment.png)

### 🌍 Step 8: Access Your Application

Once deployment is complete, you’ll get a live URL like:

https://main.<your-app-id>.amplifyapp.com

Visit this URL to open your deployed payment transfer application.

### 🧪 Step 9: Verify Functionality

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
