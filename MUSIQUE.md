Commandes sql pour traiter les données de la BDD présente dans le repo. 


Récupérer tous les albums écrits par AC/DC : 

SELECT albums.title
FROM albums
INNER JOIN artists ON albums.ArtistId=artists.ArtistId 
where artists.name = 'AC/DC';



Récupérer tous les titres des albums de AC/DC : 

SELECT tracks.name
FROM tracks
INNER JOIN albums ON albums.AlbumId = tracks.albumid
INNER JOIN artists ON albums.ArtistId = artists.artistid
where artists.name = 'AC/DC';





Récupérer la liste des titres de l'album "Let There Be Rock"
SELECT tracks.Name
FROM tracks
INNER JOIN albums ON tracks.AlbumId = albums.AlbumId
where albums.title = 'Let There Be Rock'



Afficher le prix de cet album ainsi que sa durée totale

SELECT sum(invoice_items.unitprice), sum(tracks.Milliseconds)/60000
FROM invoice_items
INNER JOIN albums ON tracks.AlbumId = albums.AlbumId
INNER JOIN tracks ON tracks.TrackId = invoice_items.TrackId
WHERE albums.AlbumId = '4'


Afficher le coût de l'intégralité de la discographie de "Deep Purple"

SELECT sum(invoice_items.unitprice)
FROM invoice_items
INNER JOIN artists ON artists.ArtistId = albums.ArtistId
INNER JOIN albums ON tracks.AlbumId = albums.AlbumId
INNER JOIN tracks ON tracks.TrackId = invoice_items.TrackId
WHERE artists.Name = 'Deep Purple'



Créer l'album de ton artiste favori en base, en renseignant correctement les trois tables albums, artists et tracks

SELECT albums.Title, artists.Name, tracks.Name
FROM albums
INNER JOIN artists ON artists.ArtistId = albums.ArtistId
INNER JOIN tracks ON tracks.AlbumId = albums.AlbumId
WHERE albums.Title = 'Machine Head'
