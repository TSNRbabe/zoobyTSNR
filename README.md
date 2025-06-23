<!doctype html>
<html lang="en">
    <head>
        <meta charset="utf-8">
        <meta http-equiv="X-UA-Compatible" content="IE=edge">
        <meta name="viewport" content="initial-scale=1,user-scalable=no,maximum-scale=1,width=device-width">
        <meta name="mobile-web-app-capable" content="yes">
        <meta name="apple-mobile-web-app-capable" content="yes">
        <link rel="stylesheet" href="css/leaflet.css">
        <link rel="stylesheet" href="css/L.Control.Layers.Tree.css">
        <link rel="stylesheet" href="css/qgis2web.css">
        <link rel="stylesheet" href="css/fontawesome-all.min.css">
        <link rel="stylesheet" href="css/leaflet-measure.css">
        <style>
        html, body, #map {
            width: 100%;
            height: 100%;
            padding: 0;
            margin: 0;
        }
        </style>

        <title>Зоогеографическая карта Иркутской области</title>
    </head>
    <body>
        <div id="map">
        </div>
        <script src="js/qgis2web_expressions.js"></script>
        <script src="js/leaflet.js"></script>
        <script src="js/L.Control.Layers.Tree.min.js"></script>
        <script src="js/multi-style-layer.js"></script>
        <script src="js/leaflet.rotatedMarker.js"></script>
        <script src="js/leaflet.pattern.js"></script>
        <script src="js/leaflet-hash.js"></script>
        <script src="js/Autolinker.min.js"></script>
        <script src="js/rbush.min.js"></script>
        <script src="js/labelgun.min.js"></script>
        <script src="js/labels.js"></script>
        <script src="js/leaflet-measure.js"></script>
        <script src="data/_1.js"></script>
        <script src="data/_2.js"></script>
        <script src="data/_3.js"></script>
        <script src="data/_4.js"></script>
        <script src="data/_5.js"></script>
        <script src="data/_6.js"></script>
        <script src="data/_7.js"></script>
        <script src="data/_8.js"></script>
        <script src="data/_9.js"></script>
        <script src="data/_10.js"></script>
        <script src="data/_11.js"></script>
        <script src="data/_12.js"></script>

