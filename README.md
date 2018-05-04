# A Frame Marker Tagger
Generic helper function for tagging markers

## Dependencies
This framework uses AJAX, so you need to have JQuery included before this file

## Usage
Simply include the `marker_tagger.js` file as a script tag at the end of your html/php file

```
<script src="marker_tagger.js"></script>
```

## Things you need
The function `matchMarkers` requires the following:

- a JSON file structured as an Array of objects. 
Example:

```
[
    {
        "id": 0,
        "name": "Woman with Plants",
        "year": 1929,
        "artist": "Grant Wood",
        "url": "https://uploads3.wikiart.org/images/grant-wood/woman-with-plants-1929.jpg"
    }
]
```

- a callback function to be executed each time a marker is found
- a condition to stop the search

Example:
```
//Callback function, prints the data of the marker
function markerFound(data) {
    console.log("Marker found with data:", data);
}

//Aframe P5 Setup
function setup() {
  matchMarkers(markerFound);
}

function draw() {
  if (!found) {
    for (let i = 0; i < markers.length; i++) {
      if (markers[i].isVisible()) {
        const thisMarker = markers[i];
        world.clearDrawingCanvas();
        found = true;
        thisMarker.executeFound();
      }
    }
  }
}
```

## In-Depth Guide

There is already a `markers` array defined in `marker_tagger.js`. This is where your markers will be stored. 

The function `matchMarkers(callback)` takes in a callback function that you will have to define yourself.
