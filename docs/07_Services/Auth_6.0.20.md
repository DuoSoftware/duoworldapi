Auth 6.0  is a secure token generator to access services provided by DuoWorld platform. This is a reset API and help developers to integrate and develop secure application and secure api with a federated security implementation.
[TOC]
## Login
**Method:** GET 

**Path:** "http://duoworld.com/auth/Login/{username:string}/{password:string}/{domain:string}

**output:**	
```json
	{
		UserID: "81be58d531e905b16aac87589984642a",
		Username: "lasitha.senanayake@gmail.com",
		Name: "Lasitha Senanayake",
		Email: "lasitha.senanayake@gmail.com",
		SecurityToken: "ecf8e3fce9133821b0c1e67e5b77ef31",
		Domain: "duoworld.duoweb.info",
		DataCaps: "#duoworld.duoweb.info#81be58d531e905b16aac87589984642a#1#2#4",
		ClientIP: "61.245.163.102:17179",
		Otherdata: {
		TenentsAccessible: "[{"TenantID":"dilshan.duoweb.info","Name":""},{"TenantID":"eranga.duoweb.info","Name":""},{"TenantID":"election.duoweb.info","Name":"Election"},{"TenantID":"srilankanvotes.com","Name":"Sri Lankan Election 2015"},{"TenantID":"admin.srilankanvotes.com","Name":"Sri Lankan Election Results"},{"TenantID":"duosoftware2.duoweb.info","Name":"ABC"}]"}
	}    
```
## Authorize
**Method:**GET 

**Path:**"http://duoworld.com/auth/Autherize/{SecurityToken:string}/{ApplicationID:string}"

**output:**	
```json
	{
		UserID: "81be58d531e905b16aac87589984642a",
		Username: "lasitha.senanayake@gmail.com",
		Name: "Lasitha Senanayake",
		Email: "lasitha.senanayake@gmail.com",
		SecurityToken: "ecf8e3fce9133821b0c1e67e5b77ef31",
		Domain: "duoworld.duoweb.info",
		DataCaps: "#duoworld.duoweb.info#81be58d531e905b16aac87589984642a#1#2#4",
		ClientIP: "61.245.163.102:17179",
		Otherdata: {
		TenentsAccessible: "[{"TenantID":"dilshan.duoweb.info","Name":""},{"TenantID":"eranga.duoweb.info","Name":""},{"TenantID":"election.duoweb.info","Name":"Election"},{"TenantID":"srilankanvotes.com","Name":"Sri Lankan Election 2015"},{"TenantID":"admin.srilankanvotes.com","Name":"Sri Lankan Election Results"},{"TenantID":"duosoftware2.duoweb.info","Name":"ABC"}]"}
	}    
```
## Get Session
**Method:**GET 

**Path:** "/GetSession/{SecurityToken:string}/{Domain:string}"

**output:**	
```json
	{
		UserID: "81be58d531e905b16aac87589984642a",
		Username: "lasitha.senanayake@gmail.com",
		Name: "Lasitha Senanayake",
		Email: "lasitha.senanayake@gmail.com",
		SecurityToken: "ecf8e3fce9133821b0c1e67e5b77ef31",
		Domain: "duoworld.duoweb.info",
		DataCaps: "#duoworld.duoweb.info#81be58d531e905b16aac87589984642a#1#2#4",
		ClientIP: "61.245.163.102:17179",
		Otherdata: {
		TenentsAccessible: "[{"TenantID":"dilshan.duoweb.info","Name":""},{"TenantID":"eranga.duoweb.info","Name":""},{"TenantID":"election.duoweb.info","Name":"Election"},{"TenantID":"srilankanvotes.com","Name":"Sri Lankan Election 2015"},{"TenantID":"admin.srilankanvotes.com","Name":"Sri Lankan Election Results"},{"TenantID":"duosoftware2.duoweb.info","Name":"ABC"}]"}
	}    
```
## Request App Authorizing code  
**Method:** GET

**Path:** "/GetAuthCode/{SecurityToken:string}/{ApplicationID:string}/{URI:string}"

**output:**	
```  
"string"
```
## Authorize Application 
**Method:** GET

**Path:**"/AutherizeApp/{SecurityToken:string}/{Code:string}/{ApplicationID:string}/{AppSecret:string}"

**output:**	
```  
"bool"
```
## Register User
**Method:** POST

**Post Data:**

```json
{
UserID: "",
EmailAddress: "lasitha.senanayake@gmail.com",
Name: "Lasitha Senanayake",
Password: "password",
ConfirmPassword: "password",
Active: false
}
```

**Path:**"/UserRegistation/"

**output:**	
```json  
{
UserID: "81be58d531e905b16aac87589984642a",
EmailAddress: "lasitha.senanayake@gmail.com",
Name: "Lasitha Senanayake",
Password: "password",
ConfirmPassword: "password",
Active: false
}
```
## Register Users by sign in users 
**Method:** POST

**Post Data:**
```json
{
UserID: "",
EmailAddress: "lasitha.senanayake@gmail.com",
Name: "Lasitha Senanayake",
Password: "password",
ConfirmPassword: "password",
Active: false
}
```

**http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string'      | 

**Path:** "/RegisterTenantUser/"

**output:**	
```json  
{
UserID: "81be58d531e905b16aac87589984642a",
EmailAddress: "lasitha.senanayake@gmail.com",
Name: "Lasitha Senanayake",
Password: "password",
ConfirmPassword: "password",
Active: false
}
```
## User Activation
**Method:** GET

**Path:** "/UserActivation/{token:string}"

**output:**	
```json  
"bool"
```
## Logout
**Method:** GET

**Path:** "/LogOut/{SecurityToken:string}"

**output:**	
```json  
"bool"
```
## Get User
**Method:** GET

**Path:** "/GetUser/{Email:string}"

**output:**	
```json  
{
UserID: "81be58d531e905b16aac87589984642a",
EmailAddress: "lasitha.senanayake@gmail.com",
Name: "Lasitha Senanayake",
Password: "password",
ConfirmPassword: "password",
Active: false
}
```
## Get GUID
**Method:** GET

**Path:**"/GetGUID/"

**output:**	
```json  
"string"
```
## Forgot Password
**Method:** GET

**Path:** "/ForgotPassword/{EmailAddress:string}/{RequestCode:string}"

**output:**	
```json  
"bool"
```
## Change Password
**Method:** GET

**Http Headers:**

| Name          | Value         | 
| ------------- |:-------------:| 
| Securitytoken | `string'      | 

**Path:**"/ChangePassword/{OldPassword:string}/{NewPassword:string}"

**output:**	
```json
"bool"
```
	
