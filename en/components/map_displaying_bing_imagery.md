---
title: Map | Data Visualization Tools | Ignite UI for Angular | Bing Maps | Infragistics
_description: The Map allows you to display imagery from Bing Maps. View the demo and usage for more
_keywords: map, Ignite UI for Angular, infragistics
mentionedTypes: ['XamGeographicMap']
---

## Displaying Imagery from Bing Maps

The [`BingMapsMapImagery`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html) is geographic imagery mapping service provided by Microsoft® company. It provides 3 styles of geographic imagery tiles of the world. This geographic imagery service is accessible directly on the <a href="http://www.bing.com/maps" target="_blank">www.bing.com/maps</a> web site. The Ignite UI for Angular map component can display geographic imagery from Bing Maps in the map’s background content using the [`BingMapsMapImagery`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html) class.

### Demo

<div class="sample-container loading" style="height: 500px">
    <iframe id="geo-map-display-bing-imagery-iframe" src='{environment:demosBaseUrl}/maps/geo-map-display-bing-imagery' width="100%" height="100%" seamless frameBorder="0" onload="onXPlatSampleIframeContentLoaded(this);"></iframe>
</div>
<div>
    <button data-localize="stackblitz" disabled class="stackblitz-btn"   data-iframe-id="geo-map-display-bing-imagery-iframe" data-demos-base-url="{environment:demosBaseUrl}">View on StackBlitz
    </button>
</div>

<div class="divider--half"></div>

### Code Snippet

The following code snippet shows how to display geographic imagery from Bing Maps in [`IgxGeographicMapComponent`](/angular-apis/typescript/latest/classes/igxgeographicmapcomponent.html) using [`BingMapsMapImagery`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html).

### Properties

The following table summarized properties of the [`BingMapsMapImagery`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html) class:

| Property Name                                                                                              | Property Type          | Description                                                                                                                                                                                                                                                                                                                                                                                                             |
| ---------------------------------------------------------------------------------------------------------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [`apiKey`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html#apikey)                         | string                 | Represents the property for setting an API key required for the Bing Maps imagery service. You must obtain this key from the <a href="http://www.bingmapsportal.coms" target="_blank">www.bingmapsportal.com</a> website.                                                                                                                                                                                               |
| [`imageryStyle`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html#imagerystyle)             | `BingMapsImageryStyle` | Represents the property for setting the Bing Maps imagery tiles map style. This property can be set to the following `BingMapsImageryStyle` enumeration values: <ul><li> Aerial - Specifies the Aerial map style without road or labels overlay</li> <li> AerialWithLabels - Specifies the Aerial map style with road and labels overlay</li><li> Road - Specifies the Roads map style without Aerial overlay</li></ul> |
| [`bingImageryRestUri`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html#bingimageryresturi) | string                 | Represents the property for setting the Bing Imagery REST URI specifying where the TilePath and SubDomains will come from. This is an optional property, and if not specified it will use the default REST URI.                                                                                                                                                                                                         |
| [`cultureName`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html#culturename)               | string                 | Represents a property for setting the culture name for the tile source.                                                                                                                                                                                                                                                                                                                                                 |
| [`isDeferredLoad`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html#isdeferredload)         | boolean                | Represents the property that specifies whether or not the Bing Maps service should auto-initialized upon the assignment of valid property values.                                                                                                                                                                                                                                                                       |
| [`isInitialized`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html#isinitialized)           | boolean                | Represents the property that is set to True occurs when geographic imagery tiles from Bing Maps service have been initialized and they are ready for rendering in the map component.                                                                                                                                                                                                                                    |
| [`subDomains`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html#subdomains)                 | `SubDomainsCollection` | Represents an image collection of URI sub domains                                                                                                                                                                                                                                                                                                                                                                       |
| [`tilePath`](/angular-apis/typescript/latest/classes/bingmapsmapimagery.html#tilepath)                     | string                 | Represents a property that sets the map tile image URI, this is the actual location of the Bing Maps                                                                                                                                                                                                                                                                                                                    |