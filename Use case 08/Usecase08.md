# Usecase 08 - Building and deploying Contoso Real Estate chat app to support customers.

**Objective**

This usecase demonstrates a few approaches for creating ChatGPT-like experiences over your own data using the Retrieval Augmented Generation
pattern. It uses Azure OpenAI Service to access the ChatGPT model (gpt-35-turbo), and Azure AI Search for data indexing and retrieval.

![](./media/image1.jpeg)

The usecase includes sample data so it's ready to try end to end. In this sample application we use a fictitious company called Contoso Real
Estate, and the experience allows its customers to ask support questions about the usage of its products. The sample data includes a set of
documents that describe its terms of service, privacy policy and a support guide.

The application is made from multiple components, including:

- **Search service**: the backend service that provides the search and
  retrieval capabilities.

- **Indexer service**: the service that indexes the data and creates the
  search indexes.

- **Web app**: the frontend web application that provides the user
  interface and orchestrates the interaction between the user and the
  backend services.

![](./media/image2.jpeg)

- Chat and Q&A interfaces

- Explores various options to help users evaluate the trustworthiness of
  responses with citations, tracking of source content, etc.

- Shows possible approaches for data preparation, prompt construction,
  and orchestration of interaction between model (ChatGPT) and retriever
  (Azure AI Search)

- Settings directly in the UX to tweak the behavior and experiment with
  options

- Optional performance tracing and monitoring with Application Insights

**Key technologies used** -- Azure OpenAI Service, ChatGPT model (gpt-35-turbo), and Azure AI Search

**Estimated duration --** 40 minutes

## Exercise 1 : Deploy the application and test it from the browser

### Task 1: Open development environment

1.  Open your browser, navigate to the address bar, type or paste the following
    URL: ``https://github.com/technofocus-pte/azure-search-openai-javascr-CSTestingipt.git`` and sign in with your Github account.

  ![](./media/image3.jpeg)

2.  Click on **Fork**.

  ![](./media/image4.jpeg)

3.  Enter the repository name and then click on **Create fork**.

  ![](./media/image5.jpeg)

4.  Click on **Code -> Codespaces -> +**

  ![](./media/image6.jpeg)

5.  Wait for the environment to set up. It takes 5-10 minutes.

  ![](./media/image7.jpeg)

### Task 2: Provision required services to build and deploy chat app to Azure

1.  Run the following command on the Terminal. Copy the code and press enter.

  +++azd auth login+++

  ![](./media/image8.png)

2.  The default browser opens to enter a code. Enter the copied code and click **Next**.

  ![](./media/image9.png)

3.  Sign in with your Azure credentials.

  Username: +++@lab.CloudPortalCredential(User1).Username+++  

  Password: +++@lab.CloudPortalCredential(User1).Password+++

  ![](./media/image10.png)

  ![](./media/image11.png)

4.  Switch back to GitHub Codespace tab. Run below command to Initialize the project environment in the current directory. Enter the  Environment name as +++ucragpgpy@lab.LabInstance.Id+++ and press Enter.this env is unique and generated as per your  loginid. please use same env name.

  +++azd env new+++

  ![](./media/image12.png)

5.  Run the below command to provision the services to Azure, build your container.

  ![](./media/image13.png)

6.  Select the below values.

  +++azd provision+++

- **Select an Azure Subscription to use** : select your subscription

- **Select an Azure location to use** : **@lab.CloudResourceGroup(ResourceGroup1).Location** (Please use this region only as this is your resource group region)

- Select existing resource group: Your existing resource group
  
    +++@lab.CloudResourceGroup(ResourceGroup1).Name+++

  ![](./media/image14.png)

7.  Wait for the resource to be provisioned completely. This process will take 5-10 min to create all the required resources.

  ![](./media/image15.png)

### Task 3: Deploy the chat app and explore it

1. Run the below command to set the resource group environment variable.

   +++azd env set AZURE_RESOURCE_GROUP @lab.CloudResourceGroup(ResourceGroup1).Name+++
   
3. Run the below command to deploy the app.

  +++azd deploy+++

  ![](./media/image16.png)

2. Wait for the deployment.It takes < 5 minutes.

  ![](./media/image17.png)

3. Click on the endpoint url generated.(redeploy by running +++azd deploy+++ if your app is not working)

  ![](./media/image18.png)

4. Click on **Open**.

  ![](./media/image19.png)

5. It opens the app in a new tab.

  ![](./media/image20.png)

6. Select **How to search and book rental?** Container and then click on the enter button next to the text box.

  ![](./media/image21.png)

### Task 4: Clean up all the resources

1.  Switch back to **Azure portal -> Resource group-> Resource group name.**

  ![](./media/image22.png)

2.  Select all the resources and then click on Delete as shown in the below image. (**DO NOT DELETE** resource group)

  ![](./media/image23.png)

3.  Type ``delete`` on the text box and then click on **Delete**.

  ![](./media/image24.png)

4.  Confirm the deletion by clicking on **Delete**.

  ![](./media/image25.png)

5.  Switch back to the Github portal tab and refresh the page.

  ![](./media/image26.png)

6.  Click on Code , select the branch created for this lab, and click on **Delete**.

  ![](./media/image27.png)

7.  Confirm the branch deletion by clicking on **Delete** button.

  ![](./media/image28.png)

### Summary:
This use case thought you , deploying a chat application for the Retrieval Augmented Generation pattern running on Azure, using Azure AI Search for retrieval and Azure OpenAI and LangChain large language models (LLMs) to power ChatGPT-style and Q&A experiences
