Tenant 6.0 is a REST api to create tenants for the cloud platform its been used for. 
[TOC]

## Create Tenant 
**Method:** POST

**Post Data:**
```
{
"TenantID":"lasitha.ssosgrid.com",
"Name":"","Shell":"12thDoorShell/index.html#/duoworld-framework/dock",
"Statistic":{"DataDown":"10GB","DataUp":"10GB","NumberOfUsers":"20","name":"Silver","price":"$10"},
"Private":true,
"OtherData":{"CompanyName":"dilshan Pvt.Ltd","SampleAttributs":"Values","catagory":"communication"}
}
```

**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string`      | 

**Path:**"/tenant/CreateTenant/"

**output:**	
```  
{
"TenantID":"lasitha.ssosgrid.com",
"Name":"","Shell":"12thDoorShell/index.html#/duoworld-framework/dock",
"Statistic":{"DataDown":"10GB","DataUp":"10GB","NumberOfUsers":"20","name":"Silver","price":"$10"},
"Private":true,
"OtherData":{"CompanyName":"dilshan Pvt.Ltd","SampleAttributs":"Values","catagory":"communication"}
}
```

## Check whether tenant is authorized
**Method:** GET

**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string`      | 

**Path:**"/tenant/Autherized/{TenantID:string}"

**output:**	
```  
{
"ID":"382eabadc85ca09875b3cab534be348b",
"UserID":"81be58d531e905b16aac87589984642a",
"TenantID":"dilshan.duoweb.info",
"SecurityLevel":"admin",
"Autherized":true
}
```

## GET Tenant
**Method:** GET 


**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string`      | 

**Path:**"/tenant/GetTenant/{TenantID:string}"

**output:**	
```  
{
"TenantID":"lasitha.ssosgrid.com",
"Name":"","Shell":"12thDoorShell/index.html#/duoworld-framework/dock",
"Statistic":{"DataDown":"10GB","DataUp":"10GB","NumberOfUsers":"20","name":"Silver","price":"$10"},
"Private":true,
"OtherData":{"CompanyName":"dilshan Pvt.Ltd","SampleAttributs":"Values","catagory":"communication"}
}
```

## Invite User to Tenant / Request t join Tenant
**Method:** POST

**Post Data:**
```
{
	"Email":"lasitha.senanayake@gmail.com"
	"Name":"Lasitha Senanayake"
	"UserID":"23213332223"
	"SecurityLevel":"admin"
}
```

**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string`      | 

**Path:**"/tenant/InviteUser/"

**output:**	
```  

```

## Accept Request
**Method:** GET


**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string`      | 

**Path:**"/tenant/AcceptRequest/{securityLevel:string}/{RequestToken:string}/{accept:bool}"

**output:**	
```  
"bool"
```

## Search Tenants
**Method:** GET 

**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string`      | 

**Path:**"/tenant/SearchTenants/{SearchString:string}/{pagesize:int}/{startPoint:int}"

**output:**	
```  
[
{"TenantID":"dilshan.duoweb.info",
"Name":"","Shell":"12thDoorShell/index.html#/duoworld-framework/dock",
"Statistic":{"DataDown":"10GB","DataUp":"10GB","NumberOfUsers":"20","name":"Silver","price":"$10"},
"Private":true,
"OtherData":{"CompanyName":"dilshan Pvt.Ltd",
"SampleAttributs":"Values",
"catagory":"communication"}}
]
```

## Subscribe to tenant 
**Method:** GET

**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string`      | 

**Path:**"/tenant/Subciribe/{TenantID:string}"

**output:**	
``` 
"bool" 
```

## Get Users
**Method:** GET

**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string`      | 

**Path:**"/tenant/GetUsers/{TenantID:string}"

**output:**	
``` 
"[]string" 
```
## Add Users
**Method:** GET

**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string`      | 

**Path:**"/tenant/AddUser/{email:string}/{level:string}"

**output:**	
``` 
"bool" 
```
