+++
title = 'About'
date = 2024-09-14T21:26:09+08:00
draft = false
+++

start

```python
import math
import numpy as np

def get_tile_number(latitude, longitude, zoom_level):
    num_tiles = 2 ** zoom_level

    # 计算每个瓦片的经度和纬度范围
    tile_longitude_range = 360.0 / num_tiles
    tile_latitude_range = 170.1022 / num_tiles

    # 计算给定经纬度点所属的瓦片行列号
    tile_column = int((longitude + 180) / tile_longitude_range)
    tile_row = int((90 - latitude) / tile_latitude_range)


#     tileX = (longitude + 180) / 360 * (2 ** zoom_level)
#     tileY = 1/2 - (np.log())  math.sec
# (180 - Math.log(Math.tan(Math.PI / 4 + lat * Math.PI / 360)) * 180 / Math.PI) / 360
#     return tile_column, tile_row

# 示例经纬度点
latitude = 22.962191
longitude = 113.888899
zoom_level = 12

# tile_column, tile_row = get_tile_number(latitude, longitude, zoom_level)
# print("瓦片行列号：", tile_column, tile_row)


import math
def deg2num(lat_deg, lon_deg, zoom):
  lat_rad = math.radians(lat_deg)
  n = 1 << zoom
  xtile = int((lon_deg + 180.0) / 360.0 * n)
  ytile = int((1.0 - math.asinh(math.tan(lat_rad)) / math.pi) / 2.0 * n)
  return xtile, ytile

print("公司:",deg2num(22.962191,113.888899,zoom_level))
print("刘臻:",deg2num(34.0240280,-118.5022140,zoom_level))
print(deg2num(22.959263,113.893807,zoom_level))
print(deg2num(22.962191,113.888902,zoom_level))

# lat':340240280,'long':-1185022140
```

end