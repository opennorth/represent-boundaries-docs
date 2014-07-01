---
layout: inner-page
title: Manage your data
---

After running Represent Boundaries for a while, you may need to add new shapefiles, update a shapefile, or correct an error in a definition file. The `loadshapefiles` command has options to make data management easy. To see all options, run:

    python manage.py help loadshapefiles

If you **add a shapefile**, <a href="{{ site.baseurl }}/docs/import/">create a definition file</a> and run the `loadshapefiles` command, which will automatically skip all shapefiles that have already been loaded.

If you **update a shapefile**, remember to change the `last_updated` field in its definition file. When you run the `loadshapefiles` command, only the updated shapefile will be re-loaded.

If you **correct an error in a definition file**, run the `loadshapefiles` with the `--reload` option to force the re-load of the shapefile. To avoid re-loading all your shapefiles, add a `--data-dir` option pointing to the directory containing the corrected definition file:

    python manage.py loadshapefiles --reload --data-dir data/shapefiles/my-folder

That's everything! If you have questions or issues, [open an issue on GitHub](https://github.com/opennorth/represent-boundaries/issues?state=open) or [contact us](mailto:represent@opennorth.ca).