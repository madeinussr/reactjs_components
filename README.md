# Some React.js components

## Modal window
Just a modal window component. Dependent on React.addons.CSSTransitionGroup.

### Usage
Here is the trigger method and it's params:
```javascript
reactModal = function (containerId, headerTitle = '', bodyContent = '', additionalClasses = {}, onShow = null, onHide = null)
```

```html
<a class="klass" onclick="reactModal('new-modal', 'New Modal', $('#new-modal-body').html(), {content: 'content_class', header: 'header_class', body: 'body_class'}, function(){}, function(){});">Show modal</a>
```
It creates a modal container div (if no proper container was found with provided containerId), appends it to body and triggers the 'show' state param.

### Events
There are two events supported at the moment:
* onShow
* onHide

### additionalClasses
Used in order to add custom CSS classes to default modal window elements:
* content (wrapper)
* header
* title
* body

## Leaflet map
React wrapper for Leaflet map + some abstractions over map events.

### Call function
```javascript
@mapInstance = (options) ->
  React.createElement(Map, options)
```

### Options (supported events groups & layers)
```javascript
center: React.PropTypes.array,
zoom: React.PropTypes.number,
onMapHandlers: React.PropTypes.object,
features: React.PropTypes.array,
featuresStyle: React.PropTypes.object,
featuresHighlightedStyle: React.PropTypes.object,
onFeatureHandlers: React.PropTypes.object,
markers: React.PropTypes.array,
pathLines: React.PropTypes.bool,
pathLinesStyle: React.PropTypes.object,
onMarkerHandlers: React.PropTypes.object,
setFocusOnLastMarker: React.PropTypes.bool,
markerDraggingEnable: React.PropTypes.bool
```

### Usage
```javascript
var onMapClick = function(e) {
    var popLocation= e.latlng;
    var popup = L.popup()
        .setLatLng(popLocation)
        .setContent('<a>Hello</a>')
        .openOn(this);
};
var onMarkerClick = function(e) {
    e.target.bindPopup('World!');
};
var markers = [{lat:1.23, lng:3.45},{lat:2.34, lng:4.56}];
React.render(mapInstance({markers:markers, onMapHandlers:{click:onMapClick}, onMarkerHandlers:{click:onMarkerClick}}), document.getElementById('worldmap'));
```
You can always reference the created leaflet map object from your javascript because of
```javascript
@map = window.map
```