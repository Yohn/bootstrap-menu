Bootstrap Context Menu
=============================

A context menu plugin using Bootstrap's dropdown component.

It's made to be usable without having to add any specific HTML for
it in the page, and to allow dynamically changing the state of its options
easily.

Depends on [jQuery](https://jquery.com/). It uses Bootstrap's styling classes, and if using the `iconClass` option, also Font Awesome.


* [See the demos](https://dgoguerra.github.io/bootstrap-menu/demos.html)


Installation
------------

The easiest way to use BootstrapMenu is installing it from NPM:

```
npm install bootstrap-menu
```

and include it with your with your build system ([Browserify](http://browserify.org/), [Webpack](https://webpack.github.io/docs/what-is-webpack.html), etc).

```js
var BootstrapMenu = require('bootstrap-menu');

var menu = new BootstrapMenu('#dropdownButton', {
  actions: /* ... */
});
```

Alternatively you can use the standalone build found at `dist/BootstrapMenu.min.js`. It expects jQuery to be included, and exposes `BootstrapMenu` globally.

```html
<script src="//code.jquery.com/jquery-2.1.4.min.js"></script>
<script src="dist/BootstrapMenu.min.js"></script>

<script>
  var menu = new BootstrapMenu('#dropdownButton', {
    actions: /* ... */
  });
</script>
```

To run the examples locally, run:

```shell
npm install
./build.sh # rebuild dist/
```

Then open a webserver in the project's root:

```shell
node_modules/.bin/static .
# serving "." at http://127.0.0.1:8080
```


Usage
-----

BootstrapMenu receives a string with the selector of the elements to listen to as first argument, and an `options` object as second argument.

The `options` object must have at least a `menuItems` array containing the items to show in the context menu.

Basic example:

```js
var menu = new BootstrapMenu('#button', {
  menuItems: [{
      name: 'Item',
      onClick: function() {
        // run when the item is clicked
      }
    }, {
      name: 'Another item',
      onClick: function() {
        // run when the item is clicked
      }
    }, {
      name: 'A third item',
      onClick: function() {
        // run when the item is clicked
      }
  }]
});
```

Extended example - with divider and submenu:

```js
var menu = new BootstrapMenu('#subMenuDemo', {
  menuItems: [
  {
    name: 'Edit name',
    iconClass: 'fa-pencil',
    onClick: function(row) { /* ... */ },
    isEnabled: function(row) { /* ... */}
  },
  {
      name: 'Edit description',
      iconClass: 'fa-pencil',
      onClick: function(row) { /* ... */ },
      isEnabled: function(row) { /* ... */}
  },
  {
      divider: true
  },
  {
    name: 'Submenu Items',
    iconClass: 'fa-bars',
    classNames: 'dropdown-submenu',
    onClick: function(row) { /* ... */ },
    isShown: function(row) { /* ... */},
    subMenuItems: [
      {
        name: 'Add',
        iconClass: 'fa-plus',
        onClick: function(row) { /* ... */ }
      },
      {
        name: 'Remove',
        iconClass: 'fa-remove',
        onClick: function(row) { /* ... */ }
      }
    ]
  },
  {
    name: 'Set uneditable',
    iconClass: 'fa-lock',
    onClick: function(row) { /* ... */ },
    isShown: function(row) { /* ... */ }
  },
  {
    name: 'Delete row',
    iconClass: 'fa-trash-o',
    onClick: function(row) { /* ... */ },
    isEnabled: function(row) { /* ... */ }
  }
  ]
});
```


Options
-------

#### Context menu initialization options:

| Name | Type | Description |
| ---- | ---- | ----------- |
| `menuSource` | string | What the source of the context menu should be when opened. Valid values are *mouse* and *element*. Defaults to *mouse*. |
| `menuPosition` | string | How to calculate the position of the context menu based on its source. Valid values are *aboveLeft*, *aboveRight*, *belowLeft*, and *belowRight*. Defaults to *belowLeft*. |
| `menuEvent` | string | The event to listen to open the menu. Valid values are *click*, *right-click*, *hover*. Defaults to *right-click*. |
| `fetchElementData` | function | Obtain specific data about the currently opened element, to pass it to the rest of user-defined functions of an action. |
| `menuItems` | array&#124;object | Array or object containing the list of items to be rendered in the context menu. |

#### Menu Item attributes:

Every function attribute is called before rendering the menu each time it is opened. If `fetchElementData` was defined, these functions will receive as first argument its returned value for the currently selected element.

| Name | Type | Description |
| ---- | ---- | ----------- |
| `name` | string&#124;function | The name of the action. |
| `onClick` | function | Handler to run when an action is clicked. |
| `iconClass` | string | Optional, Font Awesome class of the icon to show for the action. |
| `classNames` | string&#124;object&#124;function | Optional, classes to add to the action. |
| `isShown` | function | Optional, decides if the action should be shown or hidden in the context menu. |
| `isEnabled` | function | Optional, decides if the action should appear enabled or disabled in the context menu. |
| `subMenuItems ` | array&#124;object | Array or object containing the list of items to be rendered in a submenu. |


License
-------
MIT license - http://www.opensource.org/licenses/mit-license.php