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

<img width="531" height="359" alt="Screenshot 2024-11-30 090029" src="https://github.com/user-attachments/assets/243f6d4e-981c-4086-9fce-6e1d2e793209" />


I got these county boundaries from the Washington State Geospatial Open Data Portal. After I added to ArcGIS Pro, I used the "create layer from selection" tool to isolate Yakima County and the surrounding counties 

Next step was downloading the layer of all the streams in the state & adding to the project. This was also available on the Washington State Geospatial Open Data Portal labeled Hydrography. 

<img width="531" height="359" alt="Screenshot 2024-11-30 090839" src="https://github.com/user-attachments/assets/51f6775b-8f34-44be-ba62-0aba0bfc77a7" />


Next, I needed to locate all of the commercial farms that grow hops. I was able to find a list of these on the Yakima Chief Ranches website under 'Our History'. I then plugged all of these farms into Google Earth, dropped a pin, then exported the group of pins as a KMZ file to be added into ArcGIS Pro. I then used the "KML to layer" tool to convert the format into a layer shapefile that allowed me to adjust the Symbology. 

<img width="550" height="415" alt="Screenshot 2024-11-30 091749" src="https://github.com/user-attachments/assets/03956f15-1d0e-45d3-baed-5556ce3ce0fd" />


<img width="531" height="359" alt="Screenshot 2024-11-30 094907" src="https://github.com/user-attachments/assets/8890a606-c963-4187-acc7-3c409cd59d37" />

<img width="250" height="250" alt="Screenshot 2024-11-30 095002" src="https://github.com/user-attachments/assets/e722c3d9-5f6f-4f1a-8a82-c38f90cc21f2" />

<img width="531" height="359" alt="Screenshot 2024-11-30 095110" src="https://github.com/user-attachments/assets/cf7027d1-ce86-4f51-b59c-12b8d4df28df" />


Seeing all of these farms displayed in conjunction with the streams layer, there's a fair amount of distance between the farms and the streams themselves. So I dug a little further to find a much more detailed layer of the hydrography. I found this on the Department of Natural Resources GIS Open Data portal. 

<img width="530" height="360" alt="Screenshot 2024-11-30 091104" src="https://github.com/user-attachments/assets/82854a63-e7fe-44d5-a182-51cb622a95f5" />

<img width="250" height="250" alt="Screenshot 2024-11-30 091320" src="https://github.com/user-attachments/assets/8e388ff0-5bb2-4a6d-aa70-a223b493bea7" />

<img width="530" height="360" alt="Screenshot 2024-11-30 091429" src="https://github.com/user-attachments/assets/82df3c35-986e-4c45-8901-33fb71d0a287" />


Next, in an attempt to practice raster analysis, I downloaded the DEM of the area from the National Map. 
The tools I used were as follows:
1. Fill
2. Flow Direction
3. Flow Accumulation
4. Raster Calculator (>= 50000)
5. Stream Order
6. Stream to Feature
These series of tools providied me a layer of the streams by using the DEM raster. With this in hand, I can determine the watershed within the valley. To do this, I picked one farm, I just went with Perrault Farms, and used the create layer from selection tool to isolate the individual point. I then used the snap pour point tool, which gave me a pour point to apply to the watershed tool, which gave me a picture of the entire watershed.

<img width="530" height="360" alt="Screenshot 2024-11-30 131936" src="https://github.com/user-attachments/assets/9291f011-4a33-4716-8da7-ad3db4a66f6b" />

<img width="530" height="360" alt="Screenshot 2024-11-30 133452" src="https://github.com/user-attachments/assets/48448f26-0072-4c29-a895-b076da98bd5c" />

<img width="530" height="360" alt="Screenshot 2024-11-30 133552" src="https://github.com/user-attachments/assets/308125b2-979a-4b92-bb5b-f18a6af1b04e" />

<img width="250" height="250" alt="Screenshot 2024-11-30 134455" src="https://github.com/user-attachments/assets/1cc97943-d4ef-41da-91ed-a0d87a0e5d2c" />

<img width="250" height="250" alt="Screenshot 2024-11-30 134523" src="https://github.com/user-attachments/assets/d81e2419-3389-45df-acf0-465a9e702146" />

<img width="530" height="360" alt="Screenshot 2024-11-30 134824" src="https://github.com/user-attachments/assets/85e07f09-499c-4598-95b8-d0e4e0d6660a" />

This result showed me that all of the farms in Yakima Valley were all within the same water system. 

<img width="250" height="250" alt="Screenshot 2024-11-30 135148" src="https://github.com/user-attachments/assets/def9890b-a119-4c79-ae29-3c56d7728be6" />

<img width="530" height="360" alt="Screenshot 2024-11-30 135810" src="https://github.com/user-attachments/assets/d26825a4-aed8-4c6e-b71c-06a5d928dcf1" />


My final question was concerning altitude to see which direction was downstream. I found a helpful layer on the Yakima County GIS portal, from a project titled 'groundwater management area' that had the altitude. I had to isolate the individual layer, and achieved my final image. 

<img width="530" height="360" alt="Screenshot 2024-11-30 100158" src="https://github.com/user-attachments/assets/852b9cc8-a000-41ad-88ab-43ef59db51db" />

<img width="530" height="360" alt="Screenshot 2024-11-30 140528" src="https://github.com/user-attachments/assets/d4354373-1222-4d5b-b973-7764c659fa8c" />

