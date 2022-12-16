# Bay Trail map

## Getting started

First things first, you will need to insert a Mapbox access token on line 520 of index.html where it currently says `'INSERT YOUR KEY HERE'` You may start a dev server by running the following commands and navigating to [http://localhost:1337/](http://localhost:1337/).

```bash
npm install
npm start
```

The only external dependencies are Mapbox GL JS v2.11.0 and [Turf.js](https://turfjs.org/), specifically the [@turf/length](https://www.npmjs.com/package/@turf/length) module. For development convenience, all of Turf.js is included via [unpkg](https://unpkg.com/), but for production it is _highly_ recommended to use a bundler and include only the necessary [@turf/length](https://www.npmjs.com/package/@turf/length) module.

## Project structure

To make development as simple as possible and avoid dependence on a particular bundler, the full implementation is currently contained in a script tag in the `index.html`, along with the styles in `style.css`. The JavaScript can be trivially split up into multiple files. The implementation is currently achieved through custom mapbox-gl _controls_. These allow creating widgets (e.g. measurement, map controls, and a legend) which live entirely in the map element. Moving the map to a final destination should then be straightforward just as long as there are no unexpected interactions between the styles or mouse events.

`sf_baytrail_aug2022.zip` contains the original source data for paths. It has been converted to WGS84 GeoJSON in `sf_baytrail_aug2022.geojson`. The map currnetly uses the [rreusser/cl8opuxyd000014qgjao6pono](https://api.mapbox.com/styles/v1/rreusser/cl8opuxyd000014qgjao6pono.html?title=copy&access_token=pk.eyJ1IjoicnJldXNzZXIiLCJhIjoiY2tsNzNnN2xwMXJ3bTJxcWplaHptZmtmNiJ9.4jyhYK5B3nCMw2NTD761hg&zoomwheel=true&fresh=true#13.73/37.81132/-122.29152) style, which we should try to transfer to a more suitable long-term destination.

## To do list (incomplete)

- [ ] Map styles
  - [x] Update to mapbox-streets-v12
  - [x] Fix line width for paths with borders
    - This has been accomplished by splitting the lines into two layers: one for the line and one for the
      casing. It works, but it's annoying for maintainabilit. I wonder if
      [mapbox-gl-js#12208](https://github.com/mapbox/mapbox-gl-js/pull/12208) is something which could
      simplify this (It's maybe only exposed in mapbox-gl-native?)
  - [ ] Transfer [rreusser/cl8opuxyd000014qgjao6pono](https://api.mapbox.com/styles/v1/rreusser/cl8opuxyd000014qgjao6pono.html?title=copy&access_token=pk.eyJ1IjoicnJldXNzZXIiLCJhIjoiY2tsNzNnN2xwMXJ3bTJxcWplaHptZmtmNiJ9.4jyhYK5B3nCMw2NTD761hg&zoomwheel=true&fresh=true#13.73/37.81132/-122.29152) to an appropriate account
- [ ] Map interactions
  - [ ] Measurement tool
    - [x] Finalize paths by clicking last vertex
    - [ ] Add instructions to guide usage
  - [ ] Click legend items to hide/show layers
    - Right now this is done with filter expressions in the style spec. Due to the way lines and casings
      are split up, I think this is a bit of work to copy/paste the expressions into JavaScript and update
      them as needed.
- [ ] Data
  - [ ] Investigate addition of symbol layer for parking lots, restrooms, etc.

## Author

The project author has been Ricky Reussser (ricky.reusser@mapbox.com). Please feel free to contact me with questions about the current and future project direction.

