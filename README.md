# Yakima-Valley-Watersheds
## Hydrological Analysis of Hop Farms in Yakima County, WA

Modeling watershed and drainage systems using DEM-based tools (flow direction, accumulation, watershed) to evaluate water accessibility for agricultural sites 

This project focuses on modeling watershed and drainage systems in Yakima County using DEM-based tools (flow direction, flow accumulation, watershed) to better understand water accessibility for hop farms.

This was my first final project in the Geographical Information Systems certificate program at Northern Virginia Community College, completed in December 2024. Looking back on it now, it’s a good mix of where I came from (working in the brewing industry) and where I wanted to go (GIS and environmental analysis).

## Why This Matters

From *The Hop Grower's Handbook*:

> “Hops have a complicated relationship with water that makes two seemingly opposite things nonnegotiable when siting the hop yard – access to a lot of water and the ability to make water go away quickly through drainage and evaporation.”

> “A single hop needs about 16 gallons of water a week. This means a 1-acre hop yard containing approximately nine-hundred plants could need access to almost 15,000 gallons of water on a weekly basis.” – Eyck and Gehring, 58

Hops require a large and consistent water supply, while also needing effective drainage. That raised two key questions for me:

- Where is the water coming from?
- Where is it going after it moves through the system?

Understanding that relationship is critical for both farm productivity and long-term water management.

## Initial Data & Setup

I started by isolating Yakima County and its surrounding counties using boundary data from the Washington State Geospatial Open Data Portal. This gave me a clean study area and also helped with visualization by muting surrounding regions.

<img width="531" height="359" alt="Screenshot 2024-11-30 090029" src="https://github.com/user-attachments/assets/243f6d4e-981c-4086-9fce-6e1d2e793209" />


Next, I added a statewide hydrography layer to get an initial sense of stream locations.

<img width="531" height="359" alt="Screenshot 2024-11-30 090839" src="https://github.com/user-attachments/assets/51f6775b-8f34-44be-ba62-0aba0bfc77a7" />


After that, I mapped the hop farms themselves. I pulled a list of commercial farms from Yakima Chief Ranches, located them in Google Earth, and exported the points as a KMZ file. I then converted that into a shapefile in ArcGIS Pro so I could work with it more easily.

<img width="550" height="415" alt="Screenshot 2024-11-30 091749" src="https://github.com/user-attachments/assets/03956f15-1d0e-45d3-baed-5556ce3ce0fd" />


<img width="531" height="359" alt="Screenshot 2024-11-30 094907" src="https://github.com/user-attachments/assets/8890a606-c963-4187-acc7-3c409cd59d37" />

<img width="250" height="250" alt="Screenshot 2024-11-30 095002" src="https://github.com/user-attachments/assets/e722c3d9-5f6f-4f1a-8a82-c38f90cc21f2" />

<img width="531" height="359" alt="Screenshot 2024-11-30 095110" src="https://github.com/user-attachments/assets/cf7027d1-ce86-4f51-b59c-12b8d4df28df" />

At this stage, I noticed that many farms didn’t appear to sit directly near mapped streams, which led me to look for a more detailed hydrography dataset from the Department of Natural Resources.

<img width="530" height="360" alt="Screenshot 2024-11-30 091104" src="https://github.com/user-attachments/assets/82854a63-e7fe-44d5-a182-51cb622a95f5" />

<img width="250" height="250" alt="Screenshot 2024-11-30 091320" src="https://github.com/user-attachments/assets/8e388ff0-5bb2-4a6d-aa70-a223b493bea7" />

<img width="530" height="360" alt="Screenshot 2024-11-30 091429" src="https://github.com/user-attachments/assets/82df3c35-986e-4c45-8901-33fb71d0a287" />


## Raster-Based Hydrology Workflow

To go beyond existing vector data, I brought in a DEM from the US National Map and built a hydrology model from scratch.

The workflow was:

1. Fill – removed sinks in the DEM to ensure continuous flow
2. Flow Direction (D8) – assigned each cell a direction of steepest descent
3. Flow Accumulation – calculated how much upstream area contributes flow into each cell
4. Raster Calculator (≥ 50,000) – isolated major flow paths
5. Stream Order – classified the stream network
6. Stream to Feature – converted raster streams into vector lines

