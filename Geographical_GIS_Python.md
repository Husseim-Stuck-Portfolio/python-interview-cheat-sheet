## 📦 Installation Guide

### Core Geospatial Stack

bash
# 1. Create a dedicated environment (recommended)
conda create -n geo_env python=3.11
conda activate geo_env

# 2. Install geopandas and its heavy dependencies first
conda install -c conda-forge geopandas

# 3. Install osmnx (handles OSM data + network analysis)
conda install -c conda-forge osmnx

# 4. Install folium for interactive maps
pip install folium

# 5. Install additional plugins
pip install folium-plugins

# 6. Install shapely (usually comes with geopandas, but explicit is safe)
pip install shapely

# 7. Install pandas (usually included, but ensure latest)
pip install pandas

# 8. Optional: Install jupyter for notebook workflows
pip install jupyter jupyterlab

# 9. Optional: Install contextily for basemap tiles
pip install contextily

# 10. Optional: Install matplotlib for static plotting
pip install matplotlib

# 11. Optional: Install mapclassify for choropleth classification
pip install mapclassify

# 12. Optional: Install pyproj for CRS transformations
pip install pyproj


### Alternative: Pure pip installation (if conda is unavailable)

bash
pip install geopandas osmnx folium shapely pandas numpy


### Verify Installation

python
import geopandas as gpd
import osmnx as ox
import folium
import shapely
import pandas as pd

print(" All core libraries imported successfully!")
print(f"GeoPandas: {gpd.__version__}")
print(f"OSMnx: {ox.__version__}")
print(f"Folium: {folium.__version__}")
print(f"Shapely: {shapely.__version__}")
print(f"Pandas: {pd.__version__}")




## 📋 Complete Function Reference

### Table Format: function | description | explanation | syntax example



## 1️⃣ OSMNX (osmnx as ox)



ox.geometries_from_place | Download OSM features by place name | Queries OpenStreetMap for geometries (points, lines, polygons) within a named place boundary. Returns a GeoDataFrame. Perfect for extracting buildings, roads, POIs by city name. | gdf = ox.geometries_from_place("Berlin, Germany", tags={"building": True}) |
ox.geometries_from_bbox | Download OSM features by bounding box | Queries OSM within a lat/lon bounding box (north, south, east, west). Faster than place queries for small areas. | gdf = ox.geometries_from_bbox(52.55, 52.50, 13.45, 13.35, tags={"building": True}) |
ox.geometries_from_polygon | Download OSM features within a custom polygon | Uses a Shapely polygon as the spatial filter. Ideal when you have an existing boundary geometry. | gdf = ox.geometries_from_polygon(polygon, tags={"building": True}) |
ox.geometries_from_address | Download OSM features around an address | Centers on a geocoded address with a buffer distance. Good for neighborhood-scale analysis. | gdf = ox.geometries_from_address("Alexanderplatz, Berlin", tags={"building": True}, dist=1000) |
ox.graph_from_place | Download street network by place name | Creates a NetworkX graph of drivable/walkable streets. Essential for routing and network analysis. | G = ox.graph_from_place("Berlin, Germany", network_type="drive") |
ox.graph_from_bbox | Download street network by bounding box | Creates a street network graph within lat/lon bounds. | G = ox.graph_from_bbox(52.55, 52.50, 13.45, 13.35, network_type="walk") |
ox.graph_from_polygon | Download street network within a polygon | Uses a Shapely polygon to define the network extent. | G = ox.graph_from_polygon(polygon, network_type="bike") |
ox.project_graph | Project a graph to a UTM CRS | Converts the graph from WGS84 (EPSG:4326) to the appropriate UTM zone for accurate distance calculations. | G_proj = ox.project_graph(G) |
ox.project_gdf | Project a GeoDataFrame to a UTM CRS | Projects geometries to a local coordinate reference system for metric calculations (area, distance). | gdf_proj = ox.project_gdf(gdf) |
ox.plot_graph | Visualize a street network graph | Creates a matplotlib plot of the network. Good for quick sanity checks. | fig, ax = ox.plot_graph(G, node_size=0, edge_linewidth=0.5) |
ox.simplify_graph | Simplify graph topology | Removes intermediate nodes on straight road segments to reduce graph complexity. | G_simple = ox.simplify_graph(G) |
ox.consolidate_intersections | Merge nearby intersections | Combines nodes within a tolerance distance into a single intersection node. | G_clean = ox.consolidate_intersections(G_proj, tolerance=10, rebuild_graph=True) |
ox.nearest_nodes | Find nearest graph nodes to points | Returns the closest network node(s) to given coordinates. Critical for routing origins/destinations. | orig_node = ox.nearest_nodes(G, X=13.405, Y=52.52) |
ox.shortest_path | Compute shortest path between nodes | Calculates the shortest path using Dijkstra's algorithm. Returns a list of node IDs. | route = ox.shortest_path(G, orig_node, dest_node, weight="length") |
ox.utils_graph.graph_from_gdfs | Build graph from node/edge GeoDataFrames | Converts separate node and edge GeoDataFrames back into a NetworkX graph. | G = ox.utils_graph.graph_from_gdfs(gdf_nodes, gdf_edges) |
ox.utils_graph.graph_to_gdfs | Convert graph to node/edge GeoDataFrames | Extracts node and edge data as separate GeoDataFrames for analysis. | gdf_nodes, gdf_edges = ox.utils_graph.graph_to_gdfs(G) |
ox.features_from_place | Alias for geometries_from_place | Newer API naming convention. Same functionality as geometries_from_place. | gdf = ox.features_from_place("Berlin", tags={"building": True}) |
ox.features_from_bbox | Alias for geometries_from_bbox | Newer API naming convention. Same functionality as geometries_from_bbox. | gdf = ox.features_from_bbox(north, south, east, west, tags={"amenity": True}) |
ox.settings | Configure OSMnx global settings | Adjusts caching, logging, timeout, and overpass API settings. | ox.settings.log_console = True; ox.settings.use_cache = True |
ox.config | Configure OSMnx behavior | Legacy configuration method. Use settings in newer versions. | ox.config(use_cache=True, log_console=True) |



## 2️⃣ GEOPANDAS (geopandas as gpd)



