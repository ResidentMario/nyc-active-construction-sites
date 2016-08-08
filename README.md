## About

This project is a proof-of-concept implementation of `co_reader` (a version of which distributed in this library, but
see also the [`co_reader` repo](https://github.com/ResidentMario/co_reader) for the most recent version), a module
for reading building-level certificate of occupancy date data off of the New York City Department of Building's
`BISweb` interface, for generating a map of active construction sites in New York City.

It works by taking the dataset of active new building permits in New York City (a slice-and-dice of the [DOB Permit
Issuance dataset](https://data.cityofnewyork.us/Housing-Development/DOB-Permit-Issuance/ipu4-2q9a)) and using the
aforementioned module to check whether or not the site has already been issued a certificate of occupancy&mdash;a
document certifying that a newly constructed (or heavily reconstructed) building is safe for inhabitation, and the
traditional end of a new building construction job. If it has, this construction site has finished; if not, it is
still active. This latter classification is the one we are interested in.

Generating this data for the first time is a laborious process because you have to run every non-expired permit
through BISweb, which takes a long time. If this process were to be routinized a large gain can be made by caching
prior "already finished" results, but it would still be very time-consuming. If only the DOB released this data
directly...

The map (the end product) is generated via a spatial join against the [MapPLUTO](http://www1.nyc.gov/site/planning/data-maps/open-data/pluto-mappluto-archive.page)
geospatial dataset (see the responsible notebook for details). Generating the final geospatial map, as implemented,
requires heinous resources due to the size of the core geospatial file. You cna rewrite it a bit to be way more
efficient, of course, but this was all run on a desktop with 16 GB ram, so...

The map distributed here is current as of the time this POC was run: late June 2016.

**You can see the map yourself in [this public block](http://bl.ocks.org/ResidentMario/1b83027f540ee316b8f18847dc17816b).**
