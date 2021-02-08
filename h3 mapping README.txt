The H3 Mapping framework takes a set of geographic locations in CSV file format, and generates an map using the Folium mapping library for Python.  It converts the inputted latitude/longitude coordinates into a set of Uber's H3 hexagon codes at a specified resolution, that can then be plotted on the folium map.  Hexagons grids are plotted based on the number of unique resolution values in the input file.  Each hexagon is then color coded by some specified color scheme (in hexadecimal format) that creates a visual distinction of location counts in the input file.  Each hexagon can also be clicked on the folium map, and a popup will appear describing the weight of that location, as well as it's parent location.  

The input CSV table MUST contain the following fields (all lowercase):
--"name" - A string denoting the name of the location.  
--"latitude" - a floating point value denoting the latitude coordinate
--"longitude" - a floating point value denoting the longitude coordinate
--"parent" - A string denoting the parent location (i.e. the parent for 'Denver' would be 'Colorado')
--"resolution" - an integer value (between 0 and 15) denoting the resolution to generate the hexagon for that location

The function generate_h3_map() takes a filename string as the input file, and a list of a strings denoting hexadecimal color values to use for plotting.  When called, a blank map will generate, and there will be a layer control window in the top right corner.  Clicking each layer will show the hexagon grids.  

Parent locations:
The 'parent' field exists for increasing counts in smaller-scale locations that are already plotted (smaller resolution value).  The H3 framework looks at each parent location and searches for a matching location name.  If one exists, the weight for that hexagon gets increased.  All weights for all parent locations will be updated to the smallest resolution layer.  For example, the location "Los Angeles" may have a parent location of "California" which may have a parent location "United States".  All these parent locations are then updated.