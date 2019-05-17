# AzureDataFactory
This projects helps you to connect PostgreSQL to Azure Data Factory using ODBC method as an alternative



Steps  to connect to PostgreSQL database using Azure Data Factory as a Linked Service?
I was banging my head to fix this issue and had no proper documentation that could help me. It was throwing the same SSL error again and again when I used source as PostgreSQL option on Data factory. Below is the error for your reference.
>> ERROR [28000] [DataDirect][ODBC PostgreSQL Wire Protocol driver]Cannot load trust store
However, I found an alternative solution to connect to PostgreSQL using Azure Data factory as Linked service using ODBC method. This is for both Source and Sink. You will need couple of other applications apart from Data factory to perform this activity.

Pre-requisites:
1.	ODBC Drivers for PostgreSQL on your machine (Machine could be the VM or on-prem server which is up and running all the time)
2.	Self-Hosted Runtime integrator ( Download it from Microsoft website using this link https://www.microsoft.com/en-us/download/details.aspx?id=39717 )
3.	Azure Data Factory 
4.	Whitelist your IPs of your VM location on PostgreSQL server
Step 1:
Download and Install ODBC drivers to your machine 
https://www.postgresql.org/ftp/odbc/versions/msi/
Scroll down for the latest versions
 





Install drivers. It might ask for a restart to use the drivers.
 
Go to start menu and find ODBC drivers 
 
Click on Add button and new window will ask for create a data source. Select any PostgreSQL and click finish.
 
It opens a new window to create a driver setup for PostgreSQL. Select the appropriate SSL certificate mode.
 
Save  the Data source  name from above. You  will be using in the Final Step as a DSN.
 

Step 2:
Install self-hosted Integration run-time. Follow the instructions from Microsoft website.
https://www.microsoft.com/en-us/download/details.aspx?id=39717
Once you open it you will see the below window to configure Azure Data Factory with runtime integrator
 

Step 3: Get the Azure Authentication Key from Data Factory
Go to connections Tab in the bottom of Author page and click Create New connections in Integration Runtimes tab as shown below
 




Then,Select Perform data movement option
 

Next, Select Self-Hosted 
 

Now, Name it . Make sure you name it right because you cannot edit it later and it should be unique in each data factory
 

Copy any of these Keys 
 

Paste them in the Register window from step-2. You will see the successful connection window as below
 

You can gohead and test the connection using Diagnosis tab. Use the same details that you have used in step1 to create the ODBC drivers
 

Step 4:
Its time to create the new Linked service. Go to Azure Data Factory >> Author >> Connections >> Create New connection on Linked services tab as below
 
New side menu pops up to select the linked service. Search for ODBC. I know you want to search for PostgreSQL as I did but microsoft is some issue with it. If you have connected using postgresql then you are lucky. I was unable to do it even after 1000 trys.
 

 


 

 






Final Step:
For ODBC connectors JSON format syntax you can refer to this link
 https://docs.microsoft.com/en-us/azure/data-factory/connector-odbc
Now, Enter the credentials that you have used in step1 to create the ODBC drivers.
 




Click test connection, You are all set.  Go and create your pipelines now 😊

  

