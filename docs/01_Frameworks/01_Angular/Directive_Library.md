# Directive Library Guide

Angular Material still lacks some UI components. This project aims to bring those missing components. The directive library is a JavaScript file which contains custom directives that can be used easily by any developer using the DuoWorld Developer Portal. 

Note - The Dependancies for this library include the uimicrokernel.js (form the duoworld.com developer platform) which is used in the File-uploader directive and also angularMoment which is already included in the directivelibrary in itself.
 
(last build: 24-06-2016)


How to use this library in your application.

* Locate this script in your HTML document.
```html
<script src="/js/directivelibrary.js"></script>
```
* Some components require custom CSS so import the directive_library.css
```html 
<link rel="stylesheet" href="/css/directive_library.css">
```
* Add the 'directivelibrary' module to your application.

### Background banner
 This is a simple directive where the background banner can be used with a custom color and given a height. This is purely for aesthetics and conforms with the material design guidelines. 
```html
<md-background-banner color="#004682" height="300px"> </md-background-banner>
```
### Section Title
  
Give a section title for a row
  
```html
<section-title title="Account Details"></section-title>
```
To leave an empty space in a row use
```html
<section-title hide-sm hide-xs></section-title>
```

### Date Picker
  
This is an additional date-picker a developer may use if they are not satisfied with the  date-picker directive offered by angular material. After a user picks a date the value will be contained in the model attribute.

```html
<md-date-picker model="content.date" label="Pick a date"/>
```

### File uploader

The file uploader helps users to upload pictures or documents to use in the applications. 
* An os-class name should be specified, this is the name of the folder which the file/s will get saved. After a user add the file/s to the file uploader and clicks upload an array of urls will be returned to the application which will be contained in the model. This array contains direct links to the uploaded pictures or documents which were uploaded.

* Change the label to suit the user interface.


```html
<file-up-loader os-class="testupload" label="Add here" model="content.documents" class="md-block" flex-gt-sm>
</file-up-loader>
```
  
Don't forget to initialize and array before using this directive.
```js
$scope.content = {};
$scope.content.documents = []
```
  
### Rating Stars
  
A developer can use this directive to get user reviews.
  
* The ng-model equivalent of this directive is called ‘rating’ and the initial rating can be changed with the scope in the respective script file. 
* The read-only values can be set to true or false. 
* The max-rating can be changed to a higher number if necessary. 
* The ng-click equivalent is called click in this particular example. In the example it is passing the user’s rating.
* Mouse-hover events can also be written if necessary.


```html
<div star-rating rating="starRating1" read-only="false" max-rating="5" click="click1(param)" mouse-hover="mouseHover1(param)" mouse-leave="mouseLeave1(param)">
</div>
```
  
  
### Image Not Found

This directive is useful when there is already an image url however this image does not exist in the server. simply add the err-src attribute and give an url of a  default picture.

```html
<img ng-src="{{product.displayPicture}}" err-src="img/not_found.png"  alt=""/>
```
 
### Single Click
 
This directive fires an event similar to an ng-click however it has a delay of 300 milliseconds. This is ideal to use when there is a ng-double click (ng-dblclick) event so that both methods will not be fired rather than using an ng-click.
 
```html
<div sglclick="delayedAction()">
</div>
```
 
### Right-click
 
Simply write a event which will be fired if the user presses right-click.
```html
<div ng-right-click="openButtonProperties()">
</div>
```

### Notifications
The directivelibrary also contains services to improve the UI features.
##### Toast
By default the notifications service toast will be on the bottom right.

* Before using this service don't forget to inject the 'notifications' service to your controller.
* The first parameter contains the message.
* The second is if it is a success or error. This will change the color of the toast accordingly. 
* The third parameter is an optional one to contain the duration of the toast. The default time period is 2000 milliseconds.

```js
notifications.toast("This is a success toast", "success", 3000);
```
##### Alert Dialog
 
This is a Material Design alert.
```js
notifications.alertDialog("Alert Title", "Alert Message");
```
 
##### Content Loader
  
This is useful to notify the user when the content is being loaded to the UI.
```js
// Start loader
notifications.startLoading("Loading content, Please wait...");
// End loader
notifications.finishLoading();
 ```
 
### UI Initilize
The directivelibrary also contains services to improve the UI features. The 'uiInitilize' service can be injected to the controller in a specific instance if the developer wants to make a material design list-view which has md-virtual-repeat. Please note that this might not make sense if you don't have the collapse cards list view html.

```js
$scope.array  = uiInitilize.insertIndex($scope.array);

//This holds the UI logic for the collapse cards
$scope.toggles = {};
$scope.toggleOne = function($index)
{	
	$scope.toggles = uiInitilize.openOne($scope.array, $index);
}
```
