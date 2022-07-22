Combien la base de données contient-elle de sociétés offshores différentes dont la source est "Panama Papers" ?

SELECT count (DISTINCT entity.name)
FROM entity



Quel intermédiaire a créé le plus de sociétés offshores ? A-t-on son adresse et son pays ?
On voit que la table assoc_inter_entities reprend l'id des intermédiaires et des entities 
Il faut faire une jointure entre assoc_inter_entities, entity et intermediary. 


SELECT COUNT(intermediary.name), intermediary.name
FROM intermediary
INNER JOIN assoc_inter_entity ON assoc_inter_entity.inter = intermediary.id
INNER JOIN entity ON entity.id = assoc_inter_entity.entity
GROUP by intermediary.name 
ORDER by COUNT(intermediary.name) DESC
LIMIT 1





Combien la base contient-elle de bénéficiaires avec un nom unique ? Quel est le bénéficiaire dont le nom revient le plus souvent ?
1 ) SELECT count(DISTINCT name) from officer
2 ) SELECT count(officer.name), officer.name --> pas certain de la source qu'il faut utiliser. 
from officer
GROUP by officer.name
ORDER BY count(officer.name) DESC



Donner la liste des juridictions avec le nombre d'entreprises offshores enregistrées sur chaque territoire, triée par ordre décroissant.
SELECT jurisdiction, count(jurisdiction)
from entity
GROUP by jurisdiction
ORDER by count(jurisdiction) DESC




Regrouper les sociétés offshores par statut, et trier la liste par ordre décroissant.

SELECT name, status
from entity
GROUP BY name
order by status DESC


Trouver la liste des bénéficiaires dont le nom contient "BNP" et ajouter, pour chaque bénéficiaire, le nom des sociétés offshores. ==> pour moi bénéficiaires sont les officers 

SELECT officer.name as 'BNP entities', entity.name AS 'société écran'
FROM officer
INNER JOIN assoc_officer_entity ON assoc_officer_entity.officer = officer.id
INNER JOIN entity ON entity.id = assoc_officer_entity.entity
WHERE officer.name LIKE '%BNP%'
order by officer.name asc



Trouver la liste des sociétés dont la juridiction est "France", "Monaco" ou "Réunion". == > juridiction uniquement, aucun mais si on prend l'adresse oui

SELECT entity.name, address.country_codes
FROM entity
INNER JOIN address ON address.id_address = entity.id_address
WHERE address.country_codes like '%France%' or address.country_codes like '%Monaco%' or address.country_codes like '%Réunion%'
GROUP BY entity.name
ORDER by address.country_codes ASC



Trouver la liste des sociétés dont le pays de l'adresse et le pays de la juridiction sont différents.
Trouver la liste des bénéficiaires qui ont des sociétés au même nom et enregistrée à la même date, trier la liste par odre décroissant.
Donner la liste des intermédiaires qui ont aussi été bénéficiaires, en ajoutant leur nom de bénéficiaire et leur adresse.
Donner le top 10 des bénéficiaires qui ont le plus d'identités différentes (similar name and address) et le nombre d'identités correspondant.
Donner le top 10 des bénéficiaires qui ont le plus de parts toujours valides dans des entreprises offshores (dont la date de fin n'est pas encore passée).
Question bonus : réussir à retrouver dans la base au moins 3 personnalités que tu connais (indice) 😎😎😎