gpd.read_file | Read spatial data from file | Loads shapefiles, GeoJSON, GeoPackages, KML, and many other formats into a GeoDataFrame. | gdf = gpd.read_file("data/buildings.shp") |
gpd.read_file (URL) | Read spatial data from URL | Downloads and reads spatial data directly from a web URL. | gdf = gpd.read_file("https://example.com/data.geojson") |
gpd.GeoDataFrame | Create a GeoDataFrame from scratch | Constructs a GeoDataFrame from a DataFrame and a geometry column (Shapely objects). | gdf = gpd.GeoDataFrame(df, geometry=gdf.geometry, crs="EPSG:4326") |
gdf.to_file | Save GeoDataFrame to file | Exports to shapefile, GeoJSON, GeoPackage, or other formats. | gdf.to_file("output/buildings.geojson", driver="GeoJSON") |
gdf.to_crs | Reproject to a different CRS | Transforms coordinates from one Coordinate Reference System to another. Essential for accurate measurements. | gdf_proj = gdf.to_crs("EPSG:32633") |
gdf.set_crs | Assign a CRS without transforming | Sets the CRS metadata when it's missing. Does NOT reproject coordinates. | gdf = gdf.set_crs("EPSG:4326", allow_override=True) |
gdf.crs | Access the current CRS | Returns the Coordinate Reference System of the GeoDataFrame as a pyproj CRS object. | print(gdf.crs) |
gdf.buffer | Create a buffer around geometries | Generates a polygon buffer of specified distance around each geometry. Distance units depend on CRS. | gdf_buffered = gdf.buffer(distance=500) |
gdf.centroid | Calculate the centroid of each geometry | Computes the geometric center point of each polygon/line. Returns a GeoSeries of Points. | centroids = gdf.centroid |
gdf.area | Calculate polygon areas | Returns the area of each geometry in the CRS units. Must be in a projected CRS for meaningful results. | gdf["area_m2"] = gdf.area |
gdf.length | Calculate geometry lengths | Returns the length of each line or boundary length of polygons in CRS units. | gdf["length_m"] = gdf.length |
gdf.bounds | Get bounding box coordinates | Returns minx, miny, maxx, maxy for each geometry as a DataFrame. | bounds = gdf.bounds |
gdf.total_bounds | Get overall bounding box | Returns a single tuple (minx, miny, maxx, maxy) for the entire GeoDataFrame. | minx, miny, maxx, maxy = gdf.total_bounds |
gdf.envelope | Get the bounding box polygon | Creates a rectangular polygon representing each geometry's bounding box. | envelopes = gdf.envelope |
gdf.convex_hull | Create convex hull polygons | Generates the smallest convex polygon containing each geometry. | hulls = gdf.convex_hull |
gdf.dissolve | Dissolve geometries by attribute | Merges geometries that share the same value in a specified column. Like a spatial GROUP BY. | dissolved = gdf.dissolve(by="district", aggfunc="sum") |
gdf.overlay | Spatial overlay operation | Performs intersection, union, difference, or symmetric difference between two GeoDataFrames. | result = gdf1.overlay(gdf2, how="intersection") |
gdf.sjoin | Spatial join | Joins attributes from one GeoDataFrame to another based on spatial relationships (within, intersects, contains). | joined = gdf1.sjoin(gdf2, how="left", predicate="intersects") |
gdf.sjoin_nearest | Nearest spatial join | Joins each geometry to its nearest neighbor in another GeoDataFrame. | nearest = gdf1.sjoin_nearest(gdf2, how="left", max_distance=1000) |
gdf.clip | Clip geometries to a boundary | Cuts geometries to fit within a mask polygon. Removes parts outside the boundary. | clipped = gdf.clip(mask_polygon) |
gdf.intersects | Check spatial intersection | Returns a boolean Series indicating whether each geometry intersects with another geometry. | mask = gdf.intersects(berlin_boundary) |
gdf.within | Check if geometries are within another | Returns True for geometries completely inside another geometry. | mask = gdf.within(berlin_boundary) |
gdf.contains | Check if geometries contain another | Returns True for geometries that completely contain another geometry. | mask = gdf.contains(point) |
gdf.distance | Calculate distance to another geometry | Computes the minimum distance from each geometry to a target geometry or GeoSeries. | distances = gdf.distance(target_point) |
gdf.representative_point | Get a point guaranteed inside each polygon | Returns a point within each polygon (unlike centroid which may fall outside). | points = gdf.representative_point() |
gdf.explode | Explode multi-part geometries | Splits MultiPolygons/MultiLines into individual geometries, duplicating attributes. | exploded = gdf.explode(index_parts=True) |
gdf.plot | Create a static map plot | Generates a matplotlib map visualization with customizable colors, markers, and legends. | gdf.plot(column="height", cmap="viridis", legend=True, figsize=(10,10)) |
gdf.explore | Create an interactive map | Generates an interactive Folium map directly from a GeoDataFrame. Quick alternative to manual Folium. | gdf.explore(column="height", cmap="plasma", tiles="CartoDB positron") |
gpd.sjoin | Standalone spatial join function | Functional version of the GeoDataFrame.sjoin method. Same result, different syntax. | joined = gpd.sjoin(gdf1, gdf2, how="inner", predicate="within") |
gpd.clip | Standalone clip function | Functional version of GeoDataFrame.clip. Useful for pipeline-style code. | clipped = gpd.clip(gdf, mask) |
gpd.overlay | Standalone overlay function | Functional version of GeoDataFrame.overlay. Supports all overlay operations. | result = gpd.overlay(gdf1, gdf2, how="union") |
gpd.points_from_xy | Create Point geometries from coordinates | Converts x/y coordinate columns into Shapely Point objects for a geometry column. | geometry = gpd.points_from_xy(df.lon, df.lat) |
gpd.GeoSeries | Create a GeoSeries | A pandas Series with Shapely geometries. Can be used as a geometry column. | gs = gpd.GeoSeries([point1, point2, point3], crs="EPSG:4326") |
gdf.cx[] | Coordinate-based indexing | Selects geometries whose bounds intersect with the given coordinate slice. Fast spatial filtering. | subset = gdf.cx[13.3:13.5, 52.4:52.6] |
gdf.__geo_interface__ | Export as GeoJSON-like dict | Returns a GeoJSON FeatureCollection as a Python dictionary. Useful for serialization. | geojson_dict = gdf.__geo_interface__ |
gdf.from_features | Create GeoDataFrame from features | Builds a GeoDataFrame from a list of GeoJSON-like feature dictionaries. | gdf = gpd.GeoDataFrame.from_features(features, crs="EPSG:4326") |
gdf.to_json | Export to GeoJSON string | Converts the entire GeoDataFrame to a GeoJSON string representation. | geojson_str = gdf.to_json() |
gdf.to_wkb | Export geometries to WKB | Converts geometries to Well-Known Binary format for compact storage or database insertion. | gdf["wkb"] = gdf.geometry.to_wkb() |
gdf.from_wkb | Create geometries from WKB | Parses Well-Known Binary bytes back into Shapely geometries. | gdf["geometry"] = gpd.GeoSeries.from_wkb(gdf["wkb"]) |
gdf.to_wkt | Export geometries to WKT | Converts geometries to Well-Known Text format for human-readable storage. | gdf["wkt"] = gdf.geometry.to_wkt() |
gdf.from_wkt | Create geometries from WKT | Parses Well-Known Text strings back into Shapely geometries. | gdf["geometry"] = gpd.GeoSeries.from_wkt(gdf["wkt"]) |



