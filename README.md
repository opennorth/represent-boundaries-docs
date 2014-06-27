# represent.poplus.org

Uses [poplus-theme](https://github.com/mysociety/poplus-theme/).

Besides the following files, all files should be in sync with other *.poplus.org sites:

* `_includes/sidebar.html`
* `assets/sass/_represent-styles.scss`
* `assets/img/hero-a.jpg`
* `assets/img/hero-b.jpg`
* `css/global.css`
* `docs/`
* `_config.yml`
* `CNAME`
* `index.html`
* `README.md`

Build and preview the site:

```
sass --update assets/sass:css
jekyll serve --watch
```
