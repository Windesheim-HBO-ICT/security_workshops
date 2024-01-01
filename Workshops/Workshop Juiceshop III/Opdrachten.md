# Juice shop III opdrachten

## Opdracht 13: Laat de server met NoSQL slapen door een NoSQL injection

### ASVS:

- V5.3.4 Verify that data selection or database queries (e.g. SQL, HQL, ORM, NoSQL) use parameterized queries, ORMs, entity frameworks, or are otherwise protected from database injection attacks.

### Opdracht:

1. Maak gebruik van de API om de reviews van het database ID 1 op te halen. (http://localhost:3000/rest/products/1/reviews)
2. Door iets in de URL te veranderen kan je de reviews van een ander product ophalen. (http://localhost:3000/rest/products/2/reviews)
3. Door iets in de URL te veranderen kan je ook de server laten slapen. (http://localhost:3000/rest/products/sleep(2000)/reviews)
4. De Juice Shop is nu (tijdelijk) niet meer bereikbaar. Gefeliciteerd! Je hebt nu een NoSQL injection uitgevoerd op de Juice Shop.

## Opdracht 14: Krijg toegang tot een vergeten backup bestand via een Poison Null Byte

### ASVS:

- V4.2.1 Verify that sensitive data and APIs are protected against Insecure Direct Object Reference (IDOR) attacks targeting creation, reading, updating and deletion of records, such as creating or updating someone else's record, viewing everyone's records, or deleting all records.

### Opdracht:

1. Ga naar de FTP server van de Juice Shop. (http://localhost:3000/ftp).
2. Het doel is om het bestand `package.json.bak` te downloaden.
3. Als dit bestand wordt aangeklikt wordt er een error getoond: Dit is een backup bestand, waarvan het downloaden niet is niet toegestaan.
4. Door gebruik te maken van een Poison Null Byte kan je dit bestand toch downloaden.
5. De Poison Null Byte is `%00`.
6. De URL wordt dan: `http://localhost:3000/ftp/package.json.bak%00.md`
7. Dit werkt echter niet, omdat de Juice Shop de URL encodeert.
8. Door zelf de null byte te encoderen kan je het bestand toch downloaden.
9. De URL wordt dan: `http://localhost:3000/ftp/package.json.bak%25%30%30.md`
10. Gefeliciteerd! Je hebt nu een toegan tot een vergeten backup bestand.
