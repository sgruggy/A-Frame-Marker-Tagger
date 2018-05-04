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

