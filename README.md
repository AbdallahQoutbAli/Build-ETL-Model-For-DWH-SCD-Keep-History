# SSIS BUILD ETL MODEL TO KEY Histroy
This Project Will help you to build a ETL Model for Your Company Using SSIS 

1- I Create DATALAKE & DWH Database <br />  
Note : DATALAKE maybe (SQL SERVER,CRM,ORACLE,MYSQL.....) (Scripted Attached) <br />
 
 
2- Load Data From DATALAKE <br />
3- Inside The Lookup I made Query To Get The Last inserted Recored By using Ranking Funcation and Partion by Table Key  <br />
Ex :

``` sql

SELECT  
[CITY_KEY]
        from (
	  select * ,ROW_NUMBER() OVER (PARTITION BY [CITY_KEY] ORDER BY [END_DATE] DESC ) AS RN
	  from  [dbo].[CITY]
 ) as T 

	  WHERE T.RN =1
```

![alt text](https://github.com/abdallahkotb5566/Build-ETL-Model-For-DWH-SCD-/blob/main/ETL%20Model%20Iniatil%20Load%20and%20increm..PNG)

4- After Get Data We Have 2 Road First Insert New Recordes in DWH OR Compere the old Recoreds Inside Secound Lookup <br />
5- If Data Changed I Will Insert It in DWH by change The Status 'U' (Upated) and Close END_DATE  <br />
As Show Below The Cityname Changed So I Keep History


![alt text](https://github.com/abdallahkotb5566/Build-ETL-Model-For-DWH-SCD-/blob/main/UpdatedCase.PNG)

Query To Close DATE In OLE DB Command
``` sql
UPDATE [CITY]
SET END_DATE=?
Where CITY_KEY = ? 
and END_DATE='2999-12-31 12:00:00.000'
``` 



