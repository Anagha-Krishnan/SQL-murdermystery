# SQL-murdermystery
SELECT *
  FROM crime_scene_report where type='murder' and city='SQL City' and date=20180115

output---Security footage shows that there were 2 witnesses. The first witness lives at the last house on "Northwestern Dr". The second witness, named Annabel, lives somewhere on "Franklin Ave".

SELECT *
  FROM person where address_street_name='Northwestern Dr' or'Franklin Ave'


SELECT *
  FROM person where address_street_name='Northwestern Dr'ORDER BY address_number DESC
limit 1

output---14887	Morty Schapiro	118009	4919	Northwestern Dr	111564949

SELECT *
  FROM person where name like '%Annabel%' and address_street_name='Franklin Ave'

output---16371	Annabel Miller	490173	103	Franklin Ave	318771143

SELECT *
  FROM interview where person_id=14887

output---->I heard a gunshot and then saw a man run out. He had a "Get Fit Now Gym" bag. The membership number on the bag started with "48Z". Only gold members have those bags. The man got into a car with a plate that included "H42W".
----->16371	I saw the murder happen, and I recognized the killer from my gym when I was working out last week on January the 9th.

SELECT * 
FROM get_fit_now_member 
where person_id=12711

output---90081	16371	Annabel Miller	20160208	gold

SELECT * 
FROM get_fit_now_check_in 
where check_in_date=20180109 and membership_id like'%48Z%'
---48Z7A	20180109	1600	1730
---48Z55	20180109	1530	1700

SELECT * 
FROM get_fit_now_member 
WHERE id = '48Z7A' OR id = '48Z55';

output--->48Z55	67318	Jeremy Bowers	20160101	gold
48Z7A	28819	Joe Germuska	20160305	gold

SELECT * 
FROM drivers_license 
where plate_number like '%H42W%'

output---->183779	21	65	blue	blonde	female	H42W0X	Toyota	Prius
423327	30	70	brown	brown	male	0H42W2	Chevrolet	Spark LS
664760	21	71	black	black	male	4H42WR	Nissan	Altima

SELECT * 
FROM person 
where license_id=423327	 or license_id=664760	

output--->51739	Tushar Chandra	664760	312	Phi St	137882671
67318	Jeremy Bowers	423327	530	Washington Pl, Apt 3A	871539279

----FINAL ANSWER FOR MURDER-------
SELECT * 
FROM person 
WHERE (license_id=423327 OR license_id=664760) AND (id=67318 OR id=28819);

output---->
id	name	license_id	address_number	address_street_name	ssn
67318	Jeremy Bowers	423327	530	Washington Pl, Apt 3A	871539279
