# German-Zipcode-Database

**!!! GERMANY ONLY !!!**

## Whats this?
This is a MySQL zipcode database for german addresses containing city, state and provinces

## Query examples:
* SELECT * FROM zip.joined WHERE Zipcode LIKE '78052';
* SELECT * FROM zip.zipcode INNER JOIN zip.city ON zip.zipcode.city_id=zip.city.id WHERE zip.city.name LIKE 'Miltenberg';

## Database structure
```
CREATE TABLE `zip.city` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `state_id` int(11) NOT NULL,
  `county_id` int(11) NOT NULL,
  `name` varchar(200) NOT NULL,
  PRIMARY KEY (`id`)
)

CREATE TABLE `zip.county` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `state_id` int(11) NOT NULL,
  `name` varchar(200) NOT NULL,
  PRIMARY KEY (`id`)
)

CREATE TABLE `zip.state` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(200) NOT NULL,
  PRIMARY KEY (`id`)
)

CREATE TABLE `zip.zipcode` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `city_id` int(11) NOT NULL,
  `zipcode` varchar(10) NOT NULL,
  PRIMARY KEY (`id`)
)

CREATE VIEW zip.joined
	AS SELECT zip.city.name AS 'City',
	zip.county.name AS 'County',
	zip.state.name AS 'State',
	zip.zipcode.zipcode AS 'Zipcode'
FROM zip.city
INNER JOIN zip.county
	ON zip.city.county_id=zip.county.id
INNER JOIN zip.state
	ON zip.city.state_id=zip.state.id
INNER JOIN zip.zipcode
	ON zip.city.id=zip.zipcode.city_id;
```

## Credits
Everything needed was found on www.opengeodb.org.
