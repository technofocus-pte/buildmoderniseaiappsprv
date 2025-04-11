
# Usecase 04 - Build a TODO List ASP.NET app, deploy it to Azure App Service connecting to SQL Database

**Estimated duration:** 40 minutes

**Lab Type:** Instructor Led

**Objective:**

Azure App Service provides a highly scalable, self-patching web hosting
service. In this lab, you will learn how to deploy a data-driven ASP.NET
app in App Service and connect it to Azure SQL Database. When you\\re
finished, you have an ASP.NET app running in Azure and connected to SQL
Database.

## Exercise 1: Deploying an ASP.NET app to Azure with Azure SQL Database

### Task 1: Set up Visual Studio 2022 and run the application

1.  From the Windows **Search** bar, type !!**Visual studio**!! and select Visual Studio 2022. If it asks you to Sign in, continue with the steps 2 and 3 or continue from Step 4.

    ![](./media/image1.jpeg)

2.	Click on **Sign in** and and **sign in** with the **Username** and **password** under the **User Credentials** section in the Home tab of the VM.

    ![](./media/image2.jpeg)

    ![](./media/Picture12.png)

3.  Select **Start Visual Studio**.

    ![](./media/image4.jpeg)

4.  Select **Open a local folder**.

    ![](./media/image5.jpeg)

5.  Select **webappwithsqldb** folder in **C:\Labfiles** and click
    on **Select Folder**.

    ![](./media/image6.jpeg)

6.  Once the folder is opened, double click
    on **DotNetAppSqlDb.sln** from the **Solution Explorer**.

    **Note:** If the Solution Explorer does not get opened automatically,
Click on **View -\> Solution Explorer.**

    ![](./media/image7.jpeg)

7.  Click on **Build** -\> **Build Solution**.

    ![](./media/image8.jpeg)

8.  Once the Build is completed, select **Debug -\>** **Start
    Debugging**.

    ![](./media/image9.jpeg)

    ![](./media/image10.jpeg)

9.  This opens up a browser with the **Todos web app** running in it.

    ![](./media/image11.jpeg)

10. Add few items into the app by clicking on **Create New** as in the
    screenshots below.

    ![](./media/image12.jpeg)

    ![](./media/image13.jpeg)

11. Add few more items to the list.

    ![](./media/image14.jpeg)

12. From the Visual Studio 2022, click on **Debug -\>** **Stop
    Debugging**.

    ![](./media/image15.jpeg)

### Task 2: Publish ASP.NET application to Azure

1.  In the **Solution Explorer**, right-click on
    your **DotNetAppSqlDb** project and select **Publish**.

    ![](./media/image16.jpeg)

    ![](./media/image17.jpeg)

2.  Select **Azure** and and click on **Next**.

    ![](./media/image18.jpeg)

3.  Select **Azure App Service(Windows)** in **Which Azure service would
    you like to use to host your application?** screen and click
    on **Next**.

    ![](./media/image19.jpeg)

4.  In the Publish dialog, click **Sign In** and Sign in to your Azure
    subscription, if not signed in already.

    **Note:** If you're already signed into a Microsoft account, make sure
that account holds your Azure subscription. If the signed-in Microsoft
account doesn't have your Azure subscription, click it to add the
correct account.

5.  Click on **Create new** to create a new App service.

    ![](./media/image20.jpeg)

6.  Enter the below details.

    |  **Property**  |  **Description**  |
    |:------|:-------|
    |  Name  | **!!TodoAppXXXX!!**  |
    | Resource group   |  Select the **assigned Resource group** |

    Click **New** on **Hosting Plan**.
    
    ![](./media/Picture13.png)

8.  Click **New** on **Hosting Plan** option and enter the below details
    and click **OK**.

    |  **Property**  |  **Description**  |
    |:------|:-------|
    |  Hosting Plan  | **!!myAppServicePlanXXXX!!**   |
    | Location   |  Select **West US**  |
    |  Size  |   **Free** |

    ![](./media/Picture14.png)

9.  Click **Create** on the App Service window and wait for Azure
    resources to get created.

    ![](./media/Picture15.png)

10. The **Publish** dialog shows the resources you have configured.
    Click **Finish**.

    ![](./media/Picture16.png)

11. Click on **Close**.

    ![](./media/image24.jpeg)

12. Scroll down to the Server Dependencies section and click on
    the **+** sign to add dependency.

    ![](./media/image25.jpeg)

13. Select **Azure SQL Database** in the **Add dependency** page and
    click on **Next**.

    ![](./media/image26.jpeg)

