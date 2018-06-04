---
title: "Build Openlayers Maps using React from Zero"
categories:
  - React
tags:
  - Openlayers
---

{% include toc title="Build Openlayers Maps using React from Zero" icon="file-text" %}

## Steps

Run the following commands:

```
create-react-app openlayers-react-demo
cd openlayers-react-demo
npm install --save ol
```

Then Change your App.js to following: 
```
import React, { Component } from "react";

var ol = require("ol/ol.css");
var ol_Map = require("ol/map").default;
var ol_layer_Tile = require("ol/layer/tile").default;
var ol_source_OSM = require("ol/source/osm").default;
var ol_View = require("ol/view").default;

class App extends Component {
  constructor(props) {
    super(props);

    this.map = {};
  }

  componentDidMount() {
    this.map = new ol_Map({
      target: "map",
      layers: [
        new ol_layer_Tile({
          source: new ol_source_OSM()
        })
      ],
      view: new ol_View({
        center: [0, 0],
        zoom: 2
      })
    });
  }

  render() {
    return (
      <div className="App">
        <div id="map" className="map" />
      </div>
    );
  }
}

export default App;

```

Then run `npm start`, you should be able to see a openlayers map
