# Module 00 - Deployment and Setup

## Introduction

In this Module, you'll confirm the deployment of Azure Services needed to run this workshop then start the application to ensure everything has been properly configured.

1. Open the folder on the desktop *LabUser - Shortcut*
1. Navigate to the *multi-agent-hol* folder.
1. If it is empty or does not exist, proceed to [Git Clone](#git-clone)
1. If the folder exists and has files within it proceed to the next step.
1. Open a browser locally on the VM and navigate to https://portal.azure.com
1. In the Search box at the top of the Azure Portal, type in resource group. Open the Resource groups blade
1. Look for a resource group that starts with: *rg-agenthol-*.
1. If the resource group does not appear wait a few moments then refresh.
1. If after a few minutes, the resource group does not appear, proceed to [Lab Provisioning](#lab-provisioning)
1. When the new resource group appears, expand the Overview tab and click deployments.
![essentials-tab-deployments](./media/module-00/essentials-tab-deployments.png)
1. If all resources have been deployed successfully, you are ready to begin the lab. Your screen should look like this.
![deployments](./media/module-00/deployments.png)
1. Proceed to [Running the App](#running-the-app)

## Git Clone

1. Open the PowerShell terminal on the Start bar.
1. Navigate to the LabUser folder.
1. Clone the GitHub repository for this lab.

```shell
git clone --branch hol --single-branch https://github.com/AzureCosmosDB/banking-multi-agent-workshop.git C:\Users\LabUser\multi-agent-hol
```

1. Proceed to [Lab Provisioning](#lab-provisioning)

## Lab Provisioning

1. Open the PowerShell terminal on the Start Bar and navigate to the multi-agent-hol folder.

```shell
cd C:\Users\LabUser\multi-agent-hol\
```

1. Authenticate  yourself

```shell
azd auth login
```

1. Deploy the Azure services using `azd up`

```shell
azd up
```

1. For environment name enter: `agenthol`
1. Press enter to select the subscription listed.
1. Press enter to select the default region listed.

1. Return to the Azure Portal and refresh the list of resource groups. You may need to refresh a few times.
1. Select the *rg-agenthol* resource group.
1. Find the collapsed *Essentials* section at the top of the page and expand.
1. Click on the Deployments and watch until the status of all deployed resources shows as Succeeded.
1. Your screen should appear as below.

![deployments](./media/module-00/deployments.png)

## Running the App

### 1. Start the Backend App

1. Open the PowerShell terminal on the Start bar.
1. Navigate to `C:\Users\LabUser\multi-agent-hol\csharp\src\MultiAgentCopilot`.
1. Type `code .`
1. Open the Terminal in VS Code.
1. Type `dotnet run` to start the multi-agent service.
1. You will notice some warnings when the app starts. You can ignore these.
1. Leave the app running.

### 2. Run the Frontend App

1. Within VS Code, open a new terminal.
1. Navigate to the `frontend` folder, `cd C:\Users\LabUser\multi-agent-hol\frontend`
1. Copy and run the following:

   ```sh
   npm install
   npm start
   ```

1. If prompted, **Allow** so the Node.js Javascript Runtime to access this app over the network.
1. Open your browser and navigate to <http://localhost:4200/>.

### 3. Start a Conversation

1. In the Login dialog, select a user and company and click, Login.
1. Start a new conversation.
1. Send the message:

   ```text
   Hello, how are you?
   ```

1. You should see something like the output below.

   ![Test output](./media/module-00/test-output.png)

### 4. Stop the Application

- Return to VS Code.
- In the frontend terminal, press **Ctrl + C** to stop the frontend application.
- Select the backend terminal, press **Ctrl + C** to stop the backend application.

## Common Issues and Troubleshooting

1. Errors during azd deployment:
   - Service principal "not found" error.
   - Rerun `azd up`
1. Frontend issues:
   - If frontend doesn't fully start, navigate to `/frontend/src/environments/environment.ts` and update `apiUrl: 'https://localhost:63279/'`
   - Frontend will restart

## Next Steps

Proceed to Module 1: [Creating Your First Agent](./Module-01.md)
