# Realtime Data-entry

This is a sample angular application made to show the power and simplicity of DuoWorld. It demonstrates how to do basic CURD operations like inserting to objectstore and update the UI in real-time if the data is changed by another user. For real-time operations the Cloud Event Bus (CEB) of the DuoWorld platform is used.



### Let's get started

* The Angular Material libaray should be added to the index.html file. This includes 
```html
<!--CSS Libraries-->
<link rel="stylesheet" type="text/css" href="/bower_components/angular-material/angular-material.min.css">
<link rel="stylesheet" type="text/css" href="/css/child_app_styles.min.css">
<link rel="stylesheet" type="text/css" href="/css/directive_library.css">
```

```html
<!--Angular Material Library-->
<script src="/bower_components/angular/angular.min.js"></script>
<script src="/bower_components/angular-animate/angular-animate.min.js"></script>
<script src="/bower_components/angular-aria/angular-aria.min.js"></script>
<script src="/bower_components/angular-material/angular-material.min.js"></script>
<script src="/bower_components/angular-messages/angular-messages.min.js"></script>

<!--Angular ui-router for managing states/views-->
<script src="/bower_components/angular-ui-router/release/angular-ui-router.min.js"></script>

<!--socket.io for real-time communication-->
<script src="/uimicrokernel/socket.io-1.2.0.js"></script>
<!--uiMicrokernel for DuoWorld Operations-->
<script src="/uimicrokernel/uimicrokernel.js"></script>
<!--Directive Library additional UI components-->	
<script src="/js/directivelibrary.js"></script>
```

and finally add your controllers
```html
<script src="js/controllers/main.js"></script>
```

* Writing the application logic in the main.js

Add the modules(libraries) into your angular application.
```js
var app = angular.module('mainApp', ['ngMaterial', 'ngAnimate', 'ngMessages', 'ui.router', 'directivelibrary' ,'uiMicrokernel'])
```

When the ui-view directive is detected by the browser it will check for the configuration of the ui-router. The config for this app is -
```js
app.config(function($stateProvider, $urlRouterProvider) {
	$urlRouterProvider.otherwise('/view');
	$stateProvider
	// HOME STATES AND NESTED VIEWS ========================================
	.state('view', {
		url: '/view',
		templateUrl: 'partials/view.html',
		controller: 'viewCtrl'
	})
})
```
This means it will go and fetch the view.html file and assign it with the controller with the name of 'viewCtrl'. The viewCtrl will contain the logic of the entire application in this example.

### Objectstore
##### Insert
The function below is a save function which will store a customer object with the key property as 'email' on the 'customer' class in the objectstore.
```js
//UI logic
function saveCustomer(answer){
    $scope.currentCustomer = answer; // Object to be saved
    $objectstore.getClient("customer").onComplete(function(){
        sendNotification();
        notifications.toast("Customer Added", "success");
    }).onError(function(err){
        notifications.alertDialog("Error Inserting", "The customer was not added to the database, Try again!");
    }).insert([$scope.currentCustomer], {KeyProperty:"email"});
}
```
Example of an object which should be passed to the above method.
```js
saveCustomer({email:"dilshan@duosoftware.com",name:"Dilshan Liyanage", Address: "403 1/1, Galle Rd, Colombo"});
```

##### Retrieve
To all the data in the class 'customer' use this method. 
* note - uiInitilize is a service which is injected to the controller to do some operations relating to the collapse cards view of the DuoWorld platform. the insertIndex function gives each record an index starting from zero. This is used to reference the array elements since the directive md-virtual-repeat does not have $index by default.
```js
$scope.allCustomers = []; // Initialize an allCustomers array
function getAllCustomers(){
    $objectstore.getClient("customer").onGetMany(function(data){
        console.log(data); //log the data for reference
        $scope.allCustomers = uiInitilize.insertIndex(data);
    }).onError(function(err){
        alert ("Error loading all customers");
    }).getAll();
}
```
* Additional - This holds the UI logic for the collapse cards clicks so that if one is open the others will automatically close.
```js
 $scope.toggles = {}; 
 $scope.toggleOne = function($index)
 {	
	$scope.toggles = uiInitilize.openOne($scope.allCustomers, $index);
 }
```
### Cloud Event Bus (CEB)
To integrate the real-time data feature of this application the CEB should be integrated.
First $auth, $ceb and $presence are injected to the controller which is derived from the uiMirockernel. Then a event name is registered in the CEB called 'DemoAppUpdated' which will start listening to events if $presence.setOnline() is called. Whenever an event is triggered it will have a callback function called 'recieveNotification' which will add the newly added record into the UI. If a record is added from the client then he/she will have to call the sendNotification() function so that it will trigger an event so that other users who have registered to the CEB event ('DemoAppUpdated') will also get the update.

```js
// Check if user is logged in, if not redirect back-into login
$auth.checkSession();
//Set to online
$presence.setOnline();

$presence.onOnline(function(){
    $ceb.subscribeEvent("DemoAppUpdated");
    $ceb.onRecieveEvent("DemoAppUpdated",recieveNotification);        
});
function recieveNotification(e,data){
    console.log(data);
    if (!$scope.allCustomers) $scope.allCustomers = [];
    $scope.allCustomers.push(data);
}
function sendNotification(){
    $ceb.triggerevent("DemoAppUpdated", $scope.currentCustomer);
}
```

Congratulations if you made it this far, You can checkout the full source code from 
[Github.](https://github.com/DuoSoftware/DW-Common-UI-Seed-Projets/tree/master/Realtime%20Data-entry)
