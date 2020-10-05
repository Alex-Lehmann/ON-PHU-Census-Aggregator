Census Data Aggregator - Ontario Health Regions
Author: Alex Lehmann

Downloads Statstics Canada census data for Ontario via the CensusMapper API and
aggregates data to the health unit level. Data for census subdivisions overlapping
multiple health regions is scaled by the proportion of population actually living in the
health region. Specific features to retrieve are encoded in the Vector_Map-CA16 file.
Requires a CensusMapper API key.

I didn't bother rewriting this as a function and packaging it since this will likely only
have to run once or twice, so you'll have to edit the script directly to set it up on your
machine.

Configuration:
1) Copy and paste the "data" folder into your project root directory. Put the "get_hr_census.R" file
   anywhere in your project.

2) Open "get_hr_census.R" in your preferred text editor/R IDE and make the following changes:
	a. Put your project root directory path inside the quotation marks in line 14
	b. Put your CensusMapper API key inside the quotation marks in line 20
	c. Put your desired destination, including filename with .csv extension, in the quotation marks
	   in line 118

3) Open ROOT/data/censusmapper/Vector_Map-CA16.csv. Add each desired feature to query as a row
   according to the following schema:
	Vector: The CensusMapper vector referring to the desired feature. Call
		list_census_vectors("CA16") in R for a full list of vectors.
	Label: The desired column name for the feature
	Description: A human-readable description of the feature. Not used in computation
	To_Scale: TRUE if the feature should be scaled based on population in the case of a district
		  overlapping multiple health units. FALSE otherwise.
	Aggregation: The method used to aggregate data to higher levels. Currently only supports means
		     and sums since medians don't play nice when going from subsets to full population.
   Examples are provided.