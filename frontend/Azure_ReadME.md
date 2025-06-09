# Azure DevOps Setup Guide

This guide will help you set up your Azure DevOps project and configurations for CI/CD pipeline integration.

## Prerequisites
- Azure DevOps account
- Azure subscription with:
  - Azure Container Registry (ACR)
  - Azure App Service
  - Proper IAM permissions for service principal
- GitHub account

## Step 1: Create Azure DevOps Organization and Project

1. Go to [Azure DevOps](https://dev.azure.com)
2. Click "Sign in" and use your Microsoft account
3. Click "New organization"
   - Fill in organization details
   - Choose a unique organization name
   - Select your country/region
4. Create a new project:
   - Click "New project"
   - Name your project (e.g., "ReactApp")
   - Choose "Git" as version control
   - Click "Create"

## Step 2: Create Variable Group

1. Go to your project in Azure DevOps
2. Click "Project Settings" (gear icon)
3. Under "Pipelines", click "Variable groups"
4. Click "Add variable group"
5. Name it "ReactAppVariables"
6. Add these variables:
   ```
   ACR-LoginServer: yourregistry.azurecr.io
   ACR-Name: yourregistry
   ```
   - Replace `yourregistry` with your actual Azure Container Registry name

## Step 3: Create Azure Subscription Service Connection

1. In Project Settings
2. Under "Pipelines", click "Service connections"
3. Click "New service connection"
4. Select "Azure Resource Manager"
5. Click "Next"
6. Choose "Service principal (automatic)"
7. Select your Azure subscription
8. Click "Finish"

## Step 4: Create Azure Container Registry Service Connection

1. In Project Settings
2. Under "Pipelines", click "Service connections"
3. Click "New service connection"
4. Select "Azure Container Registry"
5. Click "Next"
6. Select your Azure subscription
7. Select your ACR
8. Click "Finish"

## Step 5: Verify Setup

1. Ensure your Azure DevOps organization has access to your Azure subscription
2. Verify both service connections are working by:
   - Testing the connection in the service connection settings
   - Checking the connection status in the Azure portal
3. Check that the variable group is properly configured by:
   - Verifying the variables are correctly set
   - Testing the values in a pipeline run

## Step 6: Push Code to GitHub

Initialize your repository:
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin <your-github-repo-url>
git push -u origin main
```

## Step 7: Connect GitHub to Azure DevOps

1. In Azure DevOps
2. Go to "Repos"
3. Click "Import repository"
4. Select "GitHub"
5. Connect your GitHub account
6. Select your repository
7. Click "Import"

## Pipeline Configuration

The pipeline will automatically trigger when you push changes to the main or develop branches. Ensure your Azure subscription has:

- Azure Container Registry (ACR)
- Azure App Service
- Proper IAM permissions for the service principal

## Troubleshooting Tips

1. If service connections fail:
   - Verify Azure subscription permissions
   - Check if the service principal has proper IAM permissions
   - Ensure the Azure subscription is active

2. If pipeline fails:
   - Check if all required variables are set
   - Verify service connections are working
   - Check pipeline logs for detailed error messages

3. If GitHub connection fails:
   - Verify GitHub repository permissions
   - Check if the repository URL is correct
   - Ensure you have proper access to the repository

## Security Best Practices

1. Never commit sensitive information to the repository
2. Use variable groups for storing sensitive values
3. Regularly review and rotate service connection credentials
4. Implement proper access control for your Azure resources

## Next Steps

1. Set up your CI/CD pipeline configuration
2. Configure environment variables
3. Set up deployment slots if needed
4. Implement proper monitoring and logging