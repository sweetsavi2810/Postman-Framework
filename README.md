# 🚀 Postman API Testing Framework

This repository provides a **generic API testing framework** built with:

-   🧪 Postman Collection
-   🌍 Postman Environment
-   ⚡ Newman CLI
-   🔄 CI/CD integration via GitHub Actions
-   🔄 CI/CD integration via Azure DevOps

It enables teams to: - Develop API tests locally in Postman - Execute
them via Newman - Automatically run tests in CI/CD pipelines

------------------------------------------------------------------------

## 📁 Repository Structure

-    Postman Framework.postman_collection.json 
-    Postman dev.postman_environment.json 
-    dev-postman-api-Github-pipelines.yaml
-    dev-postman-api-azure-pipelines.yaml
-    README.md 

------------------------------------------------------------------------

## 1️⃣ Postman Collection

File: `Postman Framework.postman_collection.json`

Contains:

-   OAuth2 Access Token (Client Credentials flow)
-   HTTP Method validation (GET, POST, PUT, PATCH, DELETE)
-   Postman Collection API CRUD testing
-   Response validation:
    -   Status code checks
    -   JSON property validation
    -   Schema validation
    -   Contract testing
    -   Environment/global variable handling

Dynamic variables used:

-   `{{client_id}}`
-   `{{client_secret}}`
-   `{{scope}}`
-   `{{URL}}`
-   `{{URLCOLL}}`
-   `{{postman-api-key}}`

------------------------------------------------------------------------

## 2️⃣ Postman Environment

File: `Postman dev.postman_environment.json`

Defined variables:

  Variable          Description
  ----------------- ----------------------------
  URLEcho           Echo test service base URL
  URLCOLL           Postman API base URL
  postman-api-key   Postman API Key

Values can be configured locally or injected via CI/CD secrets.

------------------------------------------------------------------------

## 3️⃣ CI/CD Pipeline (GitHub Actions)

File: `dev-postman-api-Github-pipelines.yaml`

Pipeline behavior:

-   Triggers on push to `developement` branch
-   Installs Node.js
-   Installs Newman
-   Injects GitHub Secrets
-   Runs Postman collection
-   Fails build if any test fails

### Required GitHub Secrets

URLCOLL\
CLIENTID\
CLIENTSECRET\
SCOPE\
JFROG_TOKEN (if internal artifact repo is used)

------------------------------------------------------------------------

## 🧪 Running Tests Locally

### Install Newman

npm install -g newman

### Run Collection

newman run "Postman Framework.postman_collection.json" -e "Postman
dev.postman_environment.json"

### Run with Environment Variables

newman run "Postman Framework.postman_collection.json"\
-e "Postman dev.postman_environment.json"\
--env-var client_id=YOUR_ID\
--env-var client_secret=YOUR_SECRET\
--env-var scope=YOUR_SCOPE\
--env-var URL=YOUR_URL

------------------------------------------------------------------------

## 🔄 CI/CD Execution Flow

1.  Push to `developement`
2.  GitHub Action triggers
3.  Node.js installed
4.  Newman installed
5.  Secrets injected
6.  Tests executed
7.  Build fails if tests fail

------------------------------------------------------------------------

## 🏗 Azure DevOps Integration

Steps:

-   Add Node.js task
-   Install Newman globally
-   Add Command Line task:

newman run Postman Framework.postman_collection.json -e Postman
dev.postman_environment.json

Store secrets in:

-   Variable Groups
-   Azure Key Vault (recommended)

------------------------------------------------------------------------

## 🧩 Framework Capabilities

✔ OAuth2 Client Credentials flow\
✔ Environment-based configuration\
✔ Global variable handling\
✔ JSON Schema validation\
✔ Dynamic request chaining\
✔ Full CRUD API validation\
✔ CI/CD ready\
✔ Easily extendable

------------------------------------------------------------------------

## 🔒 Security Best Practices

-   Do NOT commit secrets
-   Use CI/CD secret management
-   Rotate credentials regularly
-   Use scoped API keys

------------------------------------------------------------------------

## 📌 Customization Guide

To adapt this framework:

1.  Replace base URLs
2.  Modify authentication flow if needed
3.  Update test scripts
4.  Add service-specific folders
5.  Enable additional reporters

Example:

newman run collection.json -r cli,html,junit
