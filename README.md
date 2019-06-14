# sql_opdrachten


Geef de namen van de Franstalige personen van wie de naam begint met een 'M'.
SELECT personen.naam FROM personen WHERE persoon_taal=’F’ AND naam LIKE "m%";

Geef de referenties en de namen van de personen, gesorteerd volgens het referentienummer van hoog naar laag. Gebruik bij het sorteren een nummer in plaats van een kolomnaam.
SELECT persoon_id, naam FROM personen order by 1;

Geef de productcode en het productnummer van de producten waarbij een locatie is ingevuld.
SELECT product_code, product_id FROM product WHERE locatie_nr IS NOT NULL;

Geef de productcode en het productnummer van de producten met een productnummer tussen de 5 en 15 en de producten met een productnummer tussen de 30 en 50.
SELECT product_code, product_nr FROM product WHERE product_nr BETWEEN 5 AND 15 OR product_nr BETWEEN 30 AND 50;

Geef de productcode en het productnummer van de producten met productnummer 5,10,20,25. Maak gebruik van IN.
SELECT product_code, product_nr FROM producten WHERE product_nr IN(5, 10, 15, 20, 25);

Geef de naam en voornaam van de personen waarbij de laatste letter van de achternaam een 's' is en de eerste letter van de voornaam een 'f' of een 'p'.
SELECT persoon_naam, persoon_voornaam FROM persoon WHERE (persoon_naam LIKE '%S')AND (persoon_voornaam LIKE 'F%' OR persoon_voornaam LIKE 'P%');

Geef de namen van de personen van de Nederlandstalige en/of Franstalige taalgroep, hun geslacht ('man' of 'vrouw') en hun taal ('Nederlandstalig' of 'Franstalig').
SELECT persoon_naam as Naam, persoon_voornaam as Voornaam,  persoon_taal Taal FROM persoon order by persoon_taal, persoon_geslacht;

Hoeveel Franstalige personen zijn er?
SELECT COUNT(persoon_id) FROM persoon WHERE persoon_taal = 'F';

Geef de productcode en het productnummer van de producten waarbij geen oorsprong is ingevuld.
SELECT product_code, product_nr FROM product WHERE oorsprong_nr IS NULL;

Geef de productcode, het productnummer en de naam van de locatie. In de gevallen dat de naam van de locatie niet is ingevuld, moet er in die plaats geen worden vermeld.
SELECT product.product_code, product.product_id, IFNULL(locatie.locatie_naam, 'geen')FROM product LEFT JOIN locatie ON product.locatie_nr = locatie.locatie_id

Geef de namen van de locaties waarvan de naam uit 16 letters bestaat, maar waarin het woord 'Magazijn' voorkomt.
SELECT locatie_naam FROM locatie WHERE locatie_naam LIKE '%MAGAZIJN%' AND LENGTH(locatie_naam) = 16

Geef de productcode en het productnummer van de producten met productcode 'HA' of 'NE' maar waarvan het productnummer kleiner is dan 15.
SELECT DISTINCT product_code, product_nr FROM product WHERE product_nr<15 AND product_code='HA' OR product_code='NE'

Geef de productcode en het nummer van die producten waarbij de naam van de locatie begint met 'maga'. Maak gebruik van de principes van Subquery.
SELECT product.product_code, product.product_nr FROM product WHERE EXISTS(SELECT locatie_naam FROM locatie WHERE product.locatie_nr=locatie.locatie_id AND locatie_naam LIKE 'maga%');

Verhuis alle producten van magazijn 1 naar magazijn 2.
UPDATE product SET locatie_nr=3 WHERE locatie_nr=1;

Verwijder alle producten van Millie.
DELETE FROM product WHERE oorsprong_nr=14;
