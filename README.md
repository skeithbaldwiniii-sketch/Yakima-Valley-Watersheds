# Yakima-Valley-Watersheds
## Hydrological Analysis of Hop Farms in Yakima County, WA

Modeling watershed and drainage systems using DEM-based tools (flow direction, accumulation, watershed) to evaluate water accessibility for agricultural sites 

This was my first final project in the Geographical Information Systems certificate program at Northern Virginia Community College, which I completed December 2024. It is now April 2026, so my memory may be a little fuzzy but it is also a walk down memory lane. 

The reason I picked this topic was because it combined the field I was a part of when I started the certificate program, with the field I wished to jump into. 

From *The Hop Grower's Handbook*:

> “Hops have a complicated relationship with water that makes two seemingly opposite things nonnegotiable when siting the hop yard – access to a lot of water and the ability to make water go away quickly through drainage and evaporation.”

> “A single hop needs about 16 gallons of water a week. This means a 1-acre hop yard containing approximately nine-hundred plants could need access to almost 15,000 gallons of water on a weekly basis.” – Eyck and Gehring, 58

With these two quotes in mind, it is important to consider a) where the water is coming from and b) what is downstream/where the water is going. 

First step was isolating the county & its boundaries. Part of this was with the intention of having a defining line to use with the clip tool, the other intention was with presentation in mind. My thought was that if I dulled the surrounding counties with a bland color, it would draw attention to Yakima, which is our county of focus. 

I got these county boundaries from the Washington State Geospatial Open Data Portal. After I added to ArcGIS Pro, I used the "create layer from selection" tool to isolate Yakima County and the surrounding counties 

Next step was downloading the layer of all the streams in the state & adding to the project. This was also available on the Washington State Geospatial Open Data Portal labeled Hydrography. 

Next, I needed to locate all of the commercial farms that grow hops. I was able to find a list of these on the Yakima Chief Ranches website under 'Our History'. I then plugged all of these farms into Google Earth, dropped a pin, then exported the group of pins as a KMZ file to be added into ArcGIS Pro. I then used the "KML to layer" tool to convert the format into a layer shapefile that allowed me to adjust the Symbology. 

Seeing all of these farms displayed in conjunction with the streams layer, there's a fair amount of distance between the farms and the streams themselves. So I dug a little further to find a much more detailed layer of the hydrography. I found this on the Department of Natural Resources GIS Open Data portal. 

Next, in an attempt to practice raster analysis, I downloaded the DEM of the area from the National Map. 
The tools I used were as follows:
1. Fill
2. Flow Direction
3. Flow Accumulation
4. Raster Calculator (>= 50000)
5. Stream Order
6. Stream to Feature
These series of tools providied me a layer of the streams by using the DEM raster. With this in hand, I can determine the watershed within the valley. To do this, I picked one farm, I just went with Perrault Farms, and used the create layer from selection tool to isolate the individual point. I then used the snap pour point tool, which gave me a pour point to apply to the watershed tool, which gave me a picture of the entire watershed.

This result showed me that all of the farms in Yakima Valley were all within the same water system. 

My final question was concerning altitude to see which direction was downstream. I found a helpful layer on the Yakima County GIS portal, from a project titled 'groundwater management area' that had the altitude. I had to isolate the individual layer, and achieved my final image. 
