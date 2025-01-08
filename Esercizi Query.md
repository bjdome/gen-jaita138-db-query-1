-- 1)Recupera tutti gli utenti registrati nel sistema.

SELECT *

FROM utenti u

  

-- 2)Recupera il nome, cognome e email di tutti gli utenti iscritti dopo il 1° marzo 2024.

SELECT u.nome, u.cognome, u.email

FROM utenti u

WHERE u.data_iscrizione > '2024-03-01'

  

-- 3)Recupera tutti gli articoli insieme al nome e cognome dell'autore.

SELECT a.titolo, a.contenuto, a.data_pubblicazione, a.prezzo, u.nome, u.cognome

FROM articoli a

JOIN utenti u

ON a.id_utente = u.id_utente

  

-- 4)Recupera i titoli degli articoli pubblicati nel mese di maggio 2024.

SELECT a.titolo

FROM articoli a

WHERE a.data_pubblicazione >= '2024-05-01'

  

-- 5)Recupera le prime 5 categorie ordinate alfabeticamente per nome.

SELECT c.nome_categoria

FROM categorie c

ORDER BY c.nome_categoria

LIMIT 5

  

-- 6)Recupera gli articoli che appartengono alla categoria 'Tecnologia'.

SELECT a.titolo, a.contenuto, a.data_pubblicazione, a.prezzo

FROM articoli a

JOIN articoli_categorie ac

ON a.id_articolo = ac.id_articolo

JOIN categorie c

ON ac.id_categoria = c.id_categoria

WHERE c.nome_categoria = 'Tecnologia'

  

-- 7)Recupera le email degli utenti che hanno scritto almeno un articolo.

SELECT u.email

FROM utenti u

JOIN articoli a

ON u.id_utente = a.id_utente

  

-- 8)Recupera tutti gli articoli pubblicati tra il 1° giugno 2024 e il 31 agosto 2024.

SELECT *

FROM articoli a

WHERE a.data_pubblicazione BETWEEN '2024-06-01' AND '2024-08-31'

  

-- 9)Recupera i dettagli delle categorie associate all'articolo con id_articolo = 10.

SELECT *

FROM categorie c

JOIN articoli_categorie ac

ON c.id_categoria = ac.id_categoria

JOIN articoli a

ON ac.id_articolo = a.id_articolo

WHERE ac.id_articolo = 10

  

-- 10)Recupera i nomi degli utenti ordinati per data di iscrizione più recente.

SELECT u.nome

FROM utenti u

ORDER BY data_iscrizione DESC

  

-- 11)Conta il numero di articoli scritti da ogni utente.

SELECT a.id_utente, u.nome, u.cognome, COUNT(*)

FROM utenti u

JOIN articoli a

ON u.id_utente = a.id_utente

GROUP BY a.id_utente

  

-- 12)Trova la categoria con il maggior numero di articoli associati.

SELECT c.id_categoria, count(ac.id_articolo) AS 'numero'

FROM categorie c

JOIN articoli_categorie ac

ON c.id_categoria = ac.id_categoria

JOIN articoli a

ON ac.id_articolo = a.id_articolo

GROUP BY c.id_categoria

ORDER BY 'numero' DESC

LIMIT 1

  

-- 13)Recupera gli utenti che hanno scritto più di 2 articoli.

SELECT u.nome, u.cognome, u.id_utente, count(a.id_articolo) AS 'numero articoli'

FROM utenti u

JOIN articoli a

ON u.id_utente = a.id_utente

GROUP BY u.id_utente

HAVING count(a.id_articolo) > 2

  

-- 14)Calcola la data di pubblicazione più recente per ogni categoria.

SELECT c.nome_categoria, MAX(a.data_pubblicazione) AS data_pubblicazione_piu_recente

FROM categorie c

JOIN articoli_categorie ac

ON c.id_categoria = ac.id_categoria

JOIN articoli a

ON ac.id_articolo = a.id_articolo

GROUP BY

c.id_categoria, c.nome_categoria

  

  

-- 15)Trova il numero medio di articoli per utente.

  

  

-- 16)Recupera le categorie che hanno almeno 3 articoli associati.

SELECT c.nome_categoria, COUNT(ac.id_articolo) AS numero_articoli

FROM categorie c

JOIN articoli_categorie ac

ON c.id_categoria = ac.id_categoria

GROUP BY c.id_categoria

HAVING COUNT(ac.id_articolo) >= 3

  

-- 17)Calcola il totale degli articoli pubblicati per ogni mese del 2024.

SELECT YEAR(data_pubblicazione) AS 'anno', MONTH(data_pubblicazione) AS 'mese', COUNT(id_articolo) AS 'numero articoli'

FROM articoli a

WHERE YEAR(data_pubblicazione) = 2024

GROUP BY YEAR(data_pubblicazione), MONTH(data_pubblicazione)

ORDER BY 'mese'

  

-- 18)Trova l'utente che ha la data di iscrizione più antica.

SELECT u.nome, u.cognome, u.email, u.data_iscrizione

FROM utenti u

ORDER BY data_iscrizione ASC

LIMIT 1;

  

-- 19)Recupera le categorie e il numero di articoli associati a ciascuna, ordinati dal più al meno.

SELECT c.nome_categoria, COUNT(ac.id_articolo) AS 'numero articoli'

FROM categorie c

LEFT JOIN articoli_categorie ac

ON c.id_categoria = ac.id_categoria

GROUP BY c.id_categoria, c.nome_categoria

ORDER BY 'numero articoli' DESC;

  

-- 20)Calcola il numero totale di articoli pubblicati da utenti iscritti nel 2024.

SELECT COUNT(a.id_articolo) AS 'numero articoli'

FROM articoli a

JOIN Utenti u

ON a.id_utente = u.id_utente

WHERE YEAR(u.data_iscrizione) = 2024;

  

-- 21)Recupera gli utenti che non hanno scritto nessun articolo.

SELECT u.id_utente, u.nome, u.cognome, u.email

FROM utenti u

LEFT JOIN articoli a

ON u.id_utente = a.id_utente

WHERE a.id_articolo IS NULL;

  

-- 22)Trova le categorie che non hanno alcun articolo associato.

SELECT c.id_categoria, c.nome_categoria

FROM categorie c

LEFT JOIN articoli_categorie ac

ON c.id_categoria = ac.id_categoria

WHERE ac.id_articolo IS NULL;

  

-- 23)Trova le categorie che contengono articoli scritti da utenti iscritti prima del 2024.

SELECT c.id_categoria, c.nome_categoria

FROM categorie c

JOIN articoli_categorie ac

ON c.id_categoria = ac.id_categoria

JOIN articoli a

ON ac.id_articolo = a.id_articolo

JOIN utenti u

ON a.id_utente = u.id_utente

WHERE u.data_iscrizione < '2024-01-01';

  

-- 24)Recupera le categorie che sono associate ad almeno 5 articoli pubblicati nel 2024.

SELECT c.id_categoria, c.nome_categoria, COUNT(ac.id_articolo)

FROM categorie c

JOIN articoli_categorie ac

ON c.id_categoria = ac.id_categoria

JOIN articoli a

ON ac.id_articolo = a.id_articolo

WHERE a.data_pubblicazione BETWEEN '2024-01-01' AND '2024-12-31'

GROUP BY c.id_categoria, c.nome_categoria

HAVING COUNT(ac.id_articolo) >= 5;