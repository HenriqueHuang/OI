SELECT \*
FROM "Temperatura"
WHERE
time >= now() - interval '15 minutes'
AND
("temperatura" IS NOT NULL OR "umiadade" IS NOT NULL)
