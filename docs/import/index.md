---
layout: inner-page
title: Add data to the API
---

Represent Boundaries loads geospatial data in the [shapefile](http://en.wikipedia.org/wiki/Shapefile) format. Other formats like KML and GeoJSON can be converted to shapefile using tools like [ogr2ogr](http://www.gdal.org/ogr2ogr.html). Before using Represent Boundaries, collect the geospatial data that you need. For example, collect Canada's <a href="http://data.gc.ca/data/en/dataset/48f10fb9-78a2-43a9-92ab-354c28d30674">federal electoral districts</a>:

```bash
curl -O http://www12.statcan.gc.ca/census-recensement/2011/geo/bound-limit/files-fichiers/gfed000a11a_e.zip
```

You've got your shapefiles? Next, write **definition files** that describe how to load shapefiles into the API. When a shapefile is loaded, a **boundary set** is created for the shapefile and a **boundary** is created for each polygon feature in the shapefile. See the [sample definition file](http://github.com/opennorth/represent-boundaries/blob/master/definition.example.py) to learn how to control how shapefiles are loaded. Most parameters in a definition file are optional. Here's a minimal definition file for Canada's federal electoral districts:

```python
from datetime import date

import boundaries

boundaries.register('Federal electoral districts',
    encoding='iso-8859-1',
    last_updated=date(2011, 11, 28),
    name_func=boundaries.clean_attr('FEDENAME'),
    slug_func=boundaries.attr('FEDUID'),
)
```

The `loadshapefiles` command looks for definition files, ending in `definition.py` or `definitions.py`, in `my_project/data/shapefiles`. You can change this path by setting `BOUNDARIES_SHAPEFILES_DIR` in `my_project/settings.py`. Represent Boundaries will walk the directory tree looking for definition files, so you may organize your shapefiles any way you like. [OpenStates.org](https://github.com/sunlightlabs/pentagon/blob/master/shapefiles/definitions.py) puts the shapefiles in subdirectories with a single top-level definition file, while [Represent](https://github.com/opennorth/represent-canada-data) creates a tree with a definition file in each directory containing a shapefile.

If you've been following the example, move the shapefile and definition file for Canada's federal electoral districts into `my_project/data/shapefiles`. You can now run:

    python manage.py loadshapefiles

The data should now be available via the API. <a href="{{ site.baseurl }}/docs/api/">Let's explore the API.</a>
