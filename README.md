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
- an index.php file where you will need to dynamically create <a-marker> elements for each piece of data

Example:
```
<body>
    <a-scene id="ARScene" embedded arjs='sourceType: webcam; debugUIEnabled: false; detectionMode: mono;'>
        <?php
		$myfile = fopen("markers.json", "r") or die("Unable to open file!");
		$decoded = json_decode(fread($myfile, filesize('markers.json')));

		for($i = 0; $i < sizeof($decoded); $i++){
			echo '<a-marker id="' . $i .'" preset="custom" url="markers/' . $i . '.patt"></a-marker>';
		}
		fclose($myfile);
		?>
        <a-entity camera></a-entity>
    </a-scene>
    
    <!-- rest of body -->
</body>
```

## Step-by-step Guide

1. Create a file called `markers.json` to store an array of Objects to parse as your marker data
2. Add the following lines inside the `<a-scene>` tag in your `index.php` file:

```
<?php
$myfile = fopen("markers.json", "r") or die("Unable to open file!");
$decoded = json_decode(fread($myfile, filesize('markers.json')));

for($i = 0; $i < sizeof($decoded); $i++){
	echo '<a-marker id="' . $i .'" preset="custom" url="markers/' . $i . '.patt"></a-marker>';
}
	fclose($myfile);
?>
```

This reads the file and creates the number of `<a-marker>` tags with enumerated IDs equal to the number of objects in your `markers.json`.

3. In your `sketch.js` file, create a callback function for what you want to happen when a marker is found
Example:

```
//Callback function, prints the data of the marker
function markerFound(data) {
    console.log("Marker found with data:", data);
}
```
This will be passed into the higher-order function

4. In your `setup()` function, pass in your callback function to `matchMarkers()`
Example:
```
function setup() {
  matchMarkers(markerFound);
  //rest of setup
}
```

5. Modify your `draw()` function to only search for markers if a marker is not found by creating a boolean variable, initially set to false. Set it to true once a marker is found, but make sure you have a function that sets it back to false, otherwise your program will only search once.

6. Call `executeFound()` on a marker if it's found.
Example:
```
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

All set! 