## 3️⃣ SHAPELY

### Core Geometry (from shapely import wkb and general shapely)



shapely.Point | Create a Point geometry | Constructs a 0-dimensional geometry from x, y (and optional z) coordinates. | point = shapely.Point(13.405, 52.52) |
shapely.LineString | Create a LineString geometry | Constructs a 1-dimensional line from a sequence of coordinate tuples. | line = shapely.LineString([(13.4, 52.5), (13.5, 52.5), (13.5, 52.6)]) |
shapely.Polygon | Create a Polygon geometry | Constructs a 2-dimensional polygon from an exterior ring and optional interior rings (holes). | poly = shapely.Polygon([(0,0), (1,0), (1,1), (0,1), (0,0)]) |
shapely.MultiPoint | Create a MultiPoint geometry | A collection of Point geometries treated as a single object. | mp = shapely.MultiPoint([point1, point2, point3]) |
shapely.MultiLineString | Create a MultiLineString geometry | A collection of LineString geometries. | ml = shapely.MultiLineString([line1, line2]) |
shapely.MultiPolygon | Create a MultiPolygon geometry | A collection of Polygon geometries. Common in administrative boundaries. | mp = shapely.MultiPolygon([poly1, poly2]) |
shapely.GeometryCollection | Create a mixed geometry collection | A collection of different geometry types (points, lines, polygons together). | gc = shapely.GeometryCollection([point, line, poly]) |
shapely.wkb.loads | Load geometry from WKB bytes | Parses Well-Known Binary format into a Shapely geometry object. Critical for binary spatial data. | geom = shapely.wkb.loads(wkb_bytes) |
shapely.wkb.dumps | Dump geometry to WKB bytes | Converts a Shapely geometry to Well-Known Binary format for storage/transmission. | wkb_bytes = shapely.wkb.dumps(geom) |
shapely.wkt.loads | Load geometry from WKT string | Parses Well-Known Text format into a Shapely geometry. | geom = shapely.wkt.loads("POINT(13.405 52.52)") |
shapely.wkt.dumps | Dump geometry to WKT string | Converts a Shapely geometry to Well-Known Text format. | wkt_str = shapely.wkt.dumps(geom) |
geom.buffer | Create a buffer polygon | Generates a polygon of specified distance around the geometry. Distance in CRS units. | buffered = geom.buffer(100) |
geom.centroid | Get the centroid | Returns the geometric center as a Point. May lie outside non-convex polygons. | center = geom.centroid |
geom.representative_point | Get a point inside the geometry | Returns a Point guaranteed to be within the polygon (unlike centroid). | pt = geom.representative_point() |
geom.area | Calculate area | Returns the area of the geometry in square units of the CRS. | area = geom.area |
geom.length | Calculate length/perimeter | Returns the length of lines or the perimeter of polygons. | length = geom.length |
geom.bounds | Get bounding box | Returns a tuple (minx, miny, maxx, maxy). | minx, miny, maxx, maxy = geom.bounds |
geom.envelope | Get bounding box polygon | Returns the minimum bounding rectangle as a Polygon. | bbox = geom.envelope |
geom.convex_hull | Get convex hull | Returns the smallest convex Polygon containing the geometry. | hull = geom.convex_hull |
geom.concave_hull | Get concave hull (Shapely 2.0+) | Returns a tighter-fitting hull than convex_hull. Better shape approximation. | hull = geom.concave_hull(ratio=0.4) |
geom.simplify | Simplify geometry | Reduces the number of vertices using the Douglas-Peucker algorithm. Tolerance controls detail. | simple = geom.simplify(tolerance=0.001, preserve_topology=True) |
geom.intersection | Spatial intersection | Returns the geometric intersection of two geometries (overlap area). | overlap = geom1.intersection(geom2) |
geom.union | Spatial union | Returns the combined geometry of two geometries (merge without overlap). | merged = geom1.union(geom2) |
geom.difference | Spatial difference | Returns the part of geom1 that does not overlap with geom2. | diff = geom1.difference(geom2) |
geom.symmetric_difference | Symmetric difference | Returns the parts of both geometries that do NOT overlap (XOR operation). | sym_diff = geom1.symmetric_difference(geom2) |
geom.contains | Check containment | Returns True if the geometry completely contains another geometry. | if poly.contains(point): ... |
geom.within | Check if within | Returns True if the geometry is completely within another geometry. | if point.within(poly): ... |
geom.intersects | Check intersection | Returns True if geometries share any space (boundary or interior). | if geom1.intersects(geom2): ... |
geom.touches | Check touching | Returns True if geometries share only a boundary (no interior overlap). | if geom1.touches(geom2): ... |
geom.disjoint | Check disjoint | Returns True if geometries have no points in common. | if geom1.disjoint(geom2): ... |
geom.crosses | Check crossing | Returns True if geometries intersect but neither contains the other. | if line.crosses(poly): ... |
geom.overlaps | Check overlapping | Returns True if geometries share space but neither contains the other. | if poly1.overlaps(poly2): ... |
geom.equals | Check exact equality | Returns True if geometries are exactly the same (coordinate-wise). | if geom1.equals(geom2): ... |
geom.almost_equals | Check near-equality | Returns True if geometries are equal within a tolerance. Handles floating-point issues. | if geom1.almost_equals(geom2, decimal=6): ... |
geom.distance | Calculate distance | Returns the minimum distance between two geometries in CRS units. | dist = geom1.distance(geom2) |
geom.hausdorff_distance | Hausdorff distance | Measures how far two geometries deviate from each other (shape similarity). | hd = geom1.hausdorff_distance(geom2) |
geom.coords | Access coordinates | Returns a sequence of coordinate tuples for lines and polygons. | for x, y in line.coords: ... |
geom.exterior | Access exterior ring | Returns the exterior boundary LineString of a Polygon. | exterior = poly.exterior |
geom.interiors | Access interior rings | Returns a sequence of interior ring LineStrings (holes) in a Polygon. | for hole in poly.interiors: ... |
geom.is_valid | Check geometry validity | Returns True if the geometry is topologically valid (no self-intersections, etc.). | if not geom.is_valid: geom = geom.buffer(0) |
geom.is_empty | Check if empty | Returns True if the geometry contains no coordinates. | if geom.is_empty: ... |
geom.is_ring | Check if closed ring | Returns True if the LineString's start and end points are equal. | if line.is_ring: ... |
geom.is_simple | Check simplicity | Returns True if the geometry does not intersect itself. | if line.is_simple: ... |
geom.geom_type | Get geometry type | Returns the type as a string: "Point", "Polygon", "MultiPolygon", etc. | print(geom.geom_type) |
shapely.make_valid | Fix invalid geometry | Repairs self-intersecting or invalid geometries to make them valid. | valid_geom = shapely.make_valid(geom) |
shapely.unary_union | Union all geometries | Combines a collection of geometries into a single geometry, dissolving overlaps. | union = shapely.unary_union([geom1, geom2, geom3]) |
shapely.coverage_union | Optimized union for non-overlapping | Faster union when geometries are known not to overlap (like parcel data). | union = shapely.coverage_union([geom1, geom2]) |
shapely.dwithin | Check distance within threshold | Returns True if distance between geometries is within a tolerance (faster than distance()). | if shapely.dwithin(geom1, geom2, 100): ... |
shapely.force_2d | Remove Z coordinates | Strips any 3D (elevation) data from geometries to ensure 2D compatibility. | geom_2d = shapely.force_2d(geom) |
shapely.segmentize | Add vertices along edges | Inserts additional vertices at regular intervals along line/polygon edges. | densified = shapely.segmentize(geom, max_segment_length=10) |

