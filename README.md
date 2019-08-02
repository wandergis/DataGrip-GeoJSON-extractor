# DataGrip-GeoJSON-extractor
A extractor for DataGrip to export geojson in sql query directly.
```sql
SELECT row_to_json(fc)
FROM (SELECT 'FeatureCollection' As type, array_to_json(array_agg(f)) As features
      FROM (SELECT 'Feature'                      As type
                 , ST_AsGeoJSON(lg.geom, 4)::json As geometry
                 , row_to_json((SELECT l
                                FROM (SELECT loc_id, loc_name) As l
          ))                                      As properties
            FROM locations As lg) As f) As fc;
```
