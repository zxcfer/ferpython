---
layout: post
title: "Creating a Date Dimension or Calendar Table"
tags: ["database", "SQL", "MySQL"]
---

# Creating a date dimension or calendar table

```sql
DROP TABLE IF EXISTS `integers`;
CREATE TABLE integers (i INTEGER);
INSERT INTO integers (i) VALUES (0), (1), (2), (3), (4), (5), (6), (7), (8), (9);

DROP TABLE IF EXISTS `dim_tiempo`;
CREATE TABLE `dim_tiempo` (
  `tiempo_id` INT(8) PRIMARY KEY,
  `fecha` DATE NOT NULL,
  `dia_id` INT(11) DEFAULT NULL,
  `dia_nombre` VARCHAR(100) DEFAULT NULL,
  `mes_id` INT(11) DEFAULT NULL,
  `mes_nombre` VARCHAR(100) DEFAULT NULL,
  `trimestre_id` INT(11) DEFAULT NULL,
  `trimestre_nombre` VARCHAR(100) DEFAULT NULL,
  `semestre_id` INT(11) DEFAULT NULL,
  `semestre_nombre` VARCHAR(100) DEFAULT NULL,
  `ano` INT(4) DEFAULT NULL,
  `cuatrimestre_id` INT(1) DEFAULT NULL,
  `cuatrimestre_nombre` VARCHAR(100) DEFAULT NULL,
  `dia_semana` INT(1) DEFAULT NULL
);

INSERT INTO dim_tiempo
SELECT 	CONCAT(	YEAR(fecha),
		IF(CHAR_LENGTH(MONTH(fecha))<2, CONCAT('0',MONTH(fecha)), MONTH(fecha)),
		IF(CHAR_LENGTH(DAY(fecha))<2, CONCAT('0',DAY(fecha)), DAY(fecha))
	) AS tiempo_id,
	fecha AS fecha,
	NULL AS `dia_id`,
	NULL AS `dia_nombre`,
  	NULL AS `mes_id`,
  	NULL AS `mes_nombre`,
  	NULL AS `trimestre_id`,
  	NULL AS `trimestre_nombre`,
  	NULL AS `semestre_id`,
  	NULL AS `semestre_nombre`,
  	NULL AS `ano`,
  	NULL AS `cuatrimestre_id`,
  	NULL AS `cuatrimestre_nombre`,
  	NULL AS `dia_semana`
  	FROM ( SELECT ('1995-06-25' + INTERVAL t.i*1000 + u.i*100 + v.i*10 + w.i DAY) AS fecha
		FROM integers AS t
		JOIN integers AS u
		JOIN integers AS v
		JOIN integers AS w
		WHERE ( t.i*1000 + u.i*100 + v.i*10 + w.i) < 10000
		ORDER BY fecha ) AS calendar;
```