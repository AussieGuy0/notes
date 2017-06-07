# Shaping Up With AngularJS
**Type**: Course
[Source](https://www.codeschool.com/courses/shaping-up-with-angularjs)


## Modules
Where application components live

## Controllers
Controllers are where the app's behaviour is by defining functions and values

```javascript
var app = angular.modle('store', []);

app.controller('StoreController', function() { //Controller name is capital case
    this.item = { name: "gem", price: 5};
});
```

- Insert controller into html by using `ng-controller` directive like so:

```html
<div ng-controller="StoreController">
</div>
```

- Values/Functions then can be used from within the html using: `{{ controller-stuff }}`

```html
<div ng-controller="StoreController">
    <h1> {{StoreController.item.name}} : ${{StoreController.item.price}} </h1>
</div>
```

## Directives
HTML Annotations that trigger javascript behaviours

### Types
- ng-app       : Attach modue to page
- ng-controller: Attach controller to page
- ng-show      : Only show attached element if the value of expression is true (or even null)
- ng-hide      : Literally the opposite of above
- ng-repeat    : Loops through a list of elements
- ng-src       : Needed to load an image from controller
- ng-click     : Allows expression to be evaluated when element is clicked
- ng-init      : Evaluate expression in current scope. If you have to use ng-init, probably best if it was moved into controller.
- ng-class     : Dynamically sets CSS classes on element.  e.g `<li ng-class="{{ active: tab === 1 }}">` active will be attached to li element if tab is 1.
- ng-model     : Binds the form element value to the property

### Expressions
Expressions define a 2-way data binding. Expressions are re-evaluated when a property changes.

## Filters

'|' in expressions can be used to pipe input into filters.

Syntax of filters: `{{ data | filter:options}}`
e.g: `{{'1388123412323' | date:'MM/dd/yy @ h:mma}}` results in `12/27/2013 @ 12:50AM`

### Types

- date: Change timestamp to human readable date
- lowercase/uppercase: as title says
- limitTo: Limits the number of elements shown by the given amount
- orderBy: Sorts elements by an attribute