14. Click on **Create New** next to SQL databases, in the **Connect to
    Azure SQL Database** dialog box.

    ![](./media/image27.jpeg)

15. In the **Azure SQL Database Create new** dialog box, click
    on **New** next to the Database server.

    ![](./media/Picture17.png)

16. Fill in the below details and click on **OK**.

    | **Property**   |  **Description**  |
    |:-------|:--------|
    |  Database server name  | **dotnetappsqldbdbserverXXXX**   |
    |  Administrator username  |   !!sqladmin!! |
    |  Administrator password  |  !!PassWord98!!  |

    ![](./media/Picture18.png)

16. Click on **Create** in the Create new dialog.

    ![](./media/Picture19.png)

### Task 3: Configure database connection

1.  When the wizard finishes creating the database resources,
    click **Next**.

    ![](./media/Picture20.png)

2.  Fill in the below details in the **Connect to Azure SQL
    Database** dialog and click **Finish**.

    | **Property**   |  **Description**  |
    |:-------|:--------|
    |  Database connection string Name  | !!MyDbConnection!!  |
    |  Database connection user name |   !!Sqladmin!! |
    |  Database connection password |  !!PassWord98!!  |
    |  Azure App Settings  |  Selected  |

    ![](./media/image32.jpeg)

3.	Click on **Finish** after reviewing the **summary of changes**.

    ![](./media/image74.png)
  	
4.  Wait for configuration wizard to finish and click **Close**. The
    Azure SQL Db is now **connected** to your app.

    ![](./media/image33.jpeg)

5.  From the Publish page, click **Publish** on the top right corner.

    ![](./media/Picture21.png)

    **Note:** This will take around 5 minutes

6.  Once your ASP.NET app is deployed to Azure, your default browser is
    launched with the URL to the deployed app. **Add a few to-do items**.

    ![](./media/image35.jpeg)

### Task 4: Access the database locally

Visual Studio lets you explore and manage your new database in Azure
easily in the **SQL Server Object Explorer**. The new database already
opened its firewall to the App Service app that you created. But to
access it from your local computer (such as from Visual Studio), you
must open a firewall for your local machine\\s public IP address. If
your internet service provider changes your public IP address, you need
to reconfigure the firewall to access the Azure database again.

1.  From the Visual Studio 2022, **View** menu, select **SQL Server
    Object Explorer**.

    ![](./media/image36.jpeg)

2.  At the top of **SQL Server Object Explorer**, click the **Add SQL
    Server** button.

    ![](./media/image37.jpeg)

### Task 5: Configure the database connection

1.  In the **Connect** dialog, expand the **Azure** node. All your SQL
    Database instances in Azure are listed here.

2.  Select the database that you created
    earlier(**dotnetappsqldbdbserver98**). The connection you created
    earlier is automatically filled at the bottom.

3.  Type the database administrator **password** you created
    earlier(!!**PassWord98**!!) and click Connect.

    ![](./media/image38.jpeg)

### Task 6: Allow client connection from your computer

The Create a new firewall rule dialog is opened. By default, a server
only allows connections to its databases from Azure services, such as
your Azure app. To connect to your database from outside of Azure,
create a firewall rule at the server level. The firewall rule allows the
public IP address of your local computer.

The dialog is already filled with your computer's public IP address.

1.  Make sure that Add my client IP is selected and click OK.

    ![](./media/image39.jpeg)

2.  Once Visual Studio finishes creating the firewall setting for your
    SQL Database instance, your connection shows up in **SQL Server
    Object Explorer**.

3.  Expand your **connection \> Databases \> \< YOUR DATABASE \> \>
    Tables**.

    ![](./media/image40.jpeg)

4.  Right-click on the **Todoes** table and select **View Data**.

    ![](./media/image41.jpeg)

5.  View the contents of the table. The data added from the app UI should get listed here.

    ![](./media/image42.jpeg)

## Exercise 2: Update app with Code First Migrations

1.  From the **Solution Explorer**, open **Models\Todo.cs** in the code
    editor. Add the following property to the **ToDo** class as the last
    line (after the **public DateTime CreatedDate { get; set; }** line
    )and click on **Save**.

    !!**public bool Done { get; set; }**!!

    ![](./media/image43.jpeg)

### Task 1: Run Code First Migrations locally

Run a few commands to make updates to your local database.

1.  From the **Tools** menu, click **NuGet Package
    Manager** \> **Package Manager Console**.

    ![](./media/image44.jpeg)

