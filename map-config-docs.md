# Map Configuration Documentation

## Overview
This configuration file defines a complete web mapping application setup, including layer definitions, user interface components, and various tool configurations. The configuration is structured in JSON format with three main sections: `map`, `datacatalog`, and `tools`.

## Structure

### Map Settings
```json
"map": {
    "zoom": 6.5,
    "center": [5.375, 52.168],
    "pitch": 0
}
```
- `zoom`: Initial zoom level of the map
- `center`: Initial center coordinates [longitude, latitude]
- `pitch`: 3D viewing angle in degrees

### Data Catalog
The `datacatalog` section contains an array of layer groups and their sublayers. Each layer can be one of several types:

#### Layer Types
1. **WMS (Web Map Service)**
   - Uses standard WMS protocol
   - Requires URL with GetMap endpoint
   - Supports GetFeatureInfo for clickable information

2. **WMTS (Web Map Tile Service)**
   - Tiled map service
   - More efficient than WMS for base maps
   - Requires tile URL template

3. **Vector Tile**
   - MVT format vector data
   - Supports custom styling
   - More interactive than raster tiles

4. **GeoJSON**
   - Direct vector data
   - Supports complex styling
   - Interactive features

5. **TopoJSON**
   - Compressed vector format
   - Similar to GeoJSON but more efficient
   - Good for administrative boundaries

#### Layer Properties
Common properties for layers include:
- `id`: Unique identifier
- `type`: Layer type (wms, wmts, vectortile, etc.)
- `title`: Display name
- `layerInfo`: Technical configuration
  - `source`: Data source configuration
  - `paint`: Visual styling rules
  - `layout`: Layout properties
  - `metadata`: Additional layer metadata

### Tools Configuration
The `tools` section defines the available UI components and their settings:

```json
"tools": {
    "toolbar": {
        "opened": 1
    },
    // ... other tools
}
```

Each tool can have:
- `visible`: Whether the tool is shown (1 or 0)
- `order`: Display order in the interface
- `position`: UI position (e.g., "top-right", "bottom-left")

## Layer Group Structure
Layers are organized in groups:
```json
{
    "type": "group",
    "title": "Group Name",
    "sublayers": [
        // Layer definitions
    ]
}
```

## Common Patterns

### Attribution
Most layers should include attribution:
```json
"attribution": "&copy; Organization Name"
```

### Zoom Levels
Control layer visibility ranges:
```json
"minzoom": 5,
"maxzoom": 18
```

### Styling
Vector layers support detailed styling:
```json
"paint": {
    "fill-color": "#color",
    "line-width": 1,
    // etc.
}
```

## Best Practices

1. **Layer Organization**
   - Group related layers together
   - Use clear, descriptive titles
   - Order from most specific to most general

2. **Performance**
   - Use vector tiles for interactive data
   - Use WMTS instead of WMS for base maps
   - Set appropriate zoom level ranges

3. **Metadata**
   - Include attribution information
   - Document data sources
   - Provide legends where appropriate

4. **Tool Configuration**
   - Enable only necessary tools
   - Order tools logically
   - Position tools for optimal UX

## Examples

### Basic WMS Layer
```json
{
    "title": "Example WMS",
    "type": "wms",
    "layerInfo": {
        "id": "example_wms",
        "type": "raster",
        "source": {
            "type": "raster",
            "tiles": [
                "https://example.com/wms?bbox={bbox-epsg-3857}&format=image/png&service=WMS&version=1.1.1&request=GetMap&srs=EPSG:3857&width=256&height=256&layers=example"
            ]
        }
    }
}
```

### Vector Tile Layer
```json
{
    "title": "Example Vector Tiles",
    "type": "vectortile",
    "layerInfo": {
        "id": "example_vector",
        "type": "fill",
        "source": {
            "type": "vector",
            "tiles": [
                "https://example.com/tiles/{z}/{x}/{y}.mvt"
            ]
        },
        "source-layer": "layer_name",
        "paint": {
            "fill-color": "#ff0000",
            "fill-opacity": 0.5
        }
    }
}
```
