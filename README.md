# Building-an-end-to-end-data-pipeline-using-Azure-Databricks-Delta-Lake
how to develop an end-to-end data pipeline using Delta Lake which is an open-source storage layer that provides ACID transactions and metadata handling. Also you will learn how data moves from bronze to gold container, how to make an incremental load, create external tables for data analysis and orchestrate your pipeline. 

Technologies used: PySpark, ADSLS, Azure Databricks, Azure Data Factory and Power BI,App registrations,Key vault


Requirements:

1.Azure Account (Free Trial Subscription)

2.Basic knowledge of Azure

3.Basic knowledge of Databricks

4.Basic knowledge of Python and PySpark

![image](https://github.com/user-attachments/assets/5c838af6-fa44-4e77-9843-759bf513252e)


Process:

1.Create Resource Group

2.create a databricks workspace,and set up cluster.

3.create a storage account and then the layers we are going to need for our pipeline (bronze, silver, gold) according to Delta Lake Architecture.

4.make sure to check the hierarchial namespace whether ticked or not.

5.open Azure Active Directory, click on App registrations on the left panel and then on New Registration.

6.once created, save the application Id, object Id and Directory Id on a notepad, we will need them, later

7.It’s very important to copy the secret value and keep it in a notepad, because once you come out of the screen, you won’t be able to get it again.

![image](https://github.com/user-attachments/assets/076afdf5-b748-4fb1-8e9e-0768addb2c7d)

![image](https://github.com/user-attachments/assets/0fc51117-8641-441e-b60f-7ffc551efaec)

8.Go to your storage account, on the left panel click on Access Control (IAM) and then on Add Role Assignment.
Select the “Storage Blob Data Contributor” role, then click on next or go to Members tab

![image](https://github.com/user-attachments/assets/771f5603-e541-413e-b427-121fb359c036)

9.On Members Tab, click on “+ Select members” and find your databricks-service-app and select it. Finally click on Review + assign

![image](https://github.com/user-attachments/assets/6fd6f8ae-c08b-4a01-bba6-b79ef892938c)

![image](https://github.com/user-attachments/assets/41d616c9-95b5-4fd4-9fd5-59597fa97fa2)

10.After your Key-Vault has been created, go to Secrets inside Objects section and click on Generate/Import

11.create 3 secreats wich we have saved earlier

![image](https://github.com/user-attachments/assets/b78b3d7b-1fe8-4104-a7bd-ccd0959346d2)

12.Go to the properties of your Key-vault and copy the Vault URI and Resource ID values in a notepad

![image](https://github.com/user-attachments/assets/99177556-ffec-4858-b07f-713df1947526)

13.Link Databricks Secret Scopes with Azure Key-vault,Launch your Databricks Workspace, and go to your portal page. Once you are there you need to add “secrets/createScope” after the “#” symbol in the URL and click enter.

![image](https://github.com/user-attachments/assets/4016624a-8e1b-44b6-a8f8-6b4ae31e28d9)

14.On the new screen displayed, set an scope-name, set manage principal to All Users and also fill the DNS Name (Vault URI) and Resource Id with the corresponding values from your Azure Key-Vault (Step 3) and click on Create.

![image](https://github.com/user-attachments/assets/2381c12b-30cf-4c4b-9084-fda2cc1adffb)

15.Mount azure containers into databricks,Create a workspace with the name “moun-adls-storage”  and inside it a folder called set-up

![image](https://github.com/user-attachments/assets/49e3d286-7072-4bd1-92f3-42d63d626be8)

16.Open your notebook and start your cluster.(check with databricks_notebook file)

![image](https://github.com/user-attachments/assets/a8323417-ec3f-4b33-aa0e-6c9bc7726a6d)

![image](https://github.com/user-attachments/assets/e87df906-463b-404d-b76c-e55609830b1b)


Use Case Explanation
We will be working with transactional data referred to loan transactions and customers from GeekBankPE (a famous bank around the world).

You have two requirements from different areas of the bank.

1.The Marketing area needs to have updated customer data to be able to contact them and make offers.

2.The Finance area requires to have daily loan transactions complemented with customer drivers to be able to analyze them and improve the revenue.

To comply with the request, we are going to perform incremental loads and also using techniques like upsert.

![image](https://github.com/user-attachments/assets/93516ada-1655-49fd-8111-938a7ed58f29)


Data Ingestion and Transformation:

About dataset:

1.Customer: This data needs to be treated with an UPSERT technique because it only send new and modified records daily.
- customerId: unique identifier
- firstName: name
- lastName: last name
- phone: home phone number
- email: email
- gender: Male or Female
- address: place where the customer lives
- is_active: flag that indicates if the client is with us

2.Customer Drivers: This data is generated daily from the RiskModeling area. The data that is sent is an snapshot of the day. This data will be loaded incrementally.
- date: date that the data was generated by RiskModeling area
- customerId: unique identifier of the customer
- monthly_salary: monthly salary in USD
- health_score: score - how important is the customer for the bank
- current_debt: current debt that the customer has with our bank
- category: segment of the customer

3.Loan Transactions: Data correspond to the transactions performed in a specific date. This data will be loaded incrementally.
- date: date of the transaction
- customerId: unique identifier of the customer
- paymentPeriod: term of the loan
- loanAmount: amount requested by the customer
- currencyType: currency of the loan (USD, EUR)
- evaluationChannel: channel by which the loan was sold
- interest_rate: rate of the loan

1.Upload data to bronze layer either using adf pipeline or using Azure Storage Explorer

2.download : https://azure.microsoft.com/en-us/products/storage/storage-explorer/#overview

3.Once you have set up your Storage Explorer, you just need to drag and drop the folders in it

![image](https://github.com/user-attachments/assets/248d7c45-bdfd-405c-8180-37e063d80df7)

4.The execution order of our files is the following:

![image](https://github.com/user-attachments/assets/bc5045d2-57c7-45bb-ab3a-f9f4dcba231f)

5.On your databricks workspace create a folder called "ingestion" and inside it the following notebooks:
- customer.py
- customerDriver.py
- loanTransaction.py
  
Also in your databricks workspace create a folder called "includes" and inside it the following notebooks:
- common_functions.py
- configurations.py

![image](https://github.com/user-attachments/assets/386b2f39-6c8e-453c-9ee4-88a824c0fff5)

![image](https://github.com/user-attachments/assets/7955384f-b719-40f6-917c-941a036ca7f7)










































