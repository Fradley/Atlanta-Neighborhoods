<link rel='stylesheet' href='https://cdn.jsdelivr.net/gh/kognise/water.css@latest/dist/dark.css'>

# Introduction  
We are interested in determining the optimal location for a fancy french fry boutique. In Atlanta, there could be demand for a late-night gourmet french fry boutique to accompany the active night life. Our french fry boutique will not offer many entrees and will focus on snacks and secondarily on drinks.  
  
We expect this type of restaurant to have a number of influencing factors, even if the specific restaurant type is somewhat unique.  
* The food targets younger audiences  
* Expensive menu favors higher income area  
* Adjacency to bars and other late night attractions makes our restaurant a convenient stop in a busy night  
* Pedestrian traffic would lead to more first time customers  
  
* Fast food would detract because it provides cheaper, if lower quality, comfort food

# Data
To determine the optimal location, I used a number of data sets.  
* NPU geojson to determine crimes per region  
* Statistics of the various neighborhoods (Income, Rent, Housing, Population, Age, Transit statistics)  
* Data gathered from Foursquare containing attractions nearby each neighborhood  
* Crime data to overlay on the geojson to determine perception of safety of each neighborhood  
  
Here is the map of the crime data:  
<iframe src="https://fradley.github.io/Atlanta-Neighborhoods/atl_crime_map.html" height="750" width="750"></iframe>


# Methodology  
## Safety  
We evaluated a neighborhood's safety by counting the number of violent crimes in a region. Because we are interested in the perceived danger of a region, the total number of violent crimes is more relevant than the per capita representation. We then had to broadcast the number of crimes down to the individual neighborhoods, which subdivide the neighborhood planning units.

## Attractions  
We were able to determine the attractions for each neighborhood by first using Google Maps API to determine the representative coordinates for each neighborhood. We then used the representative point to find all attractions within a certain radius (1 km). We determined compatible attractions and used those to define a classification of whether an area was a good candidate for our restaurant.

## Analysis  
We scaled the data so it could be used by our machine learning algorithms. We began by trying a similar procedure as the Toronto neighborhoods project. Unfortunately, we were unable to generate good clusters when looked at with silhouette analysis. The solution was to refine the question to a classification problem rather than clustering. The similar venue categories were determined to be: 'Gastropub', 'Burger Joint', 'Candy Store', 'Dive Bar', 'Fish & Chips Shop', 'Fried Chicken Joint'. Notable exceptions are various cultural and fast food categories. By training a K-Nearest Neighbors model on the combined Neighborhoods and venues datasets, we could filter most of the neighborhoods. Finally, we gathered the result by assigning importance to low age, low crime, and high income. We used binning to smooth over minute differences before doing a multicolumn sort to determine the most compatible neighborhoods.

# Results 

<iframe src="https://fradley.github.io/Atlanta-Neighborhoods/ResultMap.html" height="750" width="750"></iframe>

Our analysis identifies Inman park as our prime candidate with Buckhead Forest, Ardmore, Howell Station, and Grant Park as potential alternatives. These locations are defined by having appropriate income levels, age, and lower crime rates while also having attractions deemed to be compatible with our gourmet french fry boutique. While this does not imply that we should build a french fry boutique, if we were to do so anyway, the contribution of location to success would be greatest at these locations.  

# Conclusion

The purpose of this project was to determine the best locations for a French Fry Boutique in the city of Atlanta, Georgia to focus stakeholder discussions. By classifying the data based on whether it is compatible wth certain types of attractions, we generated a short list of attractions, which we then binned and sorted to allow the neighborhoods with the most desirable attributes rise to the top. Further development in this project may profit from using natural language processing to analyze social media or franchise growth data to determine demand.
