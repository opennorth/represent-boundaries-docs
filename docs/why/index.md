---
layout: inner-page
title: When to use Represent Boundaries
---

Represent Boundaries has many features in common with [MapIt](http://mapit.poplus.org/), another Poplus component. If you're having trouble choosing between Represent Boundaries and MapIt, here are Represent Boundaries' advantages:

* Represent Boundaries' <a href="{{ site.baseurl }}/docs/import/">definition files</a> give you fine-grained control over how data is loaded into the API, in particular how boundaries are named and identified, without having to write [custom import scripts](https://github.com/mysociety/mapit/tree/master/mapit/management/commands) like in MapIt. If you often need to correct or transform the data in shapefiles, Represent Boundaries is the better choice.
* Represent Boundaries uses **boundary sets** to organize boundaries and to publish metadata, like the data's provenance. MapIt lacks boundary sets, so it can't publish metadata for a boundary set. However, it can still organize boundaries, using area types and boundary hierarchies: for example, [all London wards](http://mapit.mysociety.org/areas/LBW) have the type <abbr title="London borough ward">LBW</abbr>.
* Because MapIt lacks boundary sets, you need to think more carefully about how to organize boundaries. For example, should Scottish and Welsh constituencies be assigned the same generic area type ("constituency"), or should they be assigned unique area types ("Scottish constituency" and "Welsh constituency")? Your choice has an impact on how your users access your data. If you don't want to make these decisions, Represent Boundaries gives you a single, reasonable option.
* Represent Boundaries has **less code**, making it easier to learn and extend. For example, [Represent Maps](https://github.com/JoshData/represent-maps) by Joshua Tauberer extends Represent Boundaries and helps you create beautiful, colorful maps for your website.

If you want to make data from shapefiles available via API quickly and easily, Represent Boundaries will get you there with little fuss. However, MapIt has a few unique features:

* If you don't have geospatial data, you can draw boundaries in the admin interface. With Represent Boundaries, you would draw boundaries using GIS programs like [QGIS](http://www.qgis.org/), which create shapefiles for you to import.
* A boundary can be assigned a parent and children to create a hierarchy. (This is separate from querying which boundaries contain others, which both components can do.)
* Area types can organize boundaries *across* boundary sets to produce, for example, a list of all wards in all cities. Represent Boundaries would list wards one city at a time.
* A boundary (United Kingdom) can be assigned multiple names ("Regno Unito") and codes ("GB"). Represent Boundaries limits you to the data in the shapefile.
* MapIt has several features relating to postcodes. With Represent Boundaries, you would author an extension, like [Represent Postcodes](https://github.com/rhymeswithcycle/represent-postcodes/) for Canada.

## Changes over time

Each component handles changes over time differently. In Represent Boundaries, a common, simple pattern namespaces boundary sets with a year: for example, `federal-electoral-districts-2003` versus `federal-electoral-districts-2013`. In the next major release of Represent Boundaries, you can also set a `start_date` and an `end_date` on boundary sets and query boundaries across time with an `at` filter.

In MapIt, before importing the 2013 federal electoral districts, for example, you would create a new generation. All the boundaries from the previous generation would continue into the new generation, with the exception of the 2003 federal electoral districts. If you want to query the 2003 federal electoral districts, you have to know which generation it was part of, making it more difficult to query historical data.