The 50,000 threshold was chosen to highlight major drainage paths while filtering out minor noise. I adjusted this value until the resulting stream network reasonably matched known hydrography.

## Watershed Delineation

With the stream network established, I moved on to watershed analysis.

I started by selecting a single farm (Perrault Farms) as a test case. Before running the watershed tool, I needed to make sure the outlet point was actually aligned with the modeled flow network. When placing points manually, they’re usually slightly off, which can throw off the results.

To fix this, I used the Snap Pour Point tool to shift the farm location to the nearest high-flow cell in the accumulation raster. This ensured the point represented a true drainage outlet.

With that corrected point, I used the Watershed tool to identify the full upstream area contributing flow to that location. Using the flow direction raster, the tool traces all cells that drain into the selected point and defines the watershed boundary.

<img width="530" height="360" alt="Screenshot 2024-11-30 131936" src="https://github.com/user-attachments/assets/9291f011-4a33-4716-8da7-ad3db4a66f6b" />

<img width="530" height="360" alt="Screenshot 2024-11-30 133452" src="https://github.com/user-attachments/assets/48448f26-0072-4c29-a895-b076da98bd5c" />

<img width="530" height="360" alt="Screenshot 2024-11-30 133552" src="https://github.com/user-attachments/assets/308125b2-979a-4b92-bb5b-f18a6af1b04e" />

<img width="250" height="250" alt="Screenshot 2024-11-30 134455" src="https://github.com/user-attachments/assets/1cc97943-d4ef-41da-91ed-a0d87a0e5d2c" />

<img width="250" height="250" alt="Screenshot 2024-11-30 134523" src="https://github.com/user-attachments/assets/d81e2419-3389-45df-acf0-465a9e702146" />

<img width="530" height="360" alt="Screenshot 2024-11-30 134824" src="https://github.com/user-attachments/assets/85e07f09-499c-4598-95b8-d0e4e0d6660a" />

This result showed me that all of the farms in Yakima Valley were all within the same water system. 

<img width="250" height="250" alt="Screenshot 2024-11-30 135148" src="https://github.com/user-attachments/assets/def9890b-a119-4c79-ae29-3c56d7728be6" />

<img width="530" height="360" alt="Screenshot 2024-11-30 135810" src="https://github.com/user-attachments/assets/d26825a4-aed8-4c6e-b71c-06a5d928dcf1" />

## Results & Observations

The watershed output showed that the analyzed farm falls within a larger, connected drainage system. Based on additional spatial context (farm distribution, stream networks, and elevation), this suggests that many of the hop farms in Yakima Valley likely share interconnected water systems.

To better understand flow direction, I incorporated an elevation layer from the Yakima County GIS portal. This made it clear how water moves from higher elevation farms to lower ones across the valley.

<img width="530" height="360" alt="Screenshot 2024-11-30 100158" src="https://github.com/user-attachments/assets/852b9cc8-a000-41ad-88ab-43ef59db51db" />

<img width="530" height="360" alt="Screenshot 2024-11-30 140528" src="https://github.com/user-attachments/assets/d4354373-1222-4d5b-b973-7764c659fa8c" />

## Key Takeaways

- Farms in the region are not isolated in terms of water systems
- Upstream activity has direct implications for downstream farms
- Water quality and availability should be considered at a watershed level, not just at individual sites

If a downstream farm experiences water quality issues, this type of analysis makes it possible to trace potential sources upstream.

## Limitations

- The watershed analysis was demonstrated using a single farm as a representative example
- Farm locations were manually geocoded, which may introduce minor positional error
- The flow accumulation threshold influences the derived stream network
- The model does not account for seasonal variation or groundwater dynamics

## Final Thoughts 

This project helped me understand how raster-based hydrology tools can be used to model real-world systems. More importantly, it showed how GIS can connect environmental processes to practical decisions, especially in agriculture where water management is critical.

If expanded further, this analysis could be applied across multiple farms to better support regional water planning and conservation efforts.


