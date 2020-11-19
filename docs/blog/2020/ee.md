# Google earth engine functionality 



- ```image.cumulativeCost()``` to compute a cost map where every pixel contains the total cost of the lowest cost path to the nearest source location  [source](https://developers.google.com/earth-engine/guides/image_cumulative_cost)

Need:
	- need image in which each pixel represents the cost per meter to traverse it

	- Impact factors in human travel
		- Traffic network infrastructure
		- Terrain specifics (where no infrastructure exists)

