IMaRS has developed some Google Earth Engine (GEE) scripts to ease the use of common satellite image collections like Sentinel-2 and Landsat.
The goal of these scripts is to reduce the amount of code you need to maintain to do fun things like create Species Distribution Models (SDMs).

The scripts are organized under a single GEE repository (repo) called satellite functions (sat_fns).
Within this repository are files organized by satellite type (eg Sentinel2, Landsat8, WorldView2, etc).
Each of these files made for importing are called **modules**.
To use them you import them into a variable using the javascript `require()` function.
Once the module is loaded into your script, you can then use the functions exported by the module.
Common functions include cloud masking and band ratio calculations.
Below is a minimal example of using the sentinel-2 sat_fns module:

```javascript
// import the Sentinel-2 module
var img_fns = require('users/tylarmurray/sat_fns:s2_fns');

// get the recommended ee.ImageCollection for sentinel-2
var imageCollection = img_fns.imageCollection;

// map the recommended cloud mask onto all images in the collection
imageCollection = imageCollection.map(s2_fns.cloudMask);
```

The details of which image collection is being used and how the cloudmask is being applied is all inside the `users/tylarmurray/sat_fns/s2_fns` script.
The code can be viewed at https://code.earthengine.google.com/?scriptPath=users%2Ftylarmurray%2Fsat_fns%3As2_fns .
Please contact Tylar if you want help understanding or writing up these details.

Now, to do the same thing but using Landsat 8, the only line of code that needs to change is which module is being loaded by the `require()` statement:

```javascript
// import the landsat 8 module
var img_fns = require('users/tylarmurray/sat_fns:ls8_fns');

// get the recommended ee.ImageCollection for sentinel-2
var imageCollection = img_fns.imageCollection;

// map the recommended cloud mask onto all images in the collection
imageCollection = imageCollection.map(s2_fns.cloudMask);
```

More satellites and functions are being added, with the end goal of being able to write code that will work for multiple satellites.
