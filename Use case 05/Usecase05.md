# Usecase 05- Deploying a data-driven Python Restaurant web app with the Azure Database for PostgreSQL

**Objective:**

This usecase deploy a Python web app using the Flask framework and the Azure Database for PostgreSQL relational database service. The Flask app is hosted in a fully managed Azure App Service. This app is designed to be run locally and then deployed to Azure

![](./media/image1.jpeg)

You 'll deploy a data-driven Python web app (**Django** or **Flask**) to **Azure App Service** with the **Azure Database for
PostgreSQL** relational database service. Azure App Service supports Python in a Linux server environment.

**Key technologies used** -- Java 17, Azure Database for PostgreSQL

**Estimated duration** -- 45 minutes

**Lab Type:** Instructor Led

**Pre-requisites:**

GitHub account -- You are expected to have your own GitHub login credentials. If you do not have, please create one from here
- **https://github.com/signup?user_email=&source=form-home-signupobjectives**

The **requirements.txt** has the following packages, all used by a typical data-driven Flask application:


### Task 1 : Register Service provider

1.  Open a browser go to ``https://portal.azure.com`` and sign in with your cloud slice account below.

 Username: !!Cloudsliceuser!! 

 Password: !!PWD!!

2.  Click on **Subscriptions** tile.

 ![](./media/image6.png)

3.  Click on the subscription name.

 ![](./media/image7.png)

4.  Expand Settings from the left navigation menu. Click on **Resource providers**, enter !!Microsoft.AlertsManagement!! and select it, and then click **Register**.

  ![](./media/image8.png)

  ![](./media/image9.png)

### Task 2 : Create GitHub Codespace to initiate the Azure Developer CLI template

This use case has a dev container configuration, which makes it easier to develop apps locally, deploy them to Azure, and monitor them. We use
Azure development CLI templates to deploy apps

1.  Open a browser go to !!https://github.com!! and sign in with your GitHub account.

2.  Fork this repository !!https://github.com/technofocus-pte/flask-postgresql-CSTesting.git!! to your account by clicking on **Fork** as shown in the below image.

  ![](./media/image10.jpeg)

3.  Enter a unique name and then click on **Create repo**.

  ![](./media/image11.jpeg)

4.  From the repository root of your fork, select **Code** > **Codespaces** > **+**.

  ![](./media/image12.jpeg)

5.  Wait for the workspace to set up.

  ![](./media/image13.jpeg)

  ![](./media/image14.jpeg)

6.  In the codespace terminal, run the following commands:

 !!python3 -m pip install -r requirements.txt!!

  ![](./media/image15.jpeg)

7.  Run the below command to create an environment variable

 !!cp .env.sample.devcontainer .env!!

  ![](./media/image16.jpeg)

8.  Run below command for data migration

  !!python3 -m flask db upgrade!!

  ![](./media/image17.jpeg)

9.  Run the below command to Start the development server

 !!python3 -m flask run!!

 ![](./media/image18.jpeg)

10. When you see the message your application running on the port is available, click **Open in Browser**.

 ![](./media/image18.jpeg)

 ![](./media/image19.jpeg)

 ![](./media/image20.jpeg)

11. Click on **Add new restaurant** button.

 ![](./media/image21.jpeg)

12. Enter the details below and click on the **Submit** button.

 Name : !!Contoso Rica!!

 Street Adress - !!3A ,8th cross, Ferns street , Singapore!!

 Description - !!This is a medium to high-priced restaurant in the city shopping center!!

 ![](./media/image22.jpeg)

13. Click on **Add new review** button.

 ![](./media/image23.jpeg)

14. Enter your review and then click on the button. **Save changes**

 **Your name: your name**

 **Rating: your rating**

 ``This is a medium to high priced restaurant in the city shopping center. Service was a little bit confusing as we had at least 6 waiters
 coming to ask us things. Food took some time to come. We had 2 menus: one indian and one thai. The thai is 30% cheaper so we went for some
 appetizers and thai red curry. Food took some time but it was worth it. It was delicious and very well prepared. Overall, this is a good
 eat.``

 ![](./media/image24.jpeg)

 ![](./media/image25.jpeg)

15. Add some more reviews and new restaurants with comments.

 ![](./media/image26.jpeg)

### Task 3: Provision of required resources in Azure.

This project is designed to work well with the Azure Developer CLI which makes it easier to develop apps locally, deploy them to Azure, and
monitor them.

1.  Switch back to the GitHub code space tab, Run the below command to Initialize a new azd environment:

 !!azd init!!

 ![](./media/image27.jpeg)

2.  It will prompt you to provide an environment name - +++flask-app@lab.LabInstance.Id+++ , which will
    later be used in the name of the deployed resources.

  ![](./media/image28.jpeg)

3.  Login if required +++azd auth login+++ Copy the code and press enter.

  ![](./media/image29.jpeg)

4.  Enter the code and then sign in with your Azure credentials.

  Username: !!@lab.CloudPortalCredential(User1).Username!!  
 
  Password: !!@lab.CloudPortalCredential(User1).Password!!

  ![](./media/image30.jpeg)

  ![](./media/image31.jpeg)

  ![](./media/image32.jpeg)

  ![](./media/image33.jpeg)

5.  Switch back Gtihub codespace tab and run below command to provision and deploy all the resources. It will prompt to select your Azure
    subscription. Enter **1** to select your subscription and press Enter.

  !!azd provision!!

  ![](./media/image34.png)

6.  Select location as **@lab.CloudResourceGroup(ResourceGroup1).Location**. Then it will provision the resources in your account and deploy the latest code. 

  ![](./media/image35.png)

7.  Enter the resource group name below  and press enter.

   !!@lab.CloudResourceGroup(ResourceGroup1).Name!!

  ![](./media/image36.png)

8.  Deployment takes **20 - 30 minutes**. You can also check the status of deployment at the generated link or **Azure portal-> Resource
    group-> Deployments**.

  ![](./media/image37.png)

  ![](./media/image38.png)

  ![](./media/image39.png)

  ![](./media/image40.png)

### Task 4 : Deploy the application from Github

1.  Press Ctrl + C  and run the below command to set the resource group environment variable.

   !!azd env set AZURE_RESOURCE_GROUP @lab.CloudResourceGroup(ResourceGroup1).Name!!

   ![](./media/image41.png)

2.  Run the below command to deploy all resources and wait for the deployment to complete successfully.

    !!azd deploy!!

    ![](./media/image42.png)

3.  Click on the generated Endpoint URL

    ![](./media/image43.png)

4.  Click on **Open** to open the external website.

    ![](./media/image44.png)

5.  The app opens in a new tab.

    ![](./media/image45.png)

### Task 5 : Stream diagnostic logs

Azure App Service captures all messages output to the console to help you diagnose issues with your application. The app includes print()
statements to demonstrate this capability as shown below.

@app.route('/', methods=['GET'])

def index():

print('Request for index page received')

restaurants = Restaurant.query.all()

return render_template('index.html', restaurants=restaurants)

1.  Switch back to **Azure portal- > Resource group** and click on **App service**.

    ![](./media/image46.png)

2.  On the App Service page. From the left menu, select **Monitoring ->** **App Service logs.**

    ![](./media/image47.png)

3.  Under **Application logging**, make that that the toggle is set to **File System**. If it is not then select it and then select **Save**.

    ![](./media/image48.png)

4.  From the left menu, select **Log stream**. You see the logs for your app, including platform logs and logs from inside the container.

    ![](./media/image49.png)

### Task 6 : Clean up resources in Github.

1.  Switch back to Github, and click on **repo -> Code -> Codespaces.** Select the correct branch

   ![](./media/image50.png)

2.  Select the branch and click on **Delete**.

   ![](./media/image51.png)

3.  Click on **Delete**.

   ![](./media/image52.png)

4.  Switch back to **Azure portal -> Resource group.**

   ![](./media/image53.png)

5.  Select all the resources and then click on **Delete** ( DO NOT delete resource group)

   ![](./media/image54.png)

6.  Enter ``Delete`` and then click on **Delete**.

   ![](./media/image55.png)

7.  Click on **Delete** to confirm deletion.

   ![](./media/image56.png)