<link rel="stylesheet" href="https://cdn.jsdelivr.net/gh/KomelT/Leaflet.TopoScale/dist/leaflet.toposcale.min.css" />
<script src="https://cdn.jsdelivr.net/gh/KomelT/Leaflet.TopoScale/dist/leaflet.toposcale.min.js" charset="utf-8"></script>

        <script>
        var highlightLayer;
        function highlightFeature(e) {
            highlightLayer = e.target;

            if (e.target.feature.geometry.type === 'LineString' || e.target.feature.geometry.type === 'MultiLineString') {
              highlightLayer.setStyle({
                color: '#ffff00',
              });
            } else {
              highlightLayer.setStyle({
                fillColor: '#ffff00',
                fillOpacity: 1
              });
            }
        }
        var map = L.map('map', {
            zoomControl:false, maxZoom:28, minZoom:1
        }).fitBounds([[43.15666179539437,73.004498915473],[65.71205325539603,152.86484075788698]]);
        var hash = new L.Hash(map);
        map.attributionControl.setPrefix('<a href="https://github.com/tomchadwin/qgis2web" target="_blank">qgis2web</a> &middot; <a href="https://leafletjs.com" title="A JS library for interactive maps">Leaflet</a> &middot; <a href="https://qgis.org">QGIS</a>');
        var autolinker = new Autolinker({truncate: {length: 30, location: 'smart'}});
        // remove popup's row if "visible-with-data"
        function removeEmptyRowsFromPopupContent(content, feature) {
         var tempDiv = document.createElement('div');
         tempDiv.innerHTML = content;
         var rows = tempDiv.querySelectorAll('tr');
         for (var i = 0; i < rows.length; i++) {
             var td = rows[i].querySelector('td.visible-with-data');
             var key = td ? td.id : '';
             if (td && td.classList.contains('visible-with-data') && feature.properties[key] == null) {
                 rows[i].parentNode.removeChild(rows[i]);
             }
         }
         return tempDiv.innerHTML;
        }
        // add class to format popup if it contains media
		function addClassToPopupIfMedia(content, popup) {
			var tempDiv = document.createElement('div');
			tempDiv.innerHTML = content;
			if (tempDiv.querySelector('td img')) {
				popup._contentNode.classList.add('media');
					// Delay to force the redraw
					setTimeout(function() {
						popup.update();
					}, 10);
			} else {
				popup._contentNode.classList.remove('media');
			}
		}
        var title = new L.Control({'position':'bottomright'});
        title.onAdd = function (map) {
            this._div = L.DomUtil.create('div', 'info');
            this.update();
            return this._div;
        };
        title.update = function () {
            this._div.innerHTML = '<h2>Зоогеографическая карта Иркутской области</h2>';
        };
        title.addTo(map);
        var zoomControl = L.control.zoom({
            position: 'topleft'
        }).addTo(map);
        var measureControl = new L.Control.Measure({
            position: 'topleft',
            primaryLengthUnit: 'meters',
            secondaryLengthUnit: 'kilometers',
            primaryAreaUnit: 'sqmeters',
            secondaryAreaUnit: 'hectares'
        });
        measureControl.addTo(map);
        document.getElementsByClassName('leaflet-control-measure-toggle')[0].innerHTML = '';
        document.getElementsByClassName('leaflet-control-measure-toggle')[0].className += ' fas fa-ruler';
        var bounds_group = new L.featureGroup([]);
        function setBounds() {
        }
        map.createPane('pane_OSMStandard_0');
        map.getPane('pane_OSMStandard_0').style.zIndex = 400;
        var layer_OSMStandard_0 = L.tileLayer('http://tile.openstreetmap.org/{z}/{x}/{y}.png', {
            pane: 'pane_OSMStandard_0',
            opacity: 0.7,
            attribution: '<a href="https://www.openstreetmap.org/copyright">© OpenStreetMap contributors, CC-BY-SA</a>',
            minZoom: 1,
            maxZoom: 28,
            minNativeZoom: 0,
            maxNativeZoom: 19
        });
        layer_OSMStandard_0;
        map.addLayer(layer_OSMStandard_0);
        function pop__1(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        function style__1_0() {
            return {
                pane: 'pane__1',
                opacity: 1,
                color: 'rgba(247,247,247,1.0)',
                dashArray: '',
                lineCap: 'butt',
                lineJoin: 'miter',
                weight: 1.0, 
                fill: true,
                fillOpacity: 1,
                fillColor: 'rgba(238,255,153,1.0)',
                interactive: true,
            }
        }
        map.createPane('pane__1');
        map.getPane('pane__1').style.zIndex = 401;
        map.getPane('pane__1').style['mix-blend-mode'] = 'normal';
        var layer__1 = new L.geoJson(json__1, {
            attribution: '',
            interactive: true,
            dataVar: 'json__1',
            layerName: 'layer__1',
            pane: 'pane__1',
            onEachFeature: pop__1,
            style: style__1_0,
        });
        bounds_group.addLayer(layer__1);
        map.addLayer(layer__1);
        function pop__2(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['fid'] !== null ? autolinker.link(String(feature.properties['fid']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NAME'] !== null ? autolinker.link(String(feature.properties['NAME']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NAME_EN'] !== null ? autolinker.link(String(feature.properties['NAME_EN']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['NAME_RU'] !== null ? autolinker.link(String(feature.properties['NAME_RU']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_LVL'] !== null ? autolinker.link(String(feature.properties['ADMIN_LVL']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['OSM_TYPE'] !== null ? autolinker.link(String(feature.properties['OSM_TYPE']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['OSM_ID'] !== null ? autolinker.link(String(feature.properties['OSM_ID']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L1D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L1D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L1'] !== null ? autolinker.link(String(feature.properties['ADMIN_L1']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L2D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L2D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L2'] !== null ? autolinker.link(String(feature.properties['ADMIN_L2']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L3D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L3D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L3'] !== null ? autolinker.link(String(feature.properties['ADMIN_L3']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L4D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L4D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L4'] !== null ? autolinker.link(String(feature.properties['ADMIN_L4']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L5D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L5D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L5'] !== null ? autolinker.link(String(feature.properties['ADMIN_L5']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L6D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L6D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L6'] !== null ? autolinker.link(String(feature.properties['ADMIN_L6']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L7D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L7D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L7'] !== null ? autolinker.link(String(feature.properties['ADMIN_L7']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L8D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L8D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L8'] !== null ? autolinker.link(String(feature.properties['ADMIN_L8']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L9D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L9D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L9'] !== null ? autolinker.link(String(feature.properties['ADMIN_L9']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L10D'] !== null ? autolinker.link(String(feature.properties['ADMIN_L10D']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['ADMIN_L10'] !== null ? autolinker.link(String(feature.properties['ADMIN_L10']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['oktmo'] !== null ? autolinker.link(String(feature.properties['oktmo']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['okato'] !== null ? autolinker.link(String(feature.properties['okato']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }
        function style__2_0(feature) {
            var context = {
                feature: feature,
                variables: {}
            };
            // Start of if blocks and style check logic
            if (exp__2rule0_eval_expression(context)) {
                  return {
                pane: 'pane__2',
                opacity: 1,
                color: 'rgba(243,255,15,1.0)',
                dashArray: '',
                lineCap: 'butt',
                lineJoin: 'miter',
                weight: 6.0, 
                fillOpacity: 0,
                interactive: true,
            };
                }
            else {
                return {fill: false, stroke: false};
            }
        }
        map.createPane('pane__2');
        map.getPane('pane__2').style.zIndex = 402;
        map.getPane('pane__2').style['mix-blend-mode'] = 'normal';
        var layer__2 = new L.geoJson(json__2, {
            attribution: '',
            interactive: true,
            dataVar: 'json__2',
            layerName: 'layer__2',
            pane: 'pane__2',
            onEachFeature: pop__2,
            style: style__2_0,
        });
        bounds_group.addLayer(layer__2);
        map.addLayer(layer__2);
        function pop__3(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        var pattern__3_0 = new L.StripePattern({
            weight: 0.3,
            spaceWeight: 2.0,
            color: '#c85300',
            opacity: 1.0,
            spaceOpacity: 0,
            angle: 315
        });
        pattern__3_0.addTo(map);
        function style__3_0() {
            return {
                pane: 'pane__3',
                stroke: false,
                fillOpacity: 1,
                fillPattern: pattern__3_0,
                interactive: true,
            }
        }
        function style__3_1() {
            return {
                pane: 'pane__3',
                opacity: 1,
                color: 'rgba(200,83,0,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 2.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane__3');
        map.getPane('pane__3').style.zIndex = 403;
        map.getPane('pane__3').style['mix-blend-mode'] = 'normal';
        var layer__3 = new L.geoJson.multiStyle(json__3, {
            attribution: '',
            interactive: true,
            dataVar: 'json__3',
            layerName: 'layer__3',
            pane: 'pane__3',
            onEachFeature: pop__3,
            styles: [style__3_0,style__3_1,]
        });
        bounds_group.addLayer(layer__3);
        map.addLayer(layer__3);
        function pop__4(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        var pattern__4_0 = new L.StripePattern({
            weight: 0.3,
            spaceWeight: 2.0,
            color: '#ff0101',
            opacity: 1.0,
            spaceOpacity: 0,
            angle: 225
        });
        pattern__4_0.addTo(map);
        function style__4_0() {
            return {
                pane: 'pane__4',
                stroke: false,
                fillOpacity: 1,
                fillPattern: pattern__4_0,
                interactive: true,
            }
        }
        function style__4_1() {
            return {
                pane: 'pane__4',
                opacity: 1,
                color: 'rgba(255,1,1,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 2.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane__4');
        map.getPane('pane__4').style.zIndex = 404;
        map.getPane('pane__4').style['mix-blend-mode'] = 'normal';
        var layer__4 = new L.geoJson.multiStyle(json__4, {
            attribution: '',
            interactive: true,
            dataVar: 'json__4',
            layerName: 'layer__4',
            pane: 'pane__4',
            onEachFeature: pop__4,
            styles: [style__4_0,style__4_1,]
        });
        bounds_group.addLayer(layer__4);
        map.addLayer(layer__4);
        function pop__5(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        var pattern__5_0 = new L.StripePattern({
            weight: 0.3,
            spaceWeight: 2.0,
            color: '#ff11fb',
            opacity: 1.0,
            spaceOpacity: 0,
            angle: 315
        });
        pattern__5_0.addTo(map);
        function style__5_0() {
            return {
                pane: 'pane__5',
                stroke: false,
                fillOpacity: 1,
                fillPattern: pattern__5_0,
                interactive: true,
            }
        }
        function style__5_1() {
            return {
                pane: 'pane__5',
                opacity: 1,
                color: 'rgba(255,17,251,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 2.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane__5');
        map.getPane('pane__5').style.zIndex = 405;
        map.getPane('pane__5').style['mix-blend-mode'] = 'normal';
        var layer__5 = new L.geoJson.multiStyle(json__5, {
            attribution: '',
            interactive: true,
            dataVar: 'json__5',
            layerName: 'layer__5',
            pane: 'pane__5',
            onEachFeature: pop__5,
            styles: [style__5_0,style__5_1,]
        });
        bounds_group.addLayer(layer__5);
        map.addLayer(layer__5);
        function pop__6(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        var pattern__6_0 = new L.StripePattern({
            weight: 0.3,
            spaceWeight: 2.0,
            color: '#4944a9',
            opacity: 1.0,
            spaceOpacity: 0,
            angle: 225
        });
        pattern__6_0.addTo(map);
        function style__6_0() {
            return {
                pane: 'pane__6',
                stroke: false,
                fillOpacity: 1,
                fillPattern: pattern__6_0,
                interactive: true,
            }
        }
        function style__6_1() {
            return {
                pane: 'pane__6',
                opacity: 1,
                color: 'rgba(73,68,169,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 2.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane__6');
        map.getPane('pane__6').style.zIndex = 406;
        map.getPane('pane__6').style['mix-blend-mode'] = 'normal';
        var layer__6 = new L.geoJson.multiStyle(json__6, {
            attribution: '',
            interactive: true,
            dataVar: 'json__6',
            layerName: 'layer__6',
            pane: 'pane__6',
            onEachFeature: pop__6,
            styles: [style__6_0,style__6_1,]
        });
        bounds_group.addLayer(layer__6);
        map.addLayer(layer__6);
        function pop__7(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        var pattern__7_0 = new L.StripePattern({
            weight: 0.3,
            spaceWeight: 2.0,
            color: '#a411ff',
            opacity: 1.0,
            spaceOpacity: 0,
            angle: 225
        });
        pattern__7_0.addTo(map);
        function style__7_0() {
            return {
                pane: 'pane__7',
                stroke: false,
                fillOpacity: 1,
                fillPattern: pattern__7_0,
                interactive: true,
            }
        }
        function style__7_1() {
            return {
                pane: 'pane__7',
                opacity: 1,
                color: 'rgba(164,17,255,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 2.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane__7');
        map.getPane('pane__7').style.zIndex = 407;
        map.getPane('pane__7').style['mix-blend-mode'] = 'normal';
        var layer__7 = new L.geoJson.multiStyle(json__7, {
            attribution: '',
            interactive: true,
            dataVar: 'json__7',
            layerName: 'layer__7',
            pane: 'pane__7',
            onEachFeature: pop__7,
            styles: [style__7_0,style__7_1,]
        });
        bounds_group.addLayer(layer__7);
        map.addLayer(layer__7);
        function pop__8(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        var pattern__8_0 = new L.StripePattern({
            weight: 0.3,
            spaceWeight: 2.0,
            color: '#0011fe',
            opacity: 1.0,
            spaceOpacity: 0,
            angle: 225
        });
        pattern__8_0.addTo(map);
        function style__8_0() {
            return {
                pane: 'pane__8',
                stroke: false,
                fillOpacity: 1,
                fillPattern: pattern__8_0,
                interactive: true,
            }
        }
        function style__8_1() {
            return {
                pane: 'pane__8',
                opacity: 1,
                color: 'rgba(0,17,254,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 2.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane__8');
        map.getPane('pane__8').style.zIndex = 408;
        map.getPane('pane__8').style['mix-blend-mode'] = 'normal';
        var layer__8 = new L.geoJson.multiStyle(json__8, {
            attribution: '',
            interactive: true,
            dataVar: 'json__8',
            layerName: 'layer__8',
            pane: 'pane__8',
            onEachFeature: pop__8,
            styles: [style__8_0,style__8_1,]
        });
        bounds_group.addLayer(layer__8);
        map.addLayer(layer__8);
        function pop__9(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        var pattern__9_0 = new L.StripePattern({
            weight: 0.3,
            spaceWeight: 2.0,
            color: '#f3ff0f',
            opacity: 1.0,
            spaceOpacity: 0,
            angle: 315
        });
        pattern__9_0.addTo(map);
        function style__9_0() {
            return {
                pane: 'pane__9',
                stroke: false,
                fillOpacity: 1,
                fillPattern: pattern__9_0,
                interactive: true,
            }
        }
        function style__9_1() {
            return {
                pane: 'pane__9',
                opacity: 1,
                color: 'rgba(243,255,15,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 2.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane__9');
        map.getPane('pane__9').style.zIndex = 409;
        map.getPane('pane__9').style['mix-blend-mode'] = 'normal';
        var layer__9 = new L.geoJson.multiStyle(json__9, {
            attribution: '',
            interactive: true,
            dataVar: 'json__9',
            layerName: 'layer__9',
            pane: 'pane__9',
            onEachFeature: pop__9,
            styles: [style__9_0,style__9_1,]
        });
        bounds_group.addLayer(layer__9);
        map.addLayer(layer__9);
        function pop__10(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['fid'] !== null ? autolinker.link(String(feature.properties['fid']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        var pattern__10_0 = new L.StripePattern({
            weight: 0.3,
            spaceWeight: 2.0,
            color: '#27f50c',
            opacity: 1.0,
            spaceOpacity: 0,
            angle: 225
        });
        pattern__10_0.addTo(map);
        function style__10_0() {
            return {
                pane: 'pane__10',
                stroke: false,
                fillOpacity: 1,
                fillPattern: pattern__10_0,
                interactive: true,
            }
        }
        function style__10_1() {
            return {
                pane: 'pane__10',
                opacity: 1,
                color: 'rgba(39,245,12,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 2.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane__10');
        map.getPane('pane__10').style.zIndex = 410;
        map.getPane('pane__10').style['mix-blend-mode'] = 'normal';
        var layer__10 = new L.geoJson.multiStyle(json__10, {
            attribution: '',
            interactive: true,
            dataVar: 'json__10',
            layerName: 'layer__10',
            pane: 'pane__10',
            onEachFeature: pop__10,
            styles: [style__10_0,style__10_1,]
        });
        bounds_group.addLayer(layer__10);
        map.addLayer(layer__10);
        function pop__11(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        var pattern__11_0 = new L.StripePattern({
            weight: 0.3,
            spaceWeight: 2.0,
            color: '#10e2fe',
            opacity: 1.0,
            spaceOpacity: 0,
            angle: 315
        });
        pattern__11_0.addTo(map);
        function style__11_0() {
            return {
                pane: 'pane__11',
                stroke: false,
                fillOpacity: 1,
                fillPattern: pattern__11_0,
                interactive: true,
            }
        }
        function style__11_1() {
            return {
                pane: 'pane__11',
                opacity: 1,
                color: 'rgba(16,226,254,1.0)',
                dashArray: '',
                lineCap: 'square',
                lineJoin: 'bevel',
                weight: 2.0,
                fillOpacity: 0,
                interactive: true,
            }
        }
        map.createPane('pane__11');
        map.getPane('pane__11').style.zIndex = 411;
        map.getPane('pane__11').style['mix-blend-mode'] = 'normal';
        var layer__11 = new L.geoJson.multiStyle(json__11, {
            attribution: '',
            interactive: true,
            dataVar: 'json__11',
            layerName: 'layer__11',
            pane: 'pane__11',
            onEachFeature: pop__11,
            styles: [style__11_0,style__11_1,]
        });
        bounds_group.addLayer(layer__11);
        map.addLayer(layer__11);

L.control
  .toposcale({
    position: "bottomleft",
    updateWhenIdle: true,
    thousand_separator: ".",
    scale_separator: ":",
  })
  .addTo(map);

var icon11 = L.icon({iconUrl: 'legend/_12_перепелятник1.png'});
var icon2 = L.icon({iconUrl: 'legend/_12_скопа2.png'});
var icon3 = L.icon({iconUrl: 'legend/_12_беркут3.png'});
var icon4 = L.icon({iconUrl: 'legend_12_балобан4.png'});
var icon5 = L.icon({iconUrl: 'legend/_12_сапсан5.png'});
var icon6 = L.icon({iconUrl: 'legend/_12_филин6.png'});
var icon7 = L.icon({iconUrl: 'legend/_12_зимородок7.png'});
var icon8 = L.icon({iconUrl: 'legend/_12_сорока8.png'});
var icon9 = L.icon({iconUrl: 'legend/_12_воронок9.png'});
var icon10 = L.icon({iconUrl: 'legend/_12_баклан10.png'});
var icon1 = L.icon({iconUrl: 'legend/_12_гусеобразные0.png'});

        function pop__12(feature, layer) {
            layer.on({
                mouseout: function(e) {
                    for (var i in e.target._eventParents) {
                        if (typeof e.target._eventParents[i].resetStyle === 'function') {
                            e.target._eventParents[i].resetStyle(e.target);
                        }
                    }
                },
                mouseover: highlightFeature,
            });
            var popupContent = '<table>\
                    <tr>\
                        <td colspan="2">' + (feature.properties['id'] !== null ? autolinker.link(String(feature.properties['id']).replace(/'/g, '\'').toLocaleString()) : '') + '</td>\
                    </tr>\
                </table>';
            var content = removeEmptyRowsFromPopupContent(popupContent, feature);
			layer.on('popupopen', function(e) {
				addClassToPopupIfMedia(content, e.popup);
			});
			layer.bindPopup(content, { maxHeight: 400 });
        }

        function style__12_0(feature) {
            switch(String(feature.properties['id'])) {
                case '1':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon1,
            }
                    break;
                case '2':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon2,
            }
                    break;
                case '3':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon3,
            }
                    break;
                case '4':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon4,
            }
                    break;
                case '5':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon5,
            }
                    break;
                case '6':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon6,
            }
                    break;
                case '7':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon7,
            }
                    break;
                case '8':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon8,
            }
                    break;
                case '9':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon9,
            }
                    break;
                case '10':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon10,
            }
                    break;
                case '11':
                    return {
                pane: 'pane__12',
                interactive: true,
icon: icon11,
            }
                    break;
            }
        }
        map.createPane('pane__12');
        map.getPane('pane__12').style.zIndex = 412;
        map.getPane('pane__12').style['mix-blend-mode'] = 'normal';
        var layer__12 = new L.geoJson(json__12, {
            attribution: '',
            interactive: true,
            dataVar: 'json__12',
            layerName: 'layer__12',
            pane: 'pane__12',
            onEachFeature: pop__12,
            pointToLayer: function (feature, latlng) {
                var context = {
                    feature: feature,
                    variables: {}
                };
                return L.marker(latlng, style__12_0(feature));
            },
        });
        bounds_group.addLayer(layer__12);
        map.addLayer(layer__12);
        var overlaysTree = [
            {label: 'гусеобразные<br /><table><tr><td style="text-align: center;"><img src="legend/_12_гусеобразные0.png" /></td><td>гусеобразные</td></tr><tr><td style="text-align: center;"><img src="legend/_12_перепелятник1.png" /></td><td>перепелятник</td></tr><tr><td style="text-align: center;"><img src="legend/_12_скопа2.png" /></td><td>скопа</td></tr><tr><td style="text-align: center;"><img src="legend/_12_беркут3.png" /></td><td>беркут</td></tr><tr><td style="text-align: center;"><img src="legend/_12_балобан4.png" /></td><td>балобан</td></tr><tr><td style="text-align: center;"><img src="legend/_12_сапсан5.png" /></td><td>сапсан</td></tr><tr><td style="text-align: center;"><img src="legend/_12_филин6.png" /></td><td>филин</td></tr><tr><td style="text-align: center;"><img src="legend/_12_зимородок7.png" /></td><td>зимородок</td></tr><tr><td style="text-align: center;"><img src="legend/_12_сорока8.png" /></td><td>сорока</td></tr><tr><td style="text-align: center;"><img src="legend/_12_воронок9.png" /></td><td>воронок</td></tr><tr><td style="text-align: center;"><img src="legend/_12_баклан10.png" /></td><td>баклан</td></tr></table>', layer: layer__12},
            {label: '<img src="legend/_11.png" /> соболь, ласка', layer: layer__11},
            {label: '<img src="legend/_10.png" /> медведь', layer: layer__10},
            {label: '<img src="legend/_9.png" /> выдра', layer: layer__9},
            {label: '<img src="legend/_8.png" /> ондатра ', layer: layer__8},
            {label: '<img src="legend/_7.png" /> колонок ', layer: layer__7},
            {label: '<img src="legend/_6.png" /> рысь, россомаха, горностай', layer: layer__6},
            {label: '<img src="legend/_5.png" /> лось', layer: layer__5},
            {label: '<img src="legend/_4.png" /> лиса', layer: layer__4},
            {label: '<img src="legend/_3.png" /> изюбрь', layer: layer__3},
            {label: 'Административные границы<br /><table><tr><td style="text-align: center;"><img src="legend/_2_субъектовфедерации0.png" /></td><td>субъектов федерации</td></tr></table>', layer: layer__2},
            {label: '<img src="legend/_1.png" /> белка,волк', layer: layer__1},
            {label: "OSM Standard", layer: layer_OSMStandard_0},]
        var lay = L.control.layers.tree(null, overlaysTree,{
            //namedToggle: true,
            //selectorBack: false,
            //closedSymbol: '&#8862; &#x1f5c0;',
            //openedSymbol: '&#8863; &#x1f5c1;',
            //collapseAll: 'Collapse all',
            //expandAll: 'Expand all',
            collapsed: false, 
        });
        lay.addTo(map);
		document.addEventListener("DOMContentLoaded", function() {
            // set new Layers List height which considers toggle icon
            function newLayersListHeight() {
                var layerScrollbarElement = document.querySelector('.leaflet-control-layers-scrollbar');
                if (layerScrollbarElement) {
                    var layersListElement = document.querySelector('.leaflet-control-layers-list');
                    var originalHeight = layersListElement.style.height 
                        || window.getComputedStyle(layersListElement).height;
                    var newHeight = parseFloat(originalHeight) - 50;
                    layersListElement.style.height = newHeight + 'px';
                }
            }
            var isLayersListExpanded = true;
            var controlLayersElement = document.querySelector('.leaflet-control-layers');
            var toggleLayerControl = document.querySelector('.leaflet-control-layers-toggle');
            // toggle Collapsed/Expanded and apply new Layers List height
            toggleLayerControl.addEventListener('click', function() {
                if (isLayersListExpanded) {
                    controlLayersElement.classList.remove('leaflet-control-layers-expanded');
                } else {
                    controlLayersElement.classList.add('leaflet-control-layers-expanded');
                }
                isLayersListExpanded = !isLayersListExpanded;
                newLayersListHeight()
            });	
			// apply new Layers List height if toggle layerstree
			if (controlLayersElement) {
				controlLayersElement.addEventListener('click', function(event) {
					var toggleLayerHeaderPointer = event.target.closest('.leaflet-layerstree-header-pointer span');
					if (toggleLayerHeaderPointer) {
						newLayersListHeight();
					}
				});
			}
            // Collapsed/Expanded at Start to apply new height
            setTimeout(function() {
                toggleLayerControl.click();
            }, 10);
            setTimeout(function() {
                toggleLayerControl.click();
            }, 10);
            // Collapsed touch/small screen
            var isSmallScreen = window.innerWidth < 650;
            if (isSmallScreen) {
                setTimeout(function() {
                    controlLayersElement.classList.remove('leaflet-control-layers-expanded');
                    isLayersListExpanded = !isLayersListExpanded;
                }, 500);
            }  
        });       
        setBounds();
        </script>
    </body>
</html>
