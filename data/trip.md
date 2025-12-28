---
layout: default
title: "trip"
style: main
---

## Cities I've been to
Let’s see how many cities I travel before my degree!

<div style="width: 100ex; height: 50ex;">
<div id="map" style="width: 90%; height: 100%; border-radius: 10px; margin-left: 10ex; margin-bottom: 5ex"></div>
</div>


<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css"/>
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<script>
  const map = L.map("map", {
    scrollWheelZoom: true,
    maxBounds: [[-90, -180],[90, 180]],
    maxBoundsViscosity: 1.0,
  }).setView([0, 0], 2.5);
  setTimeout(() => {map.invalidateSize();}, 200);

  L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
    attribution: "&copy; OpenStreetMap",
  }).addTo(map);

  fetch("/assets/trips.geojson")
    .then(res => res.json())
    .then(data => {
      const geoLayer = L.geoJSON(data, {
        pointToLayer: (feature, latlng) =>
          L.circleMarker(latlng, {
            radius: 1,
            fillOpacity: 0.8,
            color: feature.properties.color || "#333"
          }),
        onEachFeature: (feature, layer) => {
          layer.bindTooltip(
            `${feature.properties.place}<br>${feature.properties.why}`
            , {
            permanent: false,
            direction: "top",
            offset: [0, 0],
            opacity: 0.9
          });
        }
      }).addTo(map);

      map.fitBounds(geoLayer.getBounds(), { padding: [-10, -10] });
    });
</script>

<br>
<b>Went to school there</b>
<ul style="margin-top: -1.5ex; margin-left: 5ex">
  <li>Seoul, KR</li>
  <li>Austin, TX</li>
</ul>


<b>Flew there</b><br>
2024
<ul style="margin-top: -1.5ex; margin-left: 5ex">
  <li>Tokyo, JP</li>
  <li>San Fransisco, CA</li>
  <li>Osaka, JP</li>
</ul>
2025
<ul style="margin-top: -1.5ex; margin-left: 5ex">
  <li>Chicago, IL</li>
  <li>Jeju island, KR</li>
  <li>New York, NY</li>
  <li>Boston, MA</li>
  <li>Mansfield, CT</li>
</ul>


<b>Trained there</b><br>
2025
<ul style="margin-top: -1.5ex; margin-left: 5ex">
  <li>Daegu, KR</li>
</ul>

<b>Drove there</b><br>
2024
<ul style="margin-top: -1.5ex; margin-left: 5ex">
  <li>St. Louis, MO</li>
  <li>Corpus Christi, TX</li>
  <li>Fort Davis, TX</li>
</ul>
2025
<ul style="margin-top: -1.5ex; margin-left: 5ex">
  <li>St. Louis, MO</li>
  <li>Newark, DE</li>
  <li>Philladelphia, PA</li>
  <li>New Orleans, LA</li>
  <li>San Antonio, TX</li>
  <li>Dallas, TX</li>
</ul>