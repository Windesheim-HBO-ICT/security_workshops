# Juice Shop III opdrachten

## Opdracht 13: DoS aanval op de Juice Shop

### ASVS:

- **V10.3 | Malicious Code**: Verify that the application protects against malicious code being inserted into the application, such as through code injection, and that the application can detect and respond to such attacks.

### Uitleg:

https://pwning.owasp-juice.shop/companion-guide/latest/appendix/solutions.html#_perform_a_remote_code_execution_that_would_keep_a_less_hardened_application_busy_forever

<!-- not yet working -->

1. Open de swagger documentatie van de Juice Shop API. (http://localhost:3000/api-docs)
2. Haal je auth token op uit de developer tools van de webbrowser.
3. Plak je auth token in de swagger documentatie. (Klik op Authorize rechts bovenaan de pagina en plak je token in het veld)
4. Stuur het orders POST request naar de Juice Shop API met de volgende body:
   - `{"orderLinesData": "(function dos() { while(true); })()"}`
5. Gefeliciteerd! Je hebt nu een DoS aanval uitgevoerd op de Juice Shop. Echter, werkt deze opdracht niet, omdat de Juice Shop een ininite loop detectie heeft. Daarom krijg je een 200 OK response terug. De server is getimeout, maar de Juice Shop is nog steeds bereikbaar.

## Opdracht 14: Successvolle DDOS aanval op de Juice Shop

### ASVS:

- **V10.3 | Malicious Code**: Verify that the application protects against malicious code being inserted into the application, such as through code injection, and that the application can detect and respond to such attacks.
- **V12.5.2**: Verify that direct requests to uploaded files will never be executed as HTML/JavaScript content.

### Uitleg:

1. De vorige opdracht werkte niet, omdat de Juice Shop een ininite loop detectie heeft. Daarom gaan we nu de server bezig houden zonder een infinite loop.
2. In de request body vullen we nu in:
   - `{"orderLinesData": "/((a+)+)b/.test('aaaaaaaaaaaaaaaaaaaaaaaaaaaaa')"}`
3. Hierdoor wordt er een erg intensieve regex uitgevoerd op de server. Als het goed is krijg je nu een 503 error terug.
4. Gefeliciteerd! Je hebt nu een succesvolle DDOS aanval uitgevoerd op de Juice Shop.

## Opdracht 15: Laat de server met NoSQL slapen door een NoSQL injection

### ASVS:

- V5.3.4 Verify that data selection or database queries (e.g. SQL, HQL, ORM, NoSQL) use parameterized queries, ORMs, entity frameworks, or are otherwise protected from database injection attacks.

### Opdracht:

1. Maak gebruik van de API om de reviews van het database ID 1 op te halen. (http://localhost:3000/rest/products/1/reviews)
2. Door iets in de URL te veranderen kan je de reviews van een ander product ophalen. (http://localhost:3000/rest/products/2/reviews)
3. Door iets in de URL te veranderen kan je ook de server laten slapen. (http://localhost:3000/rest/products/sleep(2000)/reviews)
4. De Juice Shop is nu (tijdelijk) niet meer bereikbaar. Gefeliciteerd! Je hebt nu een NoSQL injection uitgevoerd op de Juice Shop.

## Opdracht 16: Vind een confidentieel document

### ASVS:

- V12.5 | Files and Resources: Verify that all files and resources are protected from unauthorized access.

### Opdracht:

1. Ga naar de about pagina. (http://localhost:3000/#/about)
2. Klik op de link die verwijst naar de gebruikersvoorwaarden. (http://localhost:3000/#/ftp/legal.md)
3. In de url van de pagina is te zien dat de gebruikersvoorwaarden worden opgehaald vanaf een FTP server.
4. Ga naar de FTP server. (http://localhost:3000/ftp/)
5. Nu is het mogelijk om alle bestanden op de FTP server te bekijken.
6. Open het bestand `acquisitions.md`.
7. Gefeliciteerd! Je hebt nu een confidential document gevonden.

## Opdracht 17: Krijg toegang tot een vergeten backup bestand via een Poison Null Byte

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
10. Gefeliciteerd! Je hebt nu een toegang tot een vergeten backup bestand.
