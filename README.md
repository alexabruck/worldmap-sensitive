# worldmap-sensitive
TopoJSON worldmap with modified country borders

### The final world map is located in the /dist folder


## Process
Map is originally based on the the world maps included in the markmarkoh/datamaps project:
https://github.com/markmarkoh/datamaps/blob/master/src/js/data/world.json

I took their low-resolution map and added countries from the high resolution map that were missing.
The resulting map is a compromise: It doesn't include all dependent territories (some smaller islands that are oversea territories are missing) but it makes sure that all countries are included. 
Borders are roughly drawn, this ensures a small file size.
In the case of island nations which span a multitude of islands the territory is simplified. 

Datamaps' maps are themselves based on shapefiles produced by "Natural Earth": http://www.naturalearthdata.com/downloads/

How I produced the modified maps:
- Original File type: GeoJSON (from datamaps repository). Located in /src folder ("world.json")
- Added territories (feature objects) from higher resolution version. Located in /src folder ("world.hires.json")
- Manually modified the topology via the Application QGIS (having "topological editing" enabled)
- Saved the file as GeoJSON 
- Converted file to TopoJSON via the command line tool geo2topo (Mike Bostock): https://github.com/topojson/topojson/blob/master/README.md 

## United Nations membership status
The GEOJSON feature object associated to each country has a field "memberstate" that encoded UN membership as a boolean (true/false)

## Country names
Country names are according to the official UN listing

## Topological adaptations:
### Border Marocco / Western Sahara
In the original map data (produced by Natural Earth) the territory of Marocco also includes the western part of the disputed territory Western Sahara (from the Atlantic border to the border wall ("berm")). The territory of Western Sahara begins east of the berm.
In the new map the territory of Western Sahara includes the territory to the west of the berm.
The border of Marocco and Western Sahara is being formed by a circle of latitude at 27.6°N.
I've derived this number from the MINURSO deployment map published by the United Nations as of February 2009 (http://www.un.org/Depts/Cartographic/map/dpko/minurso.pdf)