### Geometry — from shapely.geometry import box



shapely.geometry.box | Create a rectangular polygon | Constructs an axis-aligned rectangle from minx, miny, maxx, maxy coordinates. Fast way to make bounding boxes. | bbox = shapely.geometry.box(13.3, 52.4, 13.5, 52.6) |
shapely.geometry.mapping | Convert to GeoJSON-like dict | Returns a dictionary representation compatible with the GeoJSON format. | geojson_dict = shapely.geometry.mapping(geom) |
shapely.geometry.shape | Convert from GeoJSON-like dict | Creates a Shapely geometry from a GeoJSON-like dictionary. | geom = shapely.geometry.shape(geojson_dict) |



## 4️⃣ PANDAS (pandas as pd)



pd.read_csv | Read CSV file into DataFrame | Loads comma-separated values into a structured DataFrame. Supports URLs, custom delimiters, and encoding. | df = pd.read_csv("data.csv", encoding="utf-8") |
pd.read_excel | Read Excel file into DataFrame | Loads .xls or .xlsx files. Can specify sheet names and skip rows. | df = pd.read_excel("data.xlsx", sheet_name="Sheet1") |
pd.read_json | Read JSON into DataFrame | Parses JSON strings or files into tabular format. | df = pd.read_json("data.json") |
pd.read_parquet | Read Parquet file | Loads columnar Parquet format (fast, compressed). Ideal for large datasets. | df = pd.read_parquet("data.parquet") |
pd.DataFrame | Create a DataFrame from scratch | Constructs a DataFrame from dictionaries, lists, arrays, or other data structures. | df = pd.DataFrame({"name": ["A", "B"], "value": [1, 2]}) |
df.to_csv | Save DataFrame to CSV | Exports DataFrame to a comma-separated text file. | df.to_csv("output.csv", index=False) |
df.to_excel | Save DataFrame to Excel | Exports to .xlsx format. Requires openpyxl engine. | df.to_excel("output.xlsx", index=False) |
df.to_json | Save DataFrame to JSON | Exports to JSON string or file. orient parameter controls structure. | df.to_json("output.json", orient="records") |
df.to_parquet | Save DataFrame to Parquet | Exports to compressed columnar format for efficient storage. | df.to_parquet("output.parquet") |
df.head | View first rows | Returns the first n rows (default 5) for quick inspection. | df.head(10) |
df.tail | View last rows | Returns the last n rows for quick inspection. | df.tail(5) |
df.info | DataFrame summary | Shows column names, non-null counts, and data types. Essential for data quality checks. | df.info() |
df.describe | Statistical summary | Computes count, mean, std, min, quartiles, max for numeric columns. | df.describe() |
df.shape | Get dimensions | Returns a tuple (rows, columns). | rows, cols = df.shape |
df.columns | Access column names | Returns an Index object of column names. | print(df.columns) |
df.dtypes | Check data types | Returns the data type of each column. | print(df.dtypes) |
df.index | Access row index | Returns the DataFrame's index (row labels). | print(df.index) |
df.values | Get underlying NumPy array | Returns the data as a 2D NumPy array. | arr = df.values |
df.copy | Create a deep copy | Makes an independent copy of the DataFrame to avoid modifying the original. | df_copy = df.copy() |
df.drop | Remove rows or columns | Deletes specified rows (axis=0) or columns (axis=1) from the DataFrame. | df = df.drop(columns=["col1", "col2"]) |
df.dropna | Remove missing values | Drops rows (or columns) containing NaN/None values. | df_clean = df.dropna(subset=["height"]) |
df.fillna | Fill missing values | Replaces NaN/None with a specified value, method, or calculated fill. | df["height"] = df["height"].fillna(0) |
df.isna | Detect missing values | Returns a boolean DataFrame indicating where values are missing. | missing = df.isna().sum() |
df.notna | Detect non-missing values | Returns the inverse of isna(). | valid = df.notna() |
df.astype | Cast data types | Converts columns to specified data types. | df["id"] = df["id"].astype(int) |
df.rename | Rename columns or index | Changes column names or index labels using a mapping dictionary. | df = df.rename(columns={"old": "new"}) |
df.sort_values | Sort by column values | Orders rows by values in one or more columns, ascending or descending. | df_sorted = df.sort_values("height", ascending=False) |
df.sort_index | Sort by index | Orders rows by the DataFrame index. | df = df.sort_index() |
df.reset_index | Reset the index | Converts the current index into a regular column and creates a new default index. | df = df.reset_index(drop=True) |
df.set_index | Set a column as index | Makes a specified column the DataFrame index for faster lookups. | df = df.set_index("building_id") |
df.loc | Label-based selection | Selects rows and columns by label/index name. Inclusive slicing. | subset = df.loc[0:10, ["name", "height"]] |
df.iloc | Position-based selection | Selects rows and columns by integer position (0-based). Exclusive end. | subset = df.iloc[0:5, 1:3] |
df.query | Query with expression | Filters rows using a string expression (SQL-like syntax). | tall = df.query("height > 50 and area > 1000") |
df.filter | Filter by column names | Selects columns by name patterns (like, regex) or items. | cols = df.filter(like="area") |
df.groupby | Group by column(s) | Splits data into groups, applies aggregation, and combines results. | stats = df.groupby("district")["height"].mean() |
df.agg | Aggregate with multiple functions | Applies one or more aggregation functions to columns. | stats = df.agg({"height": ["mean", "max"], "area": "sum"}) |
df.merge | Merge DataFrames | SQL-style join on common columns or indices. Supports inner, left, right, outer joins. | merged = df1.merge(df2, on="id", how="left") |
df.join | Join on index | Joins DataFrames on their indices (faster than merge for index-aligned data). | joined = df1.join(df2, how="outer") |
df.concat | Concatenate DataFrames | Stacks DataFrames vertically (axis=0) or horizontally (axis=1). | combined = pd.concat([df1, df2], axis=0) |
df.pivot | Reshape data (pivot) | Transforms long-format data to wide format using index, columns, and values. | pivot = df.pivot(index="date", columns="metric", values="value") |
df.pivot_table | Pivot with aggregation | Creates a pivot table with aggregation functions (like Excel). | pt = df.pivot_table(values="height", index="district", aggfunc="mean") |
df.melt | Unpivot DataFrame | Converts wide format to long format (inverse of pivot). | long = df.melt(id_vars=["id"], value_vars=["height", "area"]) |
df.apply | Apply function element-wise or row-wise | Applies a custom function to each element (axis=0) or row (axis=1). | df["new"] = df["height"].apply(lambda x: x * 2) |
df.map | Apply function element-wise (Series) | Applies a function to each element of a Series. | df["height"] = df["height"].map(lambda x: round(x, 2)) |
df.applymap | Apply function element-wise (DataFrame) | Applies a function to every element of the DataFrame. | df = df.applymap(lambda x: x.upper() if isinstance(x, str) else x) |
df.where | Replace where condition is False | Keeps values where condition is True, replaces others with a specified value. | df["flag"] = df["height"].where(df["height"] > 30, "low") |
df.mask | Replace where condition is True | Inverse of where(). Replaces values where condition is True. | df["flag"] = df["height"].mask(df["height"] > 30, "high") |
df.clip | Clip values to a range | Limits values to a minimum and maximum bound. | df["height"] = df["height"].clip(lower=0, upper=300) |
df.round | Round numeric values | Rounds floating-point numbers to specified decimal places. | df = df.round(2) |
df.nunique | Count unique values | Returns the number of unique values in each column. | unique_counts = df.nunique() |
df.unique | Get unique values (Series) | Returns an array of unique values from a Series. | types = df["building_type"].unique() |
df.value_counts | Count value frequencies | Returns counts of unique values, sorted descending. | counts = df["district"].value_counts() |
df.corr | Correlation matrix | Computes pairwise correlation of numeric columns. | corr = df[["height", "area", "floors"]].corr() |
df.cov | Covariance matrix | Computes pairwise covariance of numeric columns. | cov = df[["height", "area"]].cov() |
df.memory_usage | Check memory usage | Returns the memory footprint of each column in bytes. | print(df.memory_usage(deep=True)) |
pd.cut | Bin continuous data | Segments data into discrete intervals (bins). | df["height_bin"] = pd.cut(df["height"], bins=[0, 10, 30, 100, 300]) |
pd.qcut | Quantile-based binning | Segments data into bins with equal numbers of observations. | df["height_q"] = pd.qcut(df["height"], q=4, labels=["Q1", "Q2", "Q3", "Q4"]) |
pd.to_datetime | Convert to datetime | Parses strings or numbers into pandas datetime objects. | df["date"] = pd.to_datetime(df["date_str"]) |
pd.to_numeric | Convert to numeric | Converts strings to numeric types, with error handling. | df["value"] = pd.to_numeric(df["value"], errors="coerce") |
pd.get_dummies | One-hot encoding | Converts categorical variables into binary indicator columns. | dummies = pd.get_dummies(df["type"], prefix="type") |
pd.Series | Create a Series | A one-dimensional labeled array, the building block of DataFrames. | s = pd.Series([1, 2, 3], index=["a", "b", "c"]) |
pd.date_range | Generate date ranges | Creates a sequence of datetime objects for time series analysis. | dates = pd.date_range("2024-01-01", periods=365, freq="D") |
pd.read_sql | Read from SQL database | Executes a SQL query and loads results into a DataFrame. | df = pd.read_sql("SELECT * FROM buildings", conn) |
df.to_sql | Write to SQL database | Exports DataFrame to a SQL database table. | df.to_sql("buildings", conn, if_exists="replace") |
pd.read_html | Read HTML tables | Extracts tables from HTML strings or URLs into DataFrames. | dfs = pd.read_html("https://example.com/table.html") |
pd.json_normalize | Flatten nested JSON | Converts nested JSON/dicts into a flat DataFrame. | df = pd.json_normalize(data, record_path="buildings") |
pd.merge_asof | Merge on nearest key | Merges on nearest key rather than exact match (time series friendly). | merged = pd.merge_asof(df1, df2, on="timestamp") |
pd.IntervalIndex | Create interval index | Defines intervals for binning and categorization. | idx = pd.IntervalIndex.from_breaks([0, 10, 20, 30]) |
pd.MultiIndex | Create hierarchical index | Enables multi-level row/column indexing for complex data structures. | idx = pd.MultiIndex.from_tuples([("A", 1), ("A", 2), ("B", 1)]) |
df.xs | Cross-section selection | Selects data at a particular level of a MultiIndex. | subset = df.xs("Berlin", level="city") |
df.stack | Stack columns to rows | Pivots column labels into row labels (long format). | stacked = df.stack() |
df.unstack | Unstack rows to columns | Pivots row labels into column labels (wide format). | unstacked = df.unstack() |
df.explode | Explode list-like columns | Transforms each element of a list-like column into its own row. | df = df.explode("coordinates") |
df.sample | Random sampling | Returns a random sample of rows. Useful for testing on large datasets. | sample = df.sample(n=1000, random_state=42) |
df.nlargest | Top N by column | Returns the n rows with the largest values in a specified column. | tallest = df.nlargest(10, "height") |
df.nsmallest | Bottom N by column | Returns the n rows with the smallest values in a specified column. | shortest = df.nsmallest(10, "height") |
df.between | Check range membership (Series) | Returns boolean Series indicating values within a range. | mask = df["height"].between(10, 50) |
df.isin | Check membership in a set | Returns boolean indicating whether each element is in a given set. | mask = df["type"].isin(["residential", "commercial"]) |
pd.options.display | Configure display options | Sets global display settings for DataFrame output formatting. | pd.options.display.max_rows = 100 |
pd.set_option | Set pandas options | Configures display, computation, and mode options. | pd.set_option("display.float_format", "{:.2f}".format) |



