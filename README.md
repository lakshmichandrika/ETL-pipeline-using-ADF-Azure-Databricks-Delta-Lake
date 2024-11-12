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


















































