The uiMicrokernal is an Angular library that enables developers to use DuoWorld specific features. After adding the uimicrokernel.js to the index.html inject the module 'uiMicrokernel' to your application. This library includes features to authenticate a session, perform CURD operations with the backend, call a smoothflow process, integrate with Cloud Event Bus (CEB - for chat applications, notifications, real-time messaging with WebRTC), and includes services to handle the execution of applications in the DuoWorld Shell.
[TOC]
### Authentication

To obtain user and tenant details in your angular application inject $auth in your controller which is derived from the uiMicrokernal.js

##### checkSession
Add this code snippet to see if the user is logged-in, if not he/she will be redirected  towards the login page.
```js
$auth.checkSession();
```

##### getSession
Returns the UserID, Username, Name, Email, SecurityToken, Domain, DataCaps, ClientIP and otherData of the logged-in user
```js
$auth.getUsername();
```

##### getUsername

Returns the username of the logged in user.
```js
$auth.getUsername();
```

### Object Store

The Object Store is middle layer between the application and the backend databases. This is the data persistence layer of DuoWorld and to access the objectstore methods the $objectstore service should be injected to the controller.

##### getClient
Before performing any operation a classname should be passed to the getClient() method. The classname is similar to a database table name.

```js
$objectstore.getClient(classname)
```

##### Insert / Update
To insert/update an object use insert() method, the parameters should contain the object which should be inserted (Eg: customer object) and the key-property of the object.
```js
var customer = {id:1, name: "Supun"};

$objectstore.getClient("customer").onComplete(function(data){ 
    alert ("Successfully Inserted!!!"); 
}).onError(function(error){ 
    alert ("Error inserting an object to objectstore"); 
}).insert(customer, {KeyProperty: "id"})
```

##### Delete
To delete an object use delete() method, the parameters should contain the object which should be deleted (Eg: customer object) and the key-property of the object.
```js
var customer = {id:1, name: "Supun"};

$objectstore.getClient("customer").onComplete(function(data){ 
    alert ("Successfully Deleted!!!"); 
}).onError(function(error){ 
    alert ("Error deleting an object from objectstore"); 
}).delete(customer, {KeyProperty: "id"})
```

##### Get All Objects (of a class)
To retrieve all objects of a class use getAll() method.
```js
$objectstore.getClient("customer").onGetMany(function(data){ 
    console.log(data); 
 }).onError(function(error){ 
    console.log ("Error retrieving object"); 
}).getAll("1")
 ```


##### Get Item by Key
To retrieve a single object by the key property use getByKey() method, the parameter should contain the keyProperty of the object.

```js
$objectstore.getClient("customer").onGetOne(function(data){ 
    console.log(data); 
}).onError(function(error){ 
    console.log ("Error retrieving object");
}).getByKey("1");
```

##### Get Filtered Results
To retrieve a filtered results set use the getByFiltering() method. SQL select commands can be written in here.
```js
$objectstore.getClient("customer").onGetMany(function(data){ 
    console.log(data); 
}).onError(function(error){ 
    console.log ("Error retrieving object"); 
}).getByFiltering("select * from customer where id='1'");
 ```
 
##### Get By Key Word
To retrieve any number of records which has the specified keyword use the get the getByKeyword() method.
```js
$objectstore.getClient("customer").onGetMany(function(data){ 
    console.log(data); 
}).onError(function(error){ 
    console.log ("Error retrieving object"); 
}).getByKeyword("colombo")
```
##### Skip and Take (For paging)
Applications with a large number of records will need to lazy load the data. This method allows the users to skip some records and retrieve a specified number of records.
```js
$objectstore.getClient("customer").onGetMany(function(data){ 
    console.log(data); 
}).onError(function(error){ 
    console.log ("Error retrieving object"); 
}).skip(100).take(10).getAll()
```
##### Order By Ascending
If the application requires to order the data in ascending order use the orderBy() method.
```js
$objectstore.getClient("customer").onGetMany(function(data){ 
    console.log(data); 
}).onError(function(error){ 
    console.log ("Error retrieving object"); 
}).orderBy("name").getAll();
```
##### Order By Descending
If the application requires to order the data in descending order use the orderByDesc() method.
```js
$objectstore.getClient("customer").onGetMany(function(data){ 
    console.log(data); 
}).onError(function(error){ 
    console.log ("Error retrieving object"); 
}).orderByDesc("name").getAll()
```



