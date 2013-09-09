# Backbone.Obscura

Backbone.Obscura is a read-only proxy of a Backbone.Collection that can easily be 
filtered, sorted, and paginated. As the underlying collection is changed the proxy 
is efficiently kept in sync, taking into account all of the transformations. All
transformations can be modified at any time. The proxy implements all of the read-only
Backbone.Collection methods.

This means you can pass the proxy into a Backbone.View and let Backbone.Obscura take
care of the filtering or paginating logic, leaving your view to only re-render itself
as the collection changes. This keeps your views simple and [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself).
This works particularly well with [Marionette's](https://github.com/marionettejs/backbone.marionette)
[CollectionView](https://github.com/marionettejs/backbone.marionette/blob/master/docs/marionette.collectionview.md).

This library is effectively a convenience wrapper around [backbone-filtered-collection](https://github.com/jmorrell/backbone-filtered-collection),
[backbone-sorted-collection](https://github.com/jmorrell/backbone-sorted-collection), 
and [backbone-paginated-collection](https://github.com/jmorrell/backbone-paginated-collection).

```javascript
var proxy = new Backbone.Obscura(original);

// Set the transformations on the original collection
proxy
  .setPerPage(25)
  .setSort('age', 'desc')
  .filterBy(function(model) {
    return model.get('age') > 17 && model.get('age') < 70;
  });

// Pass the proxy to a view that knows how to react to a changing collection
var view = new CollectionView({ collection: proxy });

// In another view or a controller, you can modify the state of the filters
if (proxy.hasNextPage()) {
  proxy.nextPage();
}

$('button').on('click', function() {
  proxy.reverseSort();
});
```

[![Build Status](https://secure.travis-ci.org/jmorrell/backbone.obscura.png?branch=master)](http://travis-ci.org/jmorrell/backbone.obscura)

### Where does the name come from?

The camera obscura is an optical device that projects an image of its surroundings 
on a screen. In a similar way, we are using a crude projection of the original
collection to "draw" our views.

![Logo](https://raw.github.com/jmorrell/backbone.obscura/master/img/CameraObscura.jpg)

## Example

```javascript
// TODO
```

## Methods

### new Backbone.Obscura(collection, options)


## Alternative Libraries
[Backbone.Projections](https://github.com/andreypopp/backbone.projections)
[backbone.collectionsubset](https://github.com/anthonyshort/backbone.collectionsubset)

## Installation

### Usage with Browserify

Install with npm, use with [Browserify](http://browserify.org/)

```
> npm install backbone.obscura
```

and in your code

```javascript
var Obscura = require('backbone.obscura');
```

### Usage with Bower

Install with [Bower](http://bower.io):

```
bower install backbone.obscura
```

The component can be used as a Common JS module, an AMD module, or a global.

### Usage as browser global

You can include `backbone.obscura.js` directly in a script tag. Make 
sure that it is loaded after underscore and backbone. It's exported as 
`Backbone.Obscura`.

```HTML
<script src="underscore.js"></script>
<script src="backbone.js"></script>
<script src="backbone.obscura.js"></script>
```

## Testing

Install [Node](http://nodejs.org) (comes with npm) and Bower.

From the repo root, install the project's development dependencies:

```
npm install
bower install
```

Testing relies on the Karma test-runner. If you'd like to use Karma to
automatically watch and re-run the test file during development, it's easiest
to globally install Karma and run it from the CLI.

```
npm install -g karma
karma start
```

To run the tests in Firefox, just once, as CI would:

```
npm test
```

## License

MIT
