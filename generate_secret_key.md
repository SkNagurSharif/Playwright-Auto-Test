# Generating a Secret Key for Azure DevOps Authentication

## Overview
This document outlines the steps to generate a secret key for Azure DevOps (ADO) authentication, which is essential for accessing resources behind Azure federated MFA.

## Steps to Generate a Secret Key

1. **Access Azure DevOps**:
   - Log in to your Azure DevOps account.

2. **Navigate to the Project**:
   - Go to the specific project where you want to generate the secret key.

3. **Open the Project Settings**:
   - Click on the gear icon (⚙️) in the lower-left corner to access the project settings.

4. **Select Security**:
   - In the project settings menu, find and select the "Security" option.

5. **Generate a New Key**:
   - Look for the option to generate a new key or secret. This may be labeled as "New Key" or "Generate Secret Key."
   - Follow the prompts to create a new key. You may need to provide a name and specify the permissions for the key.

6. **Copy the Secret Key**:
   - Once the key is generated, make sure to copy it immediately. You will not be able to see it again after you navigate away from the page.

7. **Store the Secret Key Securely**:
   - Store the secret key in a secure location, such as an Azure Key Vault or in a `.env` file in your project (ensure this file is not committed to version control).

## Example of Using the Secret Key
Once you have generated and stored your secret key, you can use it in your application for authentication. Here’s an example of how to set it in your `.env` file:

```env
# .env file
SECRET_KEY=your_generated_secret_key_here
```

## Conclusion
Generating a secret key for Azure DevOps authentication is a crucial step for accessing secured resources. Ensure that you follow best practices for storing and using the key to maintain the security of your application.
