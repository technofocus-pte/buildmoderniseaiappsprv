# Usecase 02 - Build a Fruits List Quarkus web app with Azure App Service on Linux and PostgreSQL

**Estimated duration:** 40 minutes

**Lab Type:** Instructor Led

**Objective:**

This usecase shows how to build, configure, and deploy a secure Quarkus
application in Azure App Service that's connected to a PostgreSQL
database (using Azure Database for PostgreSQL). Azure App Service is a
highly scalable, self-patching, web-hosting service that can easily
deploy apps on Windows or Linux. When you're finished, you'll have a
Quarkus app running on Azure App Service on Linux.

**Pre-requisites:**

**GitHub account** -- You are expected to have your own GitHub login
credentials. If you do not have, please create one from here
- !!https://github.com/signup?user_email=&source=form-home-signup!!
  	
## Exercise 1: Run the sample

First, you set up a sample data-driven app as a starting point. The
sample repository we are using here includes a dev container
configuration. The dev container has everything you need to develop an
application, including the database, cache, and all environment
variables needed by the sample application. The dev container can run in
a GitHub codespace, which means you can run the sample on any computer
with a web browser.

1.  From a browser, sign in to your GitHub
    account !!**https://github.com/login**!!.

2.  Open this url from a new
    tab, !!**https://github.com/technofocus-pte/msdocs-quarkus-postgresql-sample-app**!!.

3.  Select **Fork -\> Create a new fork**.

    ![](./media/image1.jpeg)

4.  Click on **Create fork** in the Create a new fork page.

    ![](./media/image2.jpeg)

5.  In the forked page of the repo, select **Code** \> **Create
    codespace on main**.

    ![](./media/image3.jpeg)

    **Note:** If Create Codespace on main option does not show up, click on
the + symbol next to Codespaces.

    ![](./media/image4.jpeg)

    **Note:** The codespace creation takes around 10 minutes to set up.

    ![](./media/image5.jpeg)

6.  Execute !!mvn quarkus:dev!! in the Terminal. Click on **Allow** in the
    pop up.

    ![](./media/image6.jpeg)

    ![](./media/image7.jpeg)

7.  When you see the notification, **Your application running on port
    8080** is available., select **Open in Browser**. You should see the
    sample application in a new browser tab.

    If you see a **notification** with port **5005**, **skip** it.

    ![](./media/image8.jpeg)

    ![](./media/image9.jpeg)

8.  To stop the Quarkus development server, type **Ctrl+C** in the
    Codespace terminal.

    ![](./media/image10.jpeg)

## Exercise 2: Create App Service and PostgreSQL

First, you create the Azure resources. The steps used in this lab create
a set of secure-by-default resources that include App Service and Azure
Database for PostgreSQL.

1.    Open the Azure portal at !!https://portal.azure.com/!! and **login** with the Azure login credentials from the **Home** tab of the VM.

   ![](./media/Picture3.png)

2.  Select **Cancel** or the close button in the Welcome page.

    ![](./media/image12.jpeg)

3.  Enter !!**web app database**!! in the search bar at the top of the Azure
    portal. Select the item labelled **Web App + Database** under
    the **Marketplace** heading.

    ![](./media/image13.jpeg)

4.  On **Create Web App + Database**, fill in the below details and
    select **Review + create**

    | **Property**   |  **Value**  |
    |:-------|:-------|
    |  Subscription  |  Select your **assigned subscription**  |
    | Resource group   |  Select your **assigned Resource group**  |
    |  Region  |  Select nearest Location  |
    | **Web App Details**   |    |
    | Name   |  Enter !!quarkuwebappXXXX!!  |
    | Runtime stack   |  **Java 17**  |
    |  **Database**  |    |
    |  Engine  |  Select **PostgreSQL – Flexible Server**  |
    |  Hosting Plan  |  Select **Basic**  |
    
    ![](./media/Picture4.png)

    ![](./media/image15.jpeg)

6.  Once the validation passes, click on **Create**.

    ![](./media/Picture5.png)

    **Note:** The app creation takes around 15 minutes.

7.  Once the deployment is complete, click on **Go to resource**.

    ![](./media/image17.jpeg)

8.  You're taken directly to the **App Service page.** Click
    on **Home** at the top left corner.

    ![](./media/image18.jpeg)

9.  Click on the Portal menu and select **Resource Groups** from it.

    ![](./media/image19.jpeg)

10.  Select the Resource group assigned to you and see that the
    following resources are created from the deployment that we just
    performed.

    - App Service plan
    
    - App Service
    
    - Virtual network
    
    - Azure Database for PostgreSQL flexible server
    
    - Private DNS zone

   ![](./media/Picture6.png)

## Exercise 3: Verify connection settings

The creation wizard generated the connectivity variables for you already
as app settings. In this step, you learn where to find the app settings,
and how you can create your own.

1.  Click on the **App Service** from the list of resources in the
    Resource group.

    ![](./media/image21.jpeg)

2.  In the App Service page, from the left menu, select **Environment
    variables** under **Settings**.

3.  In the **App settings** tab of the **Environment variables** page,
    verify that **AZURE_POSTGRESQL_CONNECTIONSTRING** is present. It's
    injected at runtime as an environment variable.

    ![](./media/image22.jpeg)

4.  Select **+ Add**.

    ![](./media/image23.jpeg)

5.  Name the setting !!**PORT**!! and set its value to !!**8080**!!,
    which is the default port of the Quarkus application.
    Select **Apply**.

    ![](./media/image24.jpeg)

6.  Select **Apply**.

    ![](./media/image25.jpeg)

7.  Select **Confirm**.

    ![](./media/image26.jpeg)

8.  You will get a notification stating that the app settings has been
    updated.

    ![](./media/image27.jpeg)

## Exercise 4: Deploy sample code

In this step, you'll configure GitHub deployment using GitHub Actions.
It's just one of many ways to deploy to App Service, but also a great
way to have continuous integration in your deployment process. By
default, every git push to your GitHub repository will kick off the
build and deploy action.

1.  In the App Service page, from the left menu, select **Deployment
    Center** under **Deployment**.

    ![](./media/image28.jpeg)

2.  In Source, select **GitHub**. By default, GitHub Actions is selected
    as the build provider.

    ![](./media/image29.jpeg)

3.  Click on **Authorize** and sign in to your GitHub account and follow
    the prompt to authorize Azure.

    ![](./media/image30.jpeg)

4.  Fill in the details as below, leave the remaining to the default and
    click on **Save**.

    |  **Property**  | **Value**   |
    |:--------|:---------|
    |  Organization  |  Your GitHub account  |
    |  Repository  |  Select **msdocs-quarkus-postgresql-sample-app**  |
    |  Branch  |   **main** |
    
    ![](./media/image31.jpeg)

5.  Once **Save** is clicked on, App Service commits a workflow file
    into the chosen GitHub repository, in the .github/workflows
    directory.

6.  Back in the GitHub codespace of your sample fork, run !!**git pull origin main**!!. This pulls the newly committed workflow file into your codespace.

    >[!Note] **Note:** If you find test cases still running in the terminal, you can press Ctrl+C and then execute the above command.

   ![](./media/image32.jpeg)

7.  Open **src/main/resources/application.properties** in the explorer.
    Quarkus uses this file to load Java properties.

8.  Find the code (lines 10-11). This code sets the production variable
    **%prod.quarkus.datasource.jdbc.url** to the app setting that the
    creation wizard for you. The **quarkus.package.type** is set to build an
    Uber-Jar, which you need to run in App Service.

    ![](./media/image33.jpeg)

9.  Open **.github/workflows/main_quarkuwebapp[lab instance id].yml** in
    the explorer. This file was created by the App Service create
    wizard.

11. Under the Build with Maven step, change the Maven command to !!**mvn clean install -DskipTests**!!.

    **-DskipTests** skips the tests in your Quarkus project, to avoid the
GitHub workflow failing prematurely.

    ![](./media/image34.jpeg)

12. Select the **Source Control** extension.

    ![](./media/image35.jpeg)

13. In the textbox, type a commit message like !!**Configure DB and
    deployment workflow**!!. Select **Commit**, then confirm
    with **Yes**.

    ![](./media/image36.jpeg)

14. Select **Sync changes 1**, then confirm with **OK**.

    ![](./media/image37.jpeg)

    ![](./media/image38.jpeg)

15. Back in the Deployment Center page in the Azure portal,
    Select **Logs**. A new deployment run would have already started from your
    committed changes.

16. In the log item for the deployment run, select the **Build/Deploy
    Logs** entry with the latest timestamp.

    ![](./media/image39.jpeg)

17. You're taken to your GitHub repository and see that the GitHub
    action is running. The workflow file defines two separate stages,
    build and deploy. Wait for the GitHub run to show a status of
    Complete. It takes about 5 minutes.

    ![](./media/image40.jpeg)

## Exercise 5: Browse to the app

1.  From the Azure portal(!!https://portal.azure.com!!), open Resource group **ResourceGroup1** and select the **App Service** resource.

    ![](./media/Picture7.png)

2.  From the left menu, select **Overview** and select the URL of your
    app under **Default domain**.

    ![](./media/image42.jpeg)

3.  Paste the copied url in a new browser to open the app.

    ![](./media/image43.jpeg)

4.  Add a few fruits to the list. Now, you're running a web app in Azure
    App Service, with secure connectivity to Azure Database for
    PostgreSQL.

    ![](./media/image44.jpeg)

    ![](./media/image45.jpeg)

## Exercise 6: Stream diagnostic logs

Azure App Service captures all messages output to the console to help
you diagnose issues with your application. The sample application
includes standard JBoss logging statements to demonstrate this
capability as shown below.

1.  From the Azure portal App Service page, from the left menu,
    select **App Service logs** under **Monitoring**.

    ![](./media/image46.jpeg)

2.  Under **Application logging**, select **File System**. In the top
    menu, select **Save**.

    ![](./media/image47.jpeg)

3.  From the left menu, select **Log stream**. You see the logs for your
    app, including platform logs and logs from inside the container.

    ![](./media/image48.jpeg)

## Exercise 7: Clean up resources

1.  From the Azure portal Home page, select Resource groups.

    ![](./media/image49.jpeg)

2.	Select the **NetworkWatcherRG** and click on **Delete resource group**.

    ![](./media/image57.png)

3.	Type !!NetworkWatcherRG!! in the text box and click on **Delete**.
 
    ![](./media/image58.png)

    ![](./media/image59.png)
  
4.	Next, from the Resource group page, select you assigned Resource group.

    ![](./media/Picture8.png)

5.	Select all the **resources**, and then select **Delete**.

    ![](./media/Picture9.png)

6.	Type in !!**delete**!! in the text box and click on **Delete**.

    ![](./media/Picture10.png)

    ![](./media/Picture11.png)

7.	A success notification on the deleted resources confirms the deletion.

8.	Back in the GitHub Workspace, click on the drop down next to **Code**, select the three dots next to the codespace name and click on **Delete**.
   
    ![](./media/image64.jpeg)

**Summary:**

We have learnt to deploy a secure Quarkus application in Azure App
Service, connected it to PostgreSQL database to add Fruit names from the
app's UI.

