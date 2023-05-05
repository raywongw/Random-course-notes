



### Q7
non recursive query
```MySQL
select      s3.parent_area_ID as parent3_id,
            s2.parent_area_ID as parent2_id,
            s1.parent_area_ID as parent_id,
            s1.service_area_ID as product_id,
            s1.name
from        servicearea s1
left join   servicearea s2 on s2.service_area_ID = s1.parent_area_ID 
left join   servicearea s3 on s3.service_area_ID = s2.parent_area_ID 
where       (SELECT service_area_ID FROM servicearea 
			 WHERE name = 'Hong Kong Island') in (s1.parent_area_ID, s2.parent_area_ID, s3.parent_area_ID);
```

recursive query
```MySQL
WITH RECURSIVE subtree AS (
    SELECT service_area_ID, parent_area_ID, name
    FROM servicearea
    WHERE service_area_ID IN (SELECT service_area_ID FROM servicearea WHERE name = 'Hong Kong Island')
    UNION ALL
    SELECT s.service_area_ID, s.parent_area_ID, s.name
    FROM servicearea s
    JOIN subtree st ON s.parent_area_ID = st.service_area_ID
)
SELECT *
FROM subtree
WHERE NOT EXISTS (
  SELECT 1
  FROM servicearea s
  WHERE s.parent_area_ID = subtree.service_area_ID
);
```



```MySQL
SELECT LPO.order_ID, N.locker_name, N.service_Area_name FROM lockerpickuporder LPO 
INNER JOIN (SELECT L.name AS locker_name, L.locker_ID, M.name as service_Area_name FROM locker L 
            INNER JOIN (WITH RECURSIVE subtree AS (
                SELECT service_area_ID, parent_area_ID, name FROM servicearea
                WHERE service_area_ID IN (SELECT service_area_ID FROM servicearea WHERE name = 'Hong Kong Island') 
                UNION ALL 
                SELECT s.service_area_ID, s.parent_area_ID, s.name FROM servicearea s 
                JOIN subtree st 
                ON s.parent_area_ID = st.service_area_ID )
                        SELECT service_area_ID, name FROM subtree 
                        WHERE NOT EXISTS ( SELECT 1 FROM servicearea s WHERE s.parent_area_ID = subtree.service_area_ID )) m 
ON M.service_area_ID = L.service_area_ID) n ON LPO.locker_ID = N.locker_ID;
```
### Q8

```MySQL
SELECT s.* FROM servicearea s
WHERE NOT EXISTS (SELECT 1 FROM servicearea s2 WHERE s2.parent_area_ID = s.service_area_ID);
``````