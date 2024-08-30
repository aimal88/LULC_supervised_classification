# LULC_supervised_classification
LULC supervised classification
// Visualize Dynamic World landcover dataset 
// ---------------------------------------------------------

var dynWorld = ee.ImageCollection("GOOGLE/DYNAMICWORLD/V1")
.filterDate('2012-01-01','2022-12-31')
.select('label') ;

var dyn_landcover = dynWorld.reduce(ee.Reducer.mode())
.clip(roi.geometry());

// Create a visualization palette
var VIS_PALETTE = [
    '419BDF', '397D49', '88B053', '7A87C6',
    'E49635', 'DFC35A', 'C4281B', 'A59B8F',
    'B39FE1'];

Map.centerObject(roi, 11);
Map.addLayer(dyn_landcover, {min: 0, max: 8, palette: VIS_PALETTE}, "Dynamic World LUCL");
