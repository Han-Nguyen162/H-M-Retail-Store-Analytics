-- 1. Store Format Penetration by Country (Premium vs. Standard)
    SELECT 
        Location.CountryCode,
        Store.StoreClass,
        COUNT(Store.StoreCode) AS StoreCount,
        ROUND(100.0 * COUNT(Store.StoreCode) / 
            SUM(COUNT(Store.StoreCode)) OVER (PARTITION BY Location.CountryCode), 2) AS ClassSharePercent
    FROM Store
    JOIN Location ON Store.StoreCode = Location.StoreCode
    GROUP BY Location.CountryCode, Store.StoreClass
    ORDER BY Location.CountryCode, ClassSharePercent DESC;

-- 2. Calculate Actual Hours Open on Sat + Sun (using STR_TO_DATE)
    SELECT 
        loc.City,
        loc.CountryCode,
        COUNT(DISTINCT loc.StoreCode) AS StoreCount,
        ROUND(AVG(
            TIME_TO_SEC(
                TIMEDIFF(
                    STR_TO_DATE(SUBSTRING_INDEX(oh.Sat_Open_Hours, '-', -1), '%H:%i'),
                    STR_TO_DATE(SUBSTRING_INDEX(oh.Sat_Open_Hours, '-', 1), '%H:%i')
                )
            ) +
            TIME_TO_SEC(
                TIMEDIFF(
                    STR_TO_DATE(SUBSTRING_INDEX(oh.Sun_Open_Hours, '-', -1), '%H:%i'),
                    STR_TO_DATE(SUBSTRING_INDEX(oh.Sun_Open_Hours, '-', 1), '%H:%i')
                )
            )
        ) / 3600, 2) AS AvgWeekendHoursPerStore
    FROM Location loc
    JOIN OpeningHours oh ON loc.StoreCode = oh.StoreCode
    WHERE oh.Sat_Open_Hours IS NOT NULL AND oh.Sun_Open_Hours IS NOT NULL
    GROUP BY loc.City, loc.CountryCode
    ORDER BY AvgWeekendHoursPerStore DESC
    LIMIT 20;

-- 3. Store Density Analysis – Cities with Most Stores in Close Proximity

    WITH StorePairs AS (
        SELECT 
            l1.City,
            l1.StoreCode AS Store1,
            l2.StoreCode AS Store2,
            ST_Distance_Sphere(
                POINT(g1.Longitude, g1.Latitude), 
                POINT(g2.Longitude, g2.Latitude)
            ) / 1000 AS DistanceKM
        FROM Location l1
        JOIN GeoDetails g1 ON l1.StoreCode = g1.StoreCode
        JOIN Location l2 ON l1.City = l2.City AND l1.StoreCode < l2.StoreCode
        JOIN GeoDetails g2 ON l2.StoreCode = g2.StoreCode
        WHERE ST_Distance_Sphere(
            POINT(g1.Longitude, g1.Latitude), 
            POINT(g2.Longitude, g2.Latitude)
        ) / 1000 <= 10
    ),
    CityCoords AS (
        SELECT 
            l.City,
            AVG(g.Latitude) AS CityLatitude,
            AVG(g.Longitude) AS CityLongitude
        FROM Location l
        JOIN GeoDetails g ON l.StoreCode = g.StoreCode
        GROUP BY l.City
    )
    SELECT 
        sp.City,
        COUNT(*) AS StorePairsWithin10KM,
        ROUND(COUNT(*) * 100.0 / (SELECT COUNT(*) FROM Store), 2) AS ClusteredPairsPercent,
        cc.CityLatitude,
        cc.CityLongitude
    FROM StorePairs sp
    JOIN CityCoords cc ON sp.City = cc.City
    GROUP BY sp.City, cc.CityLatitude, cc.CityLongitude
    ORDER BY StorePairsWithin10KM DESC
    LIMIT 15; 
