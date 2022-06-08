# Data Catalog: /data/raw/

Some (but not all) data schemas have been provided below.

## camera_metadata_manual.csv

| Attribute      | Type | Description     |
| :---        | :----    | :---            |
| camera_id      | str       | Unique identifier for the camera consisting of station and direction. Originally comes from firemap pylaski api. For manual cameras added that do not exist in pylaski, "hpwren_missing#\_direction" was added. I.e. hpwren1_north, hpwren_missing1_north.   |
| image_id   | str        | Another form of camera identifer that is parsed from image urls, hence, calling it the image id. I.e. buff-n-mobo-c      |
| camera_name   | str        | Camera station name.      |
| direction   | str        | Direction of camera. North, east, south, west. All lowercase.      |
| gmap_lat   | float        | Corrected camera lat location with more precision determined via google maps.     |
| gmap_long   | float        | Corrected camera long location with more precision determined via google maps.      |
| elevation   | int        | Camera metadata. For manual inputs, taken from hpwren website for individual station (top of page, not lower section).      |
| x_resolution   | int        | Station camera image pixel size for x, taken by analyzing image/looking at image exif data.     |
| y_resolution   | int        | Station camera image pixel size for y, taken by analyzing image/looking at image exif data.      |
| center_lat   | float        | Lat of point along the camera field of view center line. Determined by looking at camera image, drawing vertical centerline at pixel center, and finding distinguishable landmark very close to centerline to take location of from google maps. Center point value used to calculate angle of camera away from its true_direction (north, east, south, west). I.e. Used to calculate correction to the direction documented.      |
| center_long   | float        | Long of point along the camera field of view center line. Determined by looking at camera image, drawing vertical centerline at pixel center, and finding distinguishable landmark very close to centerline to take location of from google maps. Center point value used to calculate angle of camera away from its true_direction (north, east, south, west). I.e. Used to calculate correction to the direction documented.       |

## smokeynet_test.json<br>smokeynet_train.json<br>smokeynet_valid.json

Smokeynet files are in json where each object represents 1 image prediction set.<br>
The attributes for each one of these objects are below:

| Attribute      | Type | Description     |
| :---        | :----    | :---            |
| camera_name      | str       | Full FIgLib fire event name (folder name) that the image came from. Follows **YearMonthDay\_\<Fire\_Name\>\_\<Camera_Name\>** where "camera_name" is also known as the "image_id" used in image url. I.e. buff-n-mobo-c.            |
| image_gt      | int       | Actual groundtruth smoke value. 1 for yes smoke, 0 for no smoke.            |
| tile_gt      | int[]       | Int list of groundtruth values for each tile of an image. As of now ALL will be empty list because not bounding box/contour mask labels were provided; only whole image labels. Placeholder for when additional labeling gets done.            |
| image_pred      | int       | Image prediction smoke value. 1 for yes smoke, 0 for no smoke.            |
| tile_pred      | int[]       | Int list of prediction values for each tile of an image. Currently, 45 tiles per image. 0 is top left tile of image. Goes left to right in row. Restarts left to right at each row.          |