2.  In the Package Manager Console window, enable Code First Migrations
    by executing this command.

    !!**Enable-Migrations**!!

    ![](./media/image45.jpeg)

3.  Add a migration by executing the below command.

    !!**Add-Migration AddProperty**!!

    ![](./media/image46.jpeg)

4.  Update the local database by executing the below command.

    !!**Update-Database**!!

    ![](./media/image47.jpeg)

5.  Type **Ctrl+F5** to run the app or click on **Debug -\> Start
    without Debugging**. Test the edit, details, and create links.

    ![](./media/image48.jpeg)

6.  The application page opens up and it still looks the same because
    your application logic is not using this new property yet.

    ![](./media/image49.jpeg)

### Task 2: Use the new property

Make some changes in your code to use the Done property.

1.  From the Visual Studio, open **Controllers\TodosController.cs**.
    Find the **Create()** method on line 52 and add !!**Done**!! to the list
    of properties in the Bind attribute. When you're done, your Create()
    method signature look like the following code:

    ![](./media/image50.jpeg)

2.  Open **Views\Todos\Create.cshtml**. Add the following code after the
    < div class=\"form-group\" > for **CreatedDate**.

    ![](./media/image51.jpeg)

    ```
    <div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>

    ```

3.  Open **Views\Todos\Index.cshtml**. Add the following code in the
    empty **th** element, after the **th** element for
    the **CreatedDate**.

    !!@Html.DisplayNameFor(model =\> model.Done)!!

    ![](./media/image52.jpeg)

4.  Add this code just above the html.ActionLink() helper methods.

    ```
    <td>
    @Html.DisplayFor(modelItem => item.Done)
</td>

    ```
    ![](./media/image53.jpeg)

5.  Type **Ctrl+F5** to run the app.

    ![](./media/image54.jpeg)

### Task 3: Enable Code First Migrations in Azure

1.  Right click on the project and select **Publish**.

    ![](./media/image55.jpeg)

2.  Click **More actions** \> **Edit** to open the publish settings.

    ![](./media/image56.jpeg)

3.  In the **MyDatabaseContext** dropdown, select the database
    connection for your Azure SQL Database.

4.  Select **Execute Code First Migrations** (runs on application
    start), then click **Save**.

    ![](./media/image57.jpeg)

5.  In the Publish page, click on **Publish**.

    ![](./media/image58.jpeg)

6.  The updated app is now available on Azure.

7.  Try adding to-do items again and select **Done**, and they should
    show up in your homepage as a completed item.

    ![](./media/image59.jpeg)
    
    ![](./media/image60.jpeg)

## Exercise 3: Stream application logs

1.  In the publish page, scroll down to the **Hosting** section. At the
    right-hand corner, click **...** \> **View Streaming Logs**.

    ![](./media/image61.jpeg)

2.  The logs are now streamed into the Output window.

    ![](./media/image62.jpeg)

3.  You don't see any of the trace messages yet because, when you first
    select View Streaming Logs, your Azure app sets the trace level to
    Error, which only logs error events.

    >[!Note] **Note:** Restart the logging stream from the Visual Studio if you do
not see them yet.

### Task 1: Change trace levels

1.  Go to the publish page. In the Hosting section, click **… \> Open in
    Azure portal**.

    ![](./media/image63.jpeg)

2.	In the Azure portal – app page, select **App Service Logs** from the left pane under the **Monitoring** section.

    ![](./media/image64.jpeg)

3.  Under **Application Logging** (File System), select **Verbose** in
    Level. Click **Save**.

    ![](./media/image65.jpeg)

4.  From your browser, access the web app on Azure and do some
    activities.

    ![](./media/image66.jpeg)

5.  The trace messages are now streamed to the Output window in Visual
    Studio.

    ![](./media/image67.jpeg)

6.  To stop the log-streaming service, click the **Stop
    monitoring** button in the Output window.

    ![](./media/image68.jpeg)

7.  Close the Visual Studio.

## Exercise 4: Clean up resources

1.	From the Azure portal, open your assigned Resourcegroup.

   ![](./media/Picture27.png) 

2.	Select all the resources and click on Delete.

   ![](./media/Picture28.png) 
   	
3.	Type !!delete!! in the text box and select Delete. Select Delete in the confirmation dialog box.
 
   ![](./media/Picture29.png) 

   ![](./media/Picture30.png) 

**Summary**

In this lab, you have learnt to deploy a data-driven ASP.NET app in App
Service and connect it to Azure SQL Database.

