# Shaping Up With AngularJS
[Source](https://www.codeschool.com/courses/shaping-up-with-angularjs)


## Modules
Where application components live

```javascript
(function(){
var app = angular.module('store',['comments-module']); //Strings in second argument are dependences 

app.controller('StoreController', function() { . . . });

app.directive('productGallery', function() { . . . });

})();
```

Modules should contain similar functionality. 

## Controllers
Controllers are where the app's behaviour is and is defined by functions and values

```javascript
var app = angular.module('store', []);

app.controller('StoreController', function() { //Controller name is capital case
    this.item = { name: "gem", price: 5};
});
```

Insert controller into html by using `ng-controller` directive like so:

```html
<div ng-controller="StoreController">
</div>
```

Values/Functions then can be used from within the html using: `{{ controller.stuff }}`

```html
<div ng-controller="StoreController">
    <h1> {{StoreController.item.name}} : ${{StoreController.item.price}} </h1>
</div>
```

## Directives
HTML Annotations that trigger javascript behaviours.

- **Element Directives**: Custom HTML tags that get expanded by angular. Used for UI widgets.
- **Attribute Directives**: Attached to an element on page. Used for mixin behaviours like tool-tips.

### Types
- **ng-app**       : Attach module to page
- **ng-controller**: Attach controller to page
- **ng-show**      : Only show attached element if the value of expression is true (or even null)
- **ng-hide**      : Literally the opposite of above
- **ng-repeat**    : Loops through a list of elements
- **ng-src**       : Needed to load an image from controller
- **ng-click**     : Allows expression to be evaluated when element is clicked
- **ng-init**      : Evaluate expression in current scope. If you have to use ng-init, probably best if it was moved into controller.
- **ng-class**     : Dynamically sets CSS classes on element.  e.g `<li ng-class="{{ active: tab === 1 }}">` active will be attached to li element if tab is 1.
- **ng-model**     : Binds the form element value to the property
- **ng-options**   : Dynamically generates a list of `<option>` elements for attached `<select>` element.
- **ng-submit**    : Allows a function to be called when form is submitted
- **ng-include**   : Includes a template to insert into the html page. e.g `<h3 ng-include="'product-title'"></h3>`. Generally better using a custom directive than this.


### Custom Element Directives
Allows the creation of custom HTML tags e.g. `<product-title></product-title>` that get expanded out by angular.

```javascript
app.directive('productTitle', function() { //dash in HTML translate to camelCase in javascript
    return {
        restrict: 'E', //type of directive (E for element, A for attribute
        templateUrl: 'product-title.html' //URL of a template
        controller: function() { //can embed controller in directive
            
        },
        controllerAs: 'tab' //alias for controller
        
    };

});
```




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

### Forms
AngularJS has inbuilt functionality for form validation. Setting type to input elements to things like `email` and `number` will automatically make Angularjs run validaiton on them.

#### CSS Classes
- ng-valid set if form is valid
- ng-invalid set if form is invalid
- ng-pending set if form is pending
- ng-pristene set if form hasn't been touched by user
- ng-dirty set if form has been touched by user
- ng-submitted set if form is submitted

## Services
Services give Controller extra functionality. All service begin with a `$`.

```javascript
app.controller('SomeController', [ '$http', '$log', function($http, $log) {
    var thisController = this;
    thisController.data = [];

    $http.get('/data.json').success(function(data) {
        thisController = data;     
    });

}]);

```

- $http  : Fetch/Push JSON to web services. e.g `$http.get('/products.json', { apiKey: 'myApiKey' })` returns a Promise object with `.success()` and `.error()`
- $log   : Logger
- $filter: Filter an array.

## Additonal Resources
[Course Source Code](https://github.com/codeschool/ShapingUpWithAngular.js)

[AngularJS docs](https://docs.angularjs.org/api)

[ng-newsletter](http://www.ng-newsletter.com/)

## Examples

### Shop

#### js
```javascript
(function() {
  var app = angular.module('gemStore', []);

  app.controller('StoreController', function(){
    this.products = gems;
  });

  app.controller('TabController', function(){
    this.tab = 1;

    this.setTab = function(tab){
      this.tab = tab;
    };

    this.isSet = function(tab){
      return (this.tab === tab);
    };
  });

  app.controller('GalleryController', function(){
    this.current = 0;

    this.setCurrent = function(index){
      this.current = index;
    };
  });

  app.controller('ReviewController', function() {
    this.review = {};

    this.addReview = function(product) {
      product.reviews.push(this.review);

      this.review = {};
    };
  });

  var gems = [{
      name: 'Azurite',
      description: "Some gems have hidden qualities beyond their luster, beyond their shine... Azurite is one of those gems.",
      shine: 8,
      price: 110.50,
      rarity: 7,
      color: '#CCC',
      faces: 14,
      images: [
        "images/gem-02.gif",
        "images/gem-05.gif",
        "images/gem-09.gif"
      ],
      reviews: [{
        stars: 5,
        body: "I love this gem!",
        author: "joe@example.org",
        createdOn: 1397490980837
      }, {
        stars: 1,
        body: "This gem sucks.",
        author: "tim@example.org",
        createdOn: 1397490980837
      }]
    }, {
      name: 'Bloodstone',
      description: "Origin of the Bloodstone is unknown, hence its low value. It has a very high shine and 12 sides, however.",
      shine: 9,
      price: 22.90,
      rarity: 6,
      color: '#EEE',
      faces: 12,
      images: [
        "images/gem-01.gif",
        "images/gem-03.gif",
        "images/gem-04.gif",
      ],
      reviews: [{
        stars: 3,
        body: "I think this gem was just OK, could honestly use more shine, IMO.",
        author: "JimmyDean@example.org",
        createdOn: 1397490980837
      }, {
        stars: 4,
        body: "Any gem with 12 faces is for me!",
        author: "gemsRock@example.org",
        createdOn: 1397490980837
      }]
    }, {
      name: 'Zircon',
      description: "Zircon is our most coveted and sought after gem. You will pay much to be the proud owner of this gorgeous and high shine gem.",
      shine: 70,
      price: 1100,
      rarity: 2,
      color: '#000',
      faces: 6,
      images: [
        "images/gem-06.gif",
        "images/gem-07.gif",
        "images/gem-08.gif"
      ],
      reviews: [{
        stars: 1,
        body: "This gem is WAY too expensive for its rarity value.",
        author: "turtleguyy@example.org",
        createdOn: 1397490980837
      }, {
        stars: 1,
        body: "BBW: High Shine != High Quality.",
        author: "LouisW407@example.org",
        createdOn: 1397490980837
      }, {
        stars: 1,
        body: "Don't waste your rubles!",
        author: "nat@example.org",
        createdOn: 1397490980837
      }]
    }];
})();

```

#### html
```html
<DOCTYPE html>
<html ng-app="gemStore">
  <head>
    <link rel="stylesheet" type="text/css" href="bootstrap.min.css" />
    <script type="text/javascript" src="angular.min.js"></script>
    <script type="text/javascript" src="app.js"></script>
  </head>
  <body ng-controller="StoreController as store">
    <header>
      <h1 class="text-center">Flatlander Crafted Gems</h1>
      <h2 class="text-center">– an Angular store –</h2>
    </header>
    <div class="list-group">
      <div class="list-group-item" ng-repeat="product in store.products">
        <h3>{{product.name}} <em class="pull-right">{{product.price | currency}}</em></h3>
        <div ng-controller="GalleryController as gallery"  ng-show="product.images.length">
          <div class="img-wrap">
            <img ng-src="{{product.images[gallery.current]}}" />
          </div>
          <ul class="img-thumbnails clearfix">
            <li class="small-image pull-left thumbnail" ng-repeat="image in product.images">
              <img ng-src="{{image}}" />
            </li>
          </ul>
        </div>
        <section ng-controller="TabController as tab">
          <ul class="nav nav-pills">
            <li ng-class="{ active:tab.isSet(1) }">
              <a href="" ng-click="tab.setTab(1)">Description</a>
            </li>
            <li ng-class="{ active:tab.isSet(2) }">
              <a href="" ng-click="tab.setTab(2)">Specs</a>
            </li>
            <li ng-class="{ active:tab.isSet(3) }">
              <a href="" ng-click="tab.setTab(3)">Reviews</a>
            </li>
          </ul>
          <div ng-show="tab.isSet(1)">
            <h4>Description</h4>
            <blockquote>{{product.description}}</blockquote>
          </div>
          <div ng-show="tab.isSet(2)">
            <h4>Specs</h4>
            <blockquote>Shine: {{product.shine}}</blockquote>
          </div>
          <div ng-show="tab.isSet(3)">
            <!--  Product Reviews List -->
            <ul>
              <h4>Reviews</h4>
              <li ng-repeat="review in product.reviews">
                <blockquote>
                  <strong>{{review.stars}} Stars</strong>
                  {{review.body}}
                  <cite class="clearfix">—{{review.author}}</cite>
                </blockquote>
              </li>
            </ul>

            <!--  Review Form -->
            <form name="reviewForm" ng-controller="ReviewController as reviewCtrl" ng-submit="reviewCtrl.addReview(product)">

              <!--  Live Preview -->
              <blockquote>
                <strong>{{reviewCtrl.review.stars}} Stars</strong>
                {{reviewCtrl.review.body}}
                <cite class="clearfix">—{{reviewCtrl.review.author}}</cite>
              </blockquote>

              <!--  Review Form -->
              <h4>Submit a Review</h4>
              <fieldset class="form-group">
                <select ng-model="reviewCtrl.review.stars" class="form-control" ng-options="stars for stars in [5,4,3,2,1]" title="Stars">
                  <option value="">Rate the Product</option>
                </select>
              </fieldset>
              <fieldset class="form-group">
                <textarea ng-model="reviewCtrl.review.body" class="form-control" placeholder="Write a short review of the product..." title="Review"></textarea>
              </fieldset>
              <fieldset class="form-group">
                <input ng-model="reviewCtrl.review.author" type="email" class="form-control" placeholder="jimmyDean@example.org" title="Email" />
              </fieldset>
              <fieldset class="form-group">
                <input type="submit" class="btn btn-primary pull-right" value="Submit Review" />
              </fieldset>
            </form>
          </div>
        </section>
      </div>
    </div>
  </body>
</html>


```


