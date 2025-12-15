# Exercise 1: Embedding Creation

### Estimated Duration: 120 Minutes

In this exercise, you will gain hands-on experience in setting up a comprehensive Azure-based environment for embedding creation and document processing. The exercise is structured into two main parts:

- **Configuring Azure Resources:** You will deploy and configure essential Azure services, including Azure OpenAI, Azure AI Search (Formerly known as Cognitive Search), Document Intelligence (Formerly known as Form Recognizer), and Translator. These resources are critical for the effective generation and management of document embeddings.

- **Deploying Azure Functions:** You will implement Azure Functions to automate and optimize the document processing pipeline. This involves configuring functions to handle document extraction, translation, embedding generation, and query processing.

## Lab objectives

In this exercise, you will complete the following tasks:

- Task 1: Deploy Azure OpenAI and Models
- Task 2: Create Azure AI Search Resources
- Task 3: Deploy Azure Function with Embeddings

## Task 1: Deploy Azure OpenAI and Models

In this task, you will begin by deploying an Azure OpenAI resource through the Azure portal. This involves creating an OpenAI resource, configuring it with the appropriate settings, and deploying models such as **gpt-4.1** and **text-embedding-3-small** using Azure AI Foundry portal.

Azure OpenAI offers a web-based portal called **Azure AI Foundry portal** for deploying, managing, and exploring models. Follow these steps to deploy a model using Azure AI Foundry portal:

### Deploy Azure OpenAI Resource

1. On the Azure portal, type **Azure OpenAI (1)** in the search box and select **Azure OpenAI (2)** from the results.

    ![](./media/openai1upd.png)

1. On the **Microsoft Foundry | Azure OpenAI blade**, in the left pane under **Use with AI Foundry**, select **Azure OpenAI (1)**. Then click **+ Create (2)**, and from the dropdown, choose **Azure OpenAI (3)**.

    ![](./media/l12-12-01.png)

1. On the **Basics** tab of **Create Azure OpenAI** resource page, enter the following details and click on **Next (6)** button.
   
    - **Subscription**: Default - Pre-assigned subscription  (1)
    
    - **Resource group**: Select **Openai-embedded-<inject key="Deployment ID" enableCopy="false"></inject>  (2)**
    
    - **Region**: Select **<inject key="Region" enableCopy="false" />**  **(3)**
    
    - **Name**: **Openai-<inject key="Deployment ID" enableCopy="false"></inject>  (4)**
    
    - **Pricing tier**: **Standard S0 (5)**

      ![](./media/am23.png)

1. On the **Network** tab, leave the value as default and click on **Next** button.

    ![](./media/am3.png)

1. On the **Tags** tab, leave the value as default and click on **Next** button.

    ![](./media/am4.png)
  
1. On the **Review + submit** tab, review the configuration, and click on **Create** button.

    ![](./media/am24.png)

1. Once the deployment is complete, click on the **Go to resource** button.
   
    ![](./media/24-07-2024(6).png)

1. On the Azure OpenAI resource, select **Keys & Endpoint (1)** under the **Resource Management** section from the left menu, click **Show Keys (2)**, copy **KEY 1 (3)**, and store them in a notepad for later use.

    ![](./media/lop-01.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide. 
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.
<validation step="76158c08-a6fe-4e2f-ba59-d6556a5a88e4" />

### Deploy Models in Azure AI Foundry portal

1. Go to the Azure OpenAI Overview page, and click **Go to Azure AI Foundry portal** to navigate to the Azure AI Foundry portal.

    ![](./media/ee4.png)

1. In the Azure AI Foundry portal, navigate to **Deployments (1)**, select **+ Deploy model (2)**, and then choose **Deploy base model (3)**.

    ![](./media/ee5.png)

1. On the Select a model page, search for **gpt-4.1 (1)**, select **gpt-4.1 (2)**, and click **Confirm (3)**.

    ![](./media/l1-12-1.png)    

1. In the Deploy model pop-up, enter the following details and click on the **Deploy (4)** button.
    
    - Deployment name: **gpt-4.1**

    - Deployment type: **Standard (1)**

    - Click on **Customize** to expand the menu.
    
    - Model version: **2025-04-14 (Default) (2)**

    - Tokens per Minute Rate Limit (thousands): **40K  (3)**

      ![](./media/l1-12-2.png) 

      >**Note:** Copy the deployment name **gpt-4.1** and save it in Notepad. Will use it later in the lab.

1. Repeat the process to create another deployment.

1. In the Azure AI Foundry portal, navigate to **Deployments (1)**, select **+ Deploy model (2)**, and then choose **Deploy base model (3)**.

    ![](./media/aifoundry2upd.png)

1. On the **Select a model** page, search for **text-embedding-3-small (1)**, select **text-embedding-3-small (2)**, and click **Confirm (3)**.

    ![](./media/l1-12-3.png)   

1. In the Deploy model pop-up, enter the following details and click on the **Deploy (4)** button.

    - Deployment name: **text-embedding-3-small**

    - Deployment type: **Standard (1)**

    - Click on **Customize** to expand the menu.

    - Model version: **1 (Default) (2)**
    
    - Tokens per Minute Rate Limit (thousands): **40K (3)**

      ![](./media/l1-12-4.png)  

      >**Note:** Copy the deployment name **text-embedding-3-small** and save it in Notepad. You will use it later in the lab.

## Task 2: Create Azure AI Search Resources

In this task, you will create the required Azure resources for AI Search, Document Intelligence, and Translator services. This involves setting up each service with the correct configurations, including subscription, resource group, and pricing tier, to support the document processing pipeline.

### Create AI Search Service

1. On the Azure portal, type **AI Search (1)** in the search box and select **AI Search (2)** from the results.

    ![](./media/am5.png)

1. On the **Microsoft Foundry | AI Search** blade, click on **+ Create**.

    ![](./media/l1-12-5.png)

1. On the **Basics** tab of **Create a search service** resource page, enter the following details:
   
    - Subscription: Default - **Pre-assigned subscription (1)**
    
    - Resource Group: **Select Openai-embedded-<inject key="Deployment ID" enableCopy="false"></inject> (2)**

    - Service name: **aisearch-<inject key="Deployment ID" enableCopy="false"></inject> (3)**
    
    - Location: Select **<inject key="Region" enableCopy="false" /> (4)**
    
    - Pricing tier: **Standard (5)**

    - Click on **Review + create (6)**

      ![](./media/am6.png)

      >**Note:** if you are not able to deploy resource in **East US** kindly select **East US 2** and deploy.

1. Review the configuration, and click on **Create** button.

     ![](./media/am25.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide. 
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.
<validation step="c27751de-8370-4a29-92b9-c79ee1e1e436" />

### Create Document Intelligence Resource

1. On the Azure portal, type **Document intelligence (1)** in the search box and select **Document intelligences (2)** from the results.

    ![](./media/am7.png)

1. On the **Microsoft Foundry | Document intelligence** blade, click on **+ Create**.

    ![](./media/l12-12-02.png)

1. On the **Basics** tab of **Create Document Intelligence** resource page, enter the following details:
   
    - Subscription: Default - **Pre-assigned subscription (1)**
    
    - Resource group: Select **Openai-embedded-<inject key="Deployment ID" enableCopy="false"></inject> (2)**
    
    - Region: Select **<inject key="Region" enableCopy="false" /> (3)**
    
    - Name: **Document-intelligence-<inject key="Deployment ID" enableCopy="false"></inject> (4)**
    
    - Pricing tier: **Standard S0 (1 Call per minute for training API) (5)**

      ![](./media/am8.png)
        
1. Click on **Review + create** button, review the configuration, and click on **Create** button.

    ![](./media/am26.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide. 
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.
<validation step="a4912828-00ad-4dde-83a3-75feb53266d3" />

### Create Translator Resource

1. On the Azure portal, type **Translators (1)** in the search box and select **Translators (2)** from the results.

    ![](./media/am9.png)

1. On the **Microsoft Foundry | Translator** blade, click on **+ Create**.

    ![](./media/l1-12-6.png)

1. On the **Basics** tab of **Create Translator** resource page, enter the following details:
   
    - Subscription: **Default - Pre-assigned subscription (1)**
    
    - Resource group: **Openai-embedded-<inject key="Deployment ID" enableCopy="false"></inject> (2)**
    
    - Region: Select **<inject key="Region" enableCopy="false" /> (3)**
    
    - Name: **Translator-<inject key="Deployment ID" enableCopy="false"></inject> (4)**
    
    - Pricing tier: **Standard S1 (Pay as you go) (5)**

    - Click on **Review + create (6)** button

      ![](./media/am10.png)
    
1. Review the configuration, and click on **Create** button.

    ![](./media/am27.png)

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide. 
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.
<validation step="f7eb2333-4b72-4cdb-809d-fd4c522ff2aa" />

## Task 3: Deploy Azure Function with Embeddings

In this task, you will deploy Azure Functions that automate the document processing workflow.

1. From the LabVM, open **File Explorer** by selecting its icon on the Windows Taskbar.

    ![](./media/12.png)

1. Navigate to `C:\LabFiles` **(1)** and double-click on the `deploy-01.json` **(2)** file to open it. Select **Notepad (3)** and click **OK (4)**. Copy the template in Notepad for future deployment.

    ![](./media/am12.png)

1. Navigate back to the Azure Portal, type **Deploy a custom template (1)** in the search box and select **Deploy a custom template (2)** from the results.

    ![](./media/am13.png)

1. On the **Custom deployment** page, click on **Build your own template in the editor**.

    ![](./media/am14.png)

1. Paste the template you copied in step 2, in the ARM template editor, locate the **OpenAIEngine** parameter and set the **defaultValue** **(line no: 97)** to `gpt-4.1` **(1)**. Also verify that **OpenAIDeploymentType** **(line no: 104)is set to `Chat` **(2)**.

     ![](./media/l12-12-03.png)

1. Scroll down to the embeddings section and ensure both **OpenAIEmbeddingsEngineDoc** **(1)** and **OpenAIEmbeddingsEngineQuery** **(2)** have the **defaultValue** **(line no: 111 and 118)**set to `text-embedding-3-small`.

     ![](./media/l12-12-04.png)

1. Click on the **Save** button.

    ![](./media/24-07-2024(33).png)

1. On the **Basics** tab of **Custom deployment** page, enter the required details given below:

    |Variables	|Values|
    |---|---|
    |**Subscription** | Default - Pre-assigned subscription |
    |**Resource group** | Openai-embedded-<inject key="Deployment ID" enableCopy="false"></inject> |
    |**Region** | <inject key="Region" enableCopy="false" /> |
    |**Azure AI Search** | aisearch-<inject key="Deployment ID" enableCopy="false"></inject> |
    |**Azure AI Search Sku**| standard |
    |**Hosting Plan Name** | hostingplan-<inject key="Deployment ID" enableCopy="false"></inject> |
    |**Hosting Plan Sku** | B3 |
    |**Storage Account Name** | storage<inject key="Deployment ID" enableCopy="false"></inject> |
    |**Function Name** | Functionapp-<inject key="Deployment ID" enableCopy="false"></inject> |
    |**Application Insights Name** | Application-insights-<inject key="Deployment ID" enableCopy="false"></inject> |
    |**Document Intelligence** |Document-intelligence-<inject key="Deployment ID" enableCopy="false"></inject> |
    |**Translator Name** | Translator-<inject key="Deployment ID" enableCopy="false"></inject> |
    |**Open AI Name** | Openai-<inject key="Deployment ID" enableCopy="false"></inject> |
    |**Open AI Key** | Paste the OpenAI key that you copied in task 1 |

      ![](./media/23052025(2).png)

1. Leave the other value as default and click on **Review + create** button, review the configuration, and click on **Create** button.

    ![](./media/23052025(3).png)

1. Once the deployment is complete, click on the **Go to resource group** button.

    ![](./media/24-07-2024(37).png)

1. On the **Overview** page of **Openai-embedded-<inject key="Deployment ID" enableCopy="false"></inject>** resource group, click on **Functionapp-<inject key="Deployment ID" enableCopy="false"></inject>** function app resource.

    ![](./media/rgfunction.png)

1. On the Overview page of **Functionapp-<inject key="Deployment ID" enableCopy="false"></inject>** page, review the three functions that are present under the **Functions** tab.

    ![](./media/24-07-2024(39).png)

1. The Azure Functions are triggered at different stages. Please find it in detail:

    - **BatchStartProcessing**: When a document is uploaded to Azure Storage, it automatically triggers this Azure Function. This function acts as the initial step in the document processing pipeline. Here's how it works:

        - A blob trigger is set up on the Azure Function.
        - As soon as a new file is added to the specified Azure Storage container, the function is activated.
        - This function then initiates the document extraction process using Document intelligence.

    - **BatchPushResults**: Once the paragraphs are extracted from the document, this Azure Function is triggered. This function handles two tasks:

        - If required, it translates the extracted text using Azure Translator.
        - It then converts the processed text into embeddings using the Azure OpenAI Service.
        - This function could be triggered by a queue message or by the completion of the first function.

    - **ApiQnA**: When a user submits a search query, this Azure Function is triggered. This function performs several crucial steps:

        - It processes the user's query, potentially cleaning or formatting it.
        - It performs a vector search using the query against the stored embeddings.
        - It then uses Azure OpenAI to generate a comprehensive answer based on the search results.
        - Finally, it returns this answer to the user.

1. In the left-hand menu, select **Environment variables (1)** under **Settings** section and click on **Advanced edit (2)** at the top of the page to view or modify the environment variables.

    ![](./media/am15.png)

1. Copy all the values displayed in the environment variables section and paste them into Notepad for the next exercise.

> **Congratulations** on completing the task! Now, it's time to validate it. Here are the steps:
> - If you receive a success message, you can proceed to the next task.
> - If not, carefully read the error message and retry the step, following the instructions in the lab guide. 
> - If you need any assistance, please contact us at cloudlabs-support@spektrasystems.com. We are available 24/7 to help you out.
<validation step="da23d4f2-068b-4149-8071-9870b25d261d" />

## Summary

In this exercise, you have accomplished the following:

- Provisioned an Azure OpenAI resource
- Deployed an OpenAI model within the Azure AI Foundry portal
- Integrated Azure OpenAI models into your applications

### Click on **Next >>** to proceed to the next exercise.

![](./media/lab-02.png)