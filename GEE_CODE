//Create Desired Extent by Drawing Geometry 
//Import Post-Event Imagery
var image = ee.ImageCollection('COPERNICUS/S2')
   //.filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 10))
  .filterDate('2017-11-01', '2017-11-05')
  .filterBounds(geometry)
print(image)
var medianpixels = image.median()
var medianpixelsclipped = medianpixels.clip(geometry).divide(10000)
Map.addLayer(medianpixelsclipped, {bands: ['B4', 'B3', 'B2'], max:0.3}, 'Sent-2 After Maria' )
Map.centerObject(medianpixelsclipped, 9);

//Create Post-NDVI Map
var ndvi = medianpixelsclipped.normalizedDifference(['B4', 'B8']);
Map.addLayer(ndvi, {min: -1, max: 1, palette: ['green', 'white']}, 'NDVI After Maria');

// Import Pre-Event Imagery
var image3 = ee.ImageCollection('COPERNICUS/S2')
   //.filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 10))
  .filterDate('2017-04-05', '2017-04-09')
  .filterBounds(geometry)
print(image3)
var medianpixels3 = image3.median()
var medianpixelsclipped3 = medianpixels3.clip(geometry).divide(10000)
Map.addLayer(medianpixelsclipped3, {bands: ['B4', 'B3', 'B2'], max:0.3}, 'Sent-2 Before Maria' )
Map.centerObject(medianpixelsclipped3, 9);

//Create Pre-NDVI Map
var ndvi3 = medianpixelsclipped3.normalizedDifference(['B4', 'B8']);
Map.addLayer(ndvi3, {min: -1, max: 1, palette: ['green', 'white']}, 'NDVI Before Maria');

// Create NDVI Difference Map
var diff = ndvi3.subtract(ndvi);
Map.addLayer(diff,
             {min: -2, max: 2, palette: ['white', 'blue']},
             'NDVI Difference');            
             
//Uncomment this to export the image, specifying scale and region.Region can be imported geometry or watershed. 
//Export.image.toDrive({
  //image: diff,
 // description: 'Difference Map',
 // scale: 10,
  //region: geometry
//});