## 5️⃣ FOLIUM



folium.Map | Create a base map | Initializes an interactive Leaflet map centered on coordinates with zoom level and tile choice. | m = folium.Map(location=[52.52, 13.405], zoom_start=12, tiles="CartoDB positron") |
folium.TileLayer | Add a tile layer | Adds alternative basemap tiles (OpenStreetMap, Stamen, CartoDB, etc.) to the map. | folium.TileLayer("Stamen Terrain", name="Terrain").add_to(m) |
folium.GeoJson | Add GeoJSON data | Displays GeoJSON features on the map with styling options. | folium.GeoJson(gdf, name="Buildings").add_to(m) |
folium.GeoJson (styled) | Add styled GeoJSON | Displays GeoJSON with custom colors, popups, and tooltips based on data attributes. | folium.GeoJson(gdf, style_function=lambda x: {"fillColor": "red"}).add_to(m) |
folium.Choropleth | Create a choropleth map | Colors polygons based on a numerical attribute using a color scale. | folium.Choropleth(geo_data=gdf, data=gdf, columns=["id", "height"], key_on="feature.properties.id").add_to(m) |
folium.CircleMarker | Add circle markers | Draws circles at specified locations with radius based on a value. Good for point data. | folium.CircleMarker([52.52, 13.405], radius=10, color="red").add_to(m) |
folium.Marker | Add a pin marker | Places a standard Leaflet marker at a location with optional popup text. | folium.Marker([52.52, 13.405], popup="Berlin Center").add_to(m) |
folium.Circle | Add a circle overlay | Draws a circle with a fixed radius in meters (unlike CircleMarker which is in pixels). | folium.Circle([52.52, 13.405], radius=500, color="blue").add_to(m) |
folium.Polygon | Add a polygon | Draws a custom polygon from a list of coordinate tuples. | folium.Polygon(locations=[[52.5,13.3],[52.6,13.3],[52.6,13.5]], color="green").add_to(m) |
folium.PolyLine | Add a polyline | Draws a connected line from a sequence of coordinates. | folium.PolyLine(locations=coords, color="blue", weight=3).add_to(m) |
folium.Rectangle | Add a rectangle | Draws a rectangle from bounds (two corner coordinates). | folium.Rectangle(bounds=[[52.5,13.3],[52.6,13.5]], color="red").add_to(m) |
folium.LayerControl | Add layer toggle control | Creates a control panel to show/hide different map layers. | folium.LayerControl().add_to(m) |
folium.FitBounds | Auto-fit map to bounds | Adjusts the map view to fit specified bounding coordinates. | m.fit_bounds([[52.5, 13.3], [52.6, 13.5]]) |
folium.LatLngPopup | Show coordinates on click | Displays lat/lon coordinates when clicking anywhere on the map. | m.add_child(folium.LatLngPopup()) |
folium.plugins.HeatMap | Create a heatmap | Visualizes point density as a color gradient. Requires a list of [lat, lon, weight] or [lat, lon]. | HeatMap(data=[[52.52,13.405],[52.53,13.41]]).add_to(m) |
folium.plugins.MarkerCluster | Cluster markers | Groups nearby markers into clusters that expand on zoom. Essential for large point datasets. | mc = MarkerCluster(); mc.add_child(folium.Marker([52.52,13.405])); m.add_child(mc) |
folium.plugins.FastMarkerCluster | Optimized marker clustering | Faster version of MarkerCluster for very large datasets (10k+ points). | FastMarkerCluster(data=coords).add_to(m) |
folium.plugins.GroupedLayerControl | Grouped layer toggles | Organizes layers into named groups in the layer control panel. Perfect for comparing datasets. | GroupedLayerControl(groups={"OSM": [layer1], "GBA": [layer2]}).add_to(m) |
folium.plugins.Draw | Enable drawing tools | Adds drawing tools (polygons, lines, markers) to the map for user interaction. | Draw(export=True).add_to(m) |
folium.plugins.Fullscreen | Add fullscreen button | Adds a button to toggle the map to fullscreen mode. | Fullscreen().add_to(m) |
folium.plugins.MousePosition | Show mouse coordinates | Displays the current lat/lon under the mouse cursor. | MousePosition().add_to(m) |
folium.plugins.MeasureControl | Add distance measurement tool | Allows users to measure distances and areas on the map interactively. | MeasureControl().add_to(m) |
folium.plugins.TimestampedGeoJson | Time-animated GeoJSON | Animates GeoJSON features over time. Each feature needs a "times" property. | TimestampedGeoJson(geojson_data, period="PT1H").add_to(m) |
folium.plugins.AntPath | Animated path line | Draws an animated dashed line along a path (great for routes). | AntPath(locations=coords).add_to(m) |
folium.plugins.DualMap | Side-by-side comparison | Creates two linked maps for before/after or dataset comparison. | m = DualMap(location=[52.52, 13.405], zoom_start=12) |
folium.plugins.SideBySideLayers | Swipe comparison | Adds a draggable divider to compare two layers side-by-side. | SideBySideLayers(layer1, layer2).add_to(m) |
folium.plugins.Geocoder | Add search box | Adds a location search box powered by Nominatim geocoding. | Geocoder().add_to(m) |
folium.plugins.LocateControl | Add "find my location" button | Uses browser geolocation to center the map on the user's current position. | LocateControl().add_to(m) |
folium.plugins.Search | Search within GeoJSON | Adds a search box to find features within a GeoJSON layer by property. | Search(layer=geojson, search_label="name").add_to(m) |
folium.Popup | Create a popup object | Defines HTML content for popups that appear on marker/polygon clicks. | popup = folium.Popup("<b>Building</b><br>Height: 50m", max_width=300) |
folium.Tooltip | Create a tooltip object | Defines text that appears on hover over a feature. | tooltip = folium.Tooltip("Click for details") |
folium.Icon | Create a custom icon | Defines marker icons with color, symbol, and prefix (FontAwesome or Glyphicon). | icon = folium.Icon(color="red", icon="building", prefix="fa") |
folium.CustomIcon | Use a custom image icon | Uses any image file as a marker icon. | icon = folium.CustomIcon("icon.png", icon_size=(30,30)) |
folium.DivIcon | HTML-based icon | Creates a marker using HTML/CSS content instead of an image. | icon = folium.DivIcon(html='<div style="color:red">★</div>') |
folium.map.FeatureGroup | Group map features | Creates a named group of layers that can be toggled together. | fg = folium.FeatureGroup(name="OSM Buildings").add_to(m) |
folium.map.Marker | Alternative marker syntax | Lower-level marker creation for advanced customization. | folium.map.Marker([52.52, 13.405], icon=icon).add_to(m) |
folium.map.Layer | Base layer class | Abstract base class for creating custom layer types. | class CustomLayer(folium.map.Layer): ... |
folium.Element | Create HTML element | Base class for adding arbitrary HTML to the map. | el = folium.Element("<script>...</script>") |
folium.JavascriptLink | Add external JS | Includes an external JavaScript file in the map HTML. | folium.JavascriptLink("https://.../script.js").add_to(m) |
folium.CssLink | Add external CSS | Includes an external CSS file in the map HTML. | folium.CssLink("https://.../style.css").add_to(m) |
folium.Figure | Create a figure container | Wraps the map in an HTML figure element with width/height control. | fig = folium.Figure(width=800, height=600); fig.add_child(m) |
folium.BrancaColormap | Create color scales | Generates color gradients for choropleth maps from the branca library. | from branca.colormap import linear; cmap = linear.YlOrRd_09 |
folium.map.MacroElement | Create macro elements | Base class for elements that need JavaScript initialization. | class MyPlugin(MacroElement): ... |
folium.map.Template | Jinja2 template | Defines HTML/JS templates for custom map components. | template = Template("""<div>{{ name }}</div>""") |
m.save | Save map to HTML file | Exports the interactive map as a standalone HTML file that opens in any browser. | m.save("berlin_map.html") |
m._repr_html_ | Get HTML representation | Returns the HTML string of the map (useful for Jupyter notebooks). | html = m._repr_html_() |
m.add_child | Add element to map | Adds any Folium element (layers, controls, plugins) to the map object. | m.add_child(folium.LatLngPopup()) |
m.add_to | Add map to figure | Adds the map to a Folium Figure container. | m.add_to(fig) |



## 6️⃣ URLLIB.REQUEST



urllib.request.urlopen | Open a URL | Opens a URL and returns a file-like object for reading. Handles HTTP/HTTPS/FTP. | response = urllib.request.urlopen("https://example.com/data.geojson") |
urllib.request.urlretrieve | Download file from URL | Downloads a file from a URL and saves it to a local path. Returns (filename, headers). | urllib.request.urlretrieve(url, "local_file.geojson") |
urllib.request.Request | Create a request object | Builds a request with custom headers, method, and data for more control. | req = urllib.request.Request(url, headers={"User-Agent": "MyApp"}) |
urllib.request.urlopen (with Request) | Open custom request | Sends a custom Request object instead of a raw URL string. | response = urllib.request.urlopen(req) |
urllib.request.build_opener | Build custom URL opener | Creates an opener with custom handlers (proxy, authentication, cookies). | opener = urllib.request.build_opener(urllib.request.ProxyHandler({"http": "proxy:8080"})) |
urllib.request.install_opener | Install custom opener | Sets a custom opener as the default for all subsequent urlopen calls. | urllib.request.install_opener(opener) |
urllib.request.HTTPHandler | HTTP handler | Handles HTTP protocol details. Used with build_opener for customization. | handler = urllib.request.HTTPHandler(debuglevel=1) |
urllib.request.HTTPSHandler | HTTPS handler | Handles HTTPS connections with SSL/TLS. Can specify SSL context. | handler = urllib.request.HTTPSHandler(context=ssl_context) |
urllib.request.ProxyHandler | Proxy handler | Routes requests through a proxy server. | proxy = urllib.request.ProxyHandler({"http": "http://proxy:8080"}) |
urllib.request.HTTPBasicAuthHandler | Basic authentication | Handles HTTP Basic Auth (username/password). | auth = urllib.request.HTTPBasicAuthHandler(password_mgr) |
urllib.request.HTTPPasswordMgr | Password manager | Stores authentication credentials for different realms/URLs. | pm = urllib.request.HTTPPasswordMgrWithDefaultRealm() |
urllib.request.add_password | Add credentials | Adds username/password for a specific URL realm to the password manager. | pm.add_password(None, url, "user", "pass") |
urllib.error.HTTPError | Handle HTTP errors | Exception raised for HTTP errors (404, 500, etc.). Catch for robust code. | except urllib.error.HTTPError as e: print(e.code) |
urllib.error.URLError | Handle URL errors | Exception raised for network-level errors (DNS, connection refused). | except urllib.error.URLError as e: print(e.reason) |
urllib.parse.urlencode | Encode query parameters | Converts a dictionary into a URL-encoded query string. | params = urllib.parse.urlencode({"key": "value", "format": "json"}) |
urllib.parse.urlparse | Parse URL components | Breaks a URL into scheme, netloc, path, params, query, fragment. | parsed = urllib.parse.urlparse("https://example.com/path?key=value") |
urllib.parse.urljoin | Join base URL with relative | Resolves a relative URL against a base URL to get an absolute URL. | full = urllib.parse.urljoin("https://example.com/", "data/file.geojson") |
urllib.parse.quote | URL-encode a string | Encodes special characters in a string for safe use in URLs. | safe = urllib.parse.quote("Berlin Mitte") |
urllib.parse.unquote | URL-decode a string | Reverses URL encoding back to the original string. | original = urllib.parse.unquote("Berlin%20Mitte") |
urllib.parse.quote_plus | URL-encode with plus for spaces | Like quote() but replaces spaces with '+' (form encoding standard). | safe = urllib.parse.quote_plus("Berlin Mitte") |
response.read | Read response content | Reads the entire response body as bytes. | data = response.read() |
response.readline | Read one line | Reads a single line from the response (useful for streaming). | line = response.readline() |
response.readlines | Read all lines | Returns a list of lines from the response. | lines = response.readlines() |
response.getcode | Get HTTP status code | Returns the numeric HTTP status (200, 404, etc.). | status = response.getcode() |
response.getheaders | Get response headers | Returns a list of (header_name, header_value) tuples. | headers = response.getheaders() |
response.getheader | Get specific header | Returns the value of a specific response header. | ctype = response.getheader("Content-Type") |
response.info | Get header info object | Returns an email.message.Message-like object with all headers. | info = response.info() |
response.url | Get final URL | Returns the actual URL after any redirects. | final_url = response.url |
response.status | Get status code (alias) | Same as getcode(). Returns HTTP status as integer. | if response.status == 200: ... |
response.reason | Get status reason | Returns the textual reason for the HTTP status ("OK", "Not Found"). | print(response.reason) |
response.length | Get content length | Returns the Content-Length header value if available. | size = response.length |
response.closed | Check if closed | Returns True if the response has been closed. | if not response.closed: response.close() |
response.__enter__ | Context manager entry | Enables with statement for automatic resource cleanup. | with urllib.request.urlopen(url) as r: data = r.read() |
response.__exit__ | Context manager exit | Closes the response automatically when exiting a with block. | with urllib.request.urlopen(url) as r: ... |
urllib.request.pathname2url | Convert path to URL | Converts a local file path to a URL-safe path string. | url_path = urllib.request.pathname2url("/path/to/file") |
urllib.request.url2pathname | Convert URL to path | Reverses pathname2url() for local file access. | path = urllib.request.url2pathname("file:///path/to/file") |



## 7️⃣ JSON



json.load | Parse JSON from file object | Reads a file-like object (opened in text mode) and converts JSON to Python objects. | with open("data.json") as f: data = json.load(f) |
json.loads | Parse JSON from string | Converts a JSON-formatted string into Python dictionaries, lists, etc. | data = json.loads('{"name": "Berlin", "pop": 3.6}') |
json.dump | Write JSON to file | Serializes a Python object to a file in JSON format. | with open("output.json", "w") as f: json.dump(data, f) |
json.dumps | Convert object to JSON string | Serializes a Python object to a JSON-formatted string. | json_str = json.dumps({"city": "Berlin"}, indent=2) |
json.JSONEncoder | Custom JSON encoder | Subclass to handle non-serializable types (datetime, custom objects). | class DateEncoder(json.JSONEncoder): def default(self, obj): ... |
json.JSONDecoder | Custom JSON decoder | Subclass to customize how JSON is parsed into Python objects. | class MyDecoder(json.JSONDecoder): def decode(self, s): ... |
json.loads (with object_hook) | Hook for dict parsing | Calls a function for every JSON object decoded (useful for type conversion). | data = json.loads(s, object_hook=lambda d: SimpleNamespace(**d)) |
json.loads (with object_pairs_hook) | Hook for key-value pairs | Calls a function with ordered pairs instead of a dict (preserves duplicates). | data = json.loads(s, object_pairs_hook=OrderedDict) |
json.dump (with default) | Handle non-serializable | Specifies a fallback function for types JSON can't serialize natively. | json.dump(data, f, default=str) |
json.dump (with indent) | Pretty-print JSON | Adds whitespace indentation for human-readable output. | json.dump(data, f, indent=4) |
json.dump (with sort_keys) | Sort keys alphabetically | Orders dictionary keys alphabetically in the output. | json.dump(data, f, sort_keys=True) |
json.dump (with ensure_ascii) | Control ASCII encoding | When False, outputs Unicode characters directly instead of escapes. | json.dump(data, f, ensure_ascii=False) |
json.dump (with separators) | Compact separators | Uses minimal separators for compact output (no spaces after commas/colons). | json.dump(data, f, separators=(",", ":")) |
json.load (with cls) | Custom decoder class | Uses a custom JSONDecoder subclass for parsing. | data = json.load(f, cls=MyDecoder) |
json.loads (with parse_float) | Custom float parsing | Calls a function for every JSON float (e.g., convert to Decimal). | data = json.loads(s, parse_float=Decimal) |
json.loads (with parse_int) | Custom int parsing | Calls a function for every JSON integer. | data = json.loads(s, parse_int=str) |
json.loads (with parse_constant) | Handle special constants | Calls a function for NaN, Infinity, -Infinity values. | data = json.loads(s, parse_constant=lambda x: None) |
json.tool | Command-line JSON tool | Module for pretty-printing and validating JSON from the command line. | python -m json.tool data.json |
json.scanstring | Scan a JSON string | Low-level function to scan a JSON string (used internally by the decoder). | s, end = json.decoder.scanstring('"hello"', 0) |
json.decoder.JSONScanner | JSON scanner object | Low-level scanner for tokenizing JSON input. | scanner = json.decoder.JSONScanner() |
json.encoder.encode_basestring | Encode string for JSON | Escapes special characters in a string for JSON output. | safe = json.encoder.encode_basestring("hello\\nworld") |
json.encoder.encode_basestring_ascii | ASCII-safe string encoding | Like encode_basestring but ensures ASCII output. | safe = json.encoder.encode_basestring_ascii("cafe") |
json.encoder.FLOAT_REPR | Float representation (legacy) | Controls how floats are represented (deprecated, use default parameter). | json.encoder.FLOAT_REPR = lambda o: format(o, ".2f") |
json.decoder.py_scanstring | Python string scanner | Pure Python implementation of JSON string scanning. | s, end = json.decoder.py_scanstring('"test"', 0) |
json.decoder.c_scanstring | C string scanner | C-optimized version of string scanning (faster, used by default if available). | s, end = json.decoder.c_scanstring('"test"', 0) |



## 8️⃣ WARNINGS



warnings.filterwarnings | Control warning display | Configures which warnings are shown, ignored, or converted to errors. Critical for clean output. | warnings.filterwarnings("ignore") |
warnings.warn | Emit a custom warning | Raises a warning message from your own code to alert users about deprecated features or issues. | warnings.warn("This function is deprecated", DeprecationWarning) |
warnings.catch_warnings | Context manager for warnings | Temporarily modifies warning behavior within a code block, then restores original settings. | with warnings.catch_warnings(): warnings.filterwarnings("ignore"); ... |
warnings.simplefilter | Simple warning filter | Adds a single filter action (ignore, always, error, default, module, once). | warnings.simplefilter("ignore", category=FutureWarning) |
warnings