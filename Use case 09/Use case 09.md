
# Usecase 09 - Building a Chat bot experience using Azure Cosmos DB for MongoDB and Azure OpenAI Service

**Objective:**

This usecase will create an intelligent solution that combines
vCore-based Azure Cosmos DB for MongoDB vector search and document
retrieval with Azure OpenAI services to build a chat bot experience.

![](./media/image1.jpeg)

**Key technologies used** -- Azure OpenAI Service, Azure Cosmos DB,
ChatGPT model

**Estimated duration** -- 60 minutes

**Lab Type** -- Instructor led

**Important:** If any of the commands does not get **pasted** in
the **PowerShell**, please open a notepad, keep the cursor at an empty
space of the notepad and then click on the T button of the command to be
pasted. The contents will get copied to the notepad and then you can
copy and paste from the notepad onto the PowerShell.


## Exercise 1: Provision Azure resources

### Task 1: Create Azure resources using script

1.	Login to Azure portal at !!**https://portal.azure.com**!! and login using your Azure login credentials from the **Home** tab.
   
2.	From Azure portal, select your subscription. From the left pane, select Resource providers under Settings, select !!**Microsoft.Alertsmanagement**!! and click on **Register**.

    ![](./media/pic100.jpg)

3.  From the VM, search for !!**power shell**!!, right click on **Windows
    PowerShell** and select **Run as administrator**. Click
    on **Yes** in the confirmation dialog.

    ![](./media/image2.jpeg)

    ![](./media/image3.jpeg)

4.  Execute the below command to install Az in the PowerShell.

    !!**Install-Module Az**!!

    Select **A** (Yes to all) when prompted.
    
    **Note:** This will take upto 5 minutes to complete.

    ![](./media/image4.jpeg)
    
    ![](./media/image5.jpeg)

5.  Once done, execute the below command to import the Az module.

    !!**Import-Module Az**!!

    ![](./media/image6.jpeg)

6.  Execute the below command to use browser-based sign-in

    !!Update-AzConfig -EnableLoginByWam $false!!

    ![](./media/image7.jpeg)

7.  Execute the below command and select your Azure login if prompted,
    to login to Azure.

    !!Connect-AzAccount!!
    
    ![](./media/image8.jpeg)

8.  Execute the below commands to navigate to the **LabFiles** folder.

    !!cd\\!!
    
    !!cd LabFiles\\'Build a Chat bot'\Labs\deploy!!

    ![](./media/image9.jpeg)

9.  Execute the below command to install **Microsoft
    Bicep** using **winget**.

    !!winget install -e --id Microsoft.Bicep!!
    
    Type **Y** if prompted.
    
    ![](./media/image10.jpeg)

10.  **Close** the PowerShell and **open** it again.

11.  Execute the below command and select your Azure login if prompted,
    to login to Azure.

    !!Connect-AzAccount!!

12. Execute the below commands to navigate to the **LabFiles** folder.

    !!cd\\!!
    
    !!cd LabFiles\\'Build a Chat bot'\Labs\deploy!!

    ![](./media/image9.jpeg)

13. Execute the below command to set the Subscription ID.

    !!Set-AzContext -SubscriptionId < Subscription id >!!
    
    ![](./media/image12.jpeg)

14.	Open the file **azuredeploy.bicep** in the path **C:\LabFiles\Build a Chat bot\Labs\deploy**, and replace the letters **dgxxxxxxx** at line 35 with !!dg< Random Number >!!. At line **74**, update the version as !!**0125**!!.

    ![](./media/pic1.png)

    ![](./media/img41.png)
   	
16.	Execute the below command to deploy the resources like Azure Cosmos DB workspace, Azure OpenAI in Azure. 
   	
    ```
   New-AzResourceGroupDeployment -ResourceGroupName < RG Name > -TemplateFile .\azuredeploy.bicep -TemplateParameterFile .\azuredeploy.parameters.json -c
    ```

    >[!Note] **Note:** The deployment will take around 10 to 15 minutes. 
    If there is an issue with the deployment and it fails, execute the same deployment command again.

    >[!Note] **Note:** Type Y when prompted.

   ![](./media/image14.jpeg)
    
   ![](./media/image15.jpeg)

    >[!Note] **Note:** If there is no update in the PowerShell after 15 to 20 minutes, check under Resource Group -> Deployments in the Azure portal or hit **Enter** in the **PowerShell** window.

### Task 2: Check the created resources in Azure

1.  Login to **Azure portal** at !!https://portal.azure.com/!! using
    your **Azure login credentials**. Select **Resource groups**.

    ![](./media/image16.jpeg)

2.  From the Resource groups list, select **assigned Resource Group**.

    ![](./media/Picture23.png)

3.  Notice that a set of resources including **Azure OpenAI
    resource**, **App Service**, **Azure Cosmos DB for MongoDB** are
    created.

    ![](./media/Picture54.png)

4.  Click on the **Azure OpenAI** resource.

    ![](./media/Picture55.png)

5.  Select **Keys and Endpoint** under **Resource Management**.

    ![](./media/image20.jpeg)

6.  Copy and save the **Key 1** and **Endpoint** in a notepad for later
    reference.

    ![](./media/image21.jpeg)

7.  Back in the resource group page, select
    the **Azure Cosmos DB for Mongo DB** resource.

    ![](./media/Picture53.png)

8.  Click on **Connection strings** under **Settings**. Copy the value of Self (always this cluster.

    ![](./media/image99.jpg)

9.  Copy the connection string and paste it in a notepad. Replace the
    \< **password** \> with !!**myMongoDB98**!! in the copied
    connection string and save it in the notepad.

## Exercise 2: Explore and use Azure OpenAI models from code

### Task 1: Set up the Environment

1.  From the lab VM windows search bar, search for !!Visual studio
    code!! and open **Visual Studio Code**.

    ![](./media/image24.jpeg)

2.  Click on **Open Folder**. (If it does not pop up, select **File -\>
    Open Folder**)

    ![](./media/image25.jpeg)

3.  Navigate to **C:\Labfiles**, click on **Build a Chat bot** folder
    and select **Select Folder.**

    ![](./media/image26.jpeg)

4.  Click on **Yes, I trust the Authors** in the pop up.

    ![](./media/image27.jpeg)

5.  From Visual Studio Code,
    open **lab_0_explore_and_use_models.ipynb** from
    the **Labs** folder.

    ![](./media/image28.jpeg)

6.  Click on **Select Kernel.**

7.  Select **Install** in the **Do you want to install the recommended
    extensions for Python** pop up.

    ![](./media/image29.jpeg)

8.  Click on **Allow access** if prompted.

    ![](./media/image30.jpeg)

9.  Click on **Select Kernel**. Select **Python Environments** and
    then **Python 3.12.3** or higher that gets listed as
    the **Suggested** or **Recommended** option.

    ![](./media/image31.jpeg)
    
    ![](./media/image32.jpeg)

10. Open the **.env** file

11. Replace **DB_CONNECTION
    STRING**, **AOAI_KEY** and **AOAI_Endpoint** that we saved in
    the **notepad** earlier in Task 2 of Exercise 1.

    ![](./media/image36.jpeg)

Now, the environment variables are set to point to the Azure resources
that we have created already.

### Task 2: Execute the code

1.  Back in the **Lab 0 ipynb** file, **execute** the **first cell** by
    clicking on the Play button, to install the latest OpenAI client
    library.

    ![](./media/image37.jpeg)
    
    ![](./media/image38.jpeg)

2.  **Execute** the next cell to install the **Python-dotenv**

    ![](./media/image39.jpeg)

3.  Press **Ctrl+Shift+P**, type !!Reload Window!! and select
    Developer:Reload Window option that gets listed.

    ![](./media/image40.jpeg)

4.  Execute from the **first cell** again.

5.  **Execute** the next cell to import the required OpenAI library, os
    to access the environment variables and dotenv to load the
    environment variables from .env file.

    ![](./media/image41.jpeg)

6.  **Execute** the next cell to create the **Azure OpenAI client** to
    call the Azure OpenAI Chat completion API:

    ![](./media/image42.jpeg)

7.  **Execute** the next cell to call
    the **.chat.completions.create()** method on the client to perform
    a **chat completion**. You should get a chat response.

    ![](./media/image43.jpeg)

## Exercise 3: First Cosmos DB for MongoDB API application

This exercise will cover how to create your first Cosmos DB project.
We'll use a notebook to demonstrate the basic CRUD operations.

1.  Open the file **lab_1_first_application.ipynb** from
    the **Labs** folder.

2.  Click on **Select kernel** and choose the **Python version**.

    ![](./media/image44.jpeg)

3.  **Execute** the first cell to do install **pymongo**.

    ![](./media/image45.jpeg)

4.  **Execute** the next cell to do the required **imports**

    ![](./media/image46.jpeg)

5.  Execute the next cell to **Create a database.**

    >[!Note] **Note:** This will use the connection string that we updated in the
.env file

    ![](./media/image47.jpeg)

6.  **Execute** the next cell to create a **collection**.

    ![](./media/image48.jpeg)

7.  **Execute** the next cell to create a **document**. One method of
    creating a document is using the insert_one method. This method
    takes a single document and inserts it into the database.

    ![](./media/image49.jpeg)

8.  **Execute** the next cell to **retrieve a single document** from the
    database. The **find_one** method is used here for this purpose.

    ![](./media/image50.jpeg)

9.  **Execute** the next cell in which **find_one_and_update** method is
    used to update a single document in the database.

    ![](./media/image51.jpeg)

10. **Execute** the next cell in which **delete_one** method is used to
    delete a single document from the database.

    ![](./media/image52.jpeg)

11. The **find** method is used to query for multiple documents in the
    database. **Execute** the **next 3 cells** one by one to see it in
    action.

    ![](./media/image53.jpeg)
    
    ![](./media/image54.jpeg)

    ![](./media/image55.jpeg)
    
    ![](./media/image56.jpeg)

12. The following cell will **delete** the database and collection
    created in this exercise. This is done by using
    the **drop_database** method on the database object

    ![](./media/image57.jpeg)

## Exercise 4: Load data into Cosmos DB using the MongoDB API

The previous exercise demonstrated how to add data to a collection
individually. This exercise will demonstrate how to load data using bulk
operations into multiple collections. This data will be used in
subsequent labs to explain further the capabilities of Azure Cosmos DB
API for MongoDB about AI.

This notebook demonstrates how to load data into Cosmos DB from Cosmic
Works JSON files into the database using the MongoDB API.

1.  Open the file **lab_2_load_data.ipynb** from the **Labs** folder.
    Click on **Select Kernel** and select the **Python version**.

    ![](./media/image58.jpeg)

2.  Execute the first cell to install **requests**.

    ![](./media/image59.jpeg)

3.  **Execute** the next cell to do the required **imports**.

    ![](./media/image60.jpeg)

4.  **Execute** the next cell which establishes a **connection** with
    the **database**.

    ![](./media/image61.jpeg)
    
    ![](./media/image62.jpeg)

5.  **Execute** the next cell to **load** the **products**.

    ![](./media/image63.jpeg)

6.  **Execute** the next cells
    to **load** the **customers** and **sales** **raw data**. In this
    repository, the customer and sales data are stored in the same file.
    The type field is used to differentiate between the two types of
    documents.

    ![](./media/image64.jpeg)
    
    ![](./media/image65.jpeg)
    
    ![](./media/image66.jpeg)

7.  **Execute** the next cell to **clean up**.

    ![](./media/image67.jpeg)

## Exercise 5: Vector Search using vCore-based Azure Cosmos DB for MongoDB

1.  Open the
    file **lab_3_mongodb_vector_search.ipynb** from **Labs** folder.

2.  Click on **Select Kernel** and select the **Python version**.

    ![](./media/image68.jpeg)

3.  **Execute** the first cell to install **tenacity**.

    ![](./media/image69.jpeg)

4.  **Execute** the next cell to perform the required **imports**.

    ![](./media/image70.jpeg)

5.  **Execute** the next cell to **load** the **settings** from the .env
    file.

    ![](./media/image71.jpeg)

6.  Execute the next cell to establish **connectivity** to
    the **database**.

    ![](./media/image72.jpeg)

7.  **Execute** the next cell to establish **Azure OpenAI
    connectivity**.

    ![](./media/image73.jpeg)

8.  The process of creating a vector embedding field on each document
    only needs to be done once. However, if a document changes, the
    vector embedding field will need to be updated with an updated
    vector. It is done in the next two cells. **Execute** the next two
    cells and observe the **embeddings** obtained as output in the
    second one.

    ![](./media/image74.jpeg)
    
    ![](./media/image75.jpeg)

9.  **Execute** the next cell to **Vectorize and update all documents in
    the Cosmic Works database.**

    ![](./media/image76.jpeg)

10. **Execute** the next **3** cells to add **vector
    fields** to **products, customer and sales documents.**

   **Note:** The first cell will take around 5 minutes, second one around 3 minutes and the third one around 20 minutes to complete execution.

    ![](./media/image77.jpeg)

11. **Execute** the next cell to create **products vector index**.

    ![](./media/image78.jpeg)
    
    ![](./media/image79.jpeg)

12. Now that each document has its associated vector embedding and the
    vector indexes have been created on each collection, we can now use
    the vector search capabilities of vCore-based Azure Cosmos DB for
    MongoDB. **Execute** the next **3** cells.

    ![](./media/image80.jpeg)
    
    ![](./media/image81.jpeg)
    
    ![](./media/image82.jpeg)

13. **Execute** the next cells to observe the usage of **vector search
    results** in a RAG pattern with Chat GPT-3.5

    ![](./media/image83.jpeg)
    
    ![](./media/image84.jpeg)
    
    ![](./media/image85.jpeg)

14. Observe the output of the following cells.

    ![](./media/image86.jpeg)
    
    ![](./media/image87.jpeg)

## Exercise 6: Delete the deployed resources

1.	From the Azure portal(!!https://portal.azure.com!!), select the resource group assigned.

    ![](./media/Picture24.png)

2.	Select all the resources under it, click on the **three dots** in the menu and select **Delete** to delete all the resources.

    ![](./media/Picture25.png)

3.	Type !!delete!! in the text box and click on the Delete button.
 
    ![](./media/Picture26.png)

4.  Once the resources are deleted, from the Azure portal home page,
    search for !!**Azure AI Services**!! and select it.

    ![](./media/image91.jpeg)

5.  Select **Azure OpenAI** from the left pane and then select **Manage
    deleted resources**.

    ![](./media/image92.jpeg)

6.  Select the resource that gets listed there and then click
    on **Purge**.

    ![](./media/image93.jpeg)

7.  Click on **Yes**.

    ![](./media/image94.jpeg)

**Summary:**

You have successfully created a solution with Azure Cosmos DB for
MongoDB vector search and document retrieval with Azure OpenAI services.

