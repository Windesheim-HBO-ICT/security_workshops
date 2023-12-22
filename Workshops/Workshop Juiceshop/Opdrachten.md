# Juice shop opdrachten

## Opdracht 0: Vind het scorebord

### ASVS:

---

### Opdracht:

1. Open de Juice Shop in een webbrowser.
2. Open de source code (`main.js`) van de Juice Shop.
3. Zoek naar het woord "score" in de source code.
4. Nu is het pad naar het scorebord bekend.
5. Open het scorebord in een webbrowser.
6. Gefeliciteerd! Je hebt nu het scorebord gevonden.

## Opdracht 1: Inloggen als administrator door middel van SQL injection

### ASVS:

- **V5.1 | Input Validation**: Verify that security features protecting against SQL Injection are enabled and effective.

### Uitleg:

1. Open de Juice Shop in een webbrowser.
2. Klik op de knop "Login" in de rechterbovenhoek van het scherm.
3. Voer in het veld "E-mailadres" het volgende in: `' or 1=1--`
4. Voer in het veld "Wachtwoord" iets in.
5. Klik op de knop "Login".
6. Gefeliciteerd! Je bent nu ingelogd als administrator.

## Opdracht 2: Registreer een administrator account

### ASVS:

- **V13.2 | API and Web Service**: The request and response data structures should be designed to be as simple as possible to reduce the likelihood of input validation bypasses and output encoding mistakes.

1. Open postman.
2. Maak een POST request naar `http://localhost:3000/api/Users`.
3. Voeg de volgende headers toe:
   - `Content-Type: application/json`
4. Voeg de volgende body toe:
   - `{"email":"admin","password":"admin","role":"admin"}`

## Opdracht 3: Ga naar de admin panel

### ASVS:

- **V4.1 | Access Control**: Verify that access controls are contextually appropriate, and that the authenticated user is authorized to access the requested functionality.

### Uitleg:

1. Open de Juice Shop in een webbrowser.
2. Open de source code (`main.js`) van de Juice Shop.
3. Zoek naar het woord "path:" in de source code.
4. Nu is het pad naar de admin panel bekend.
5. Open de admin panel in een webbrowser. (http://localhost:3000/#/administration)
6. Gefeliciteerd! Je bent nu in de admin panel.

## Opdracht 4: Laat een review van 0 sterren achter

### ASVS:

-  **V4.1 | Access Control**: Verify that the application enforces access control rules on a trusted service layer, especially if client-side access control is present and could be bypassed.

### Uitleg:

1. Open de Juice Shop in een webbrowser.
2. Ga naar de contact pagina. (http://localhost:3000/#/contact)
3. Open de developer tools van de webbrowser.
4. Selecteer de verstuur knop.
5. Verwijder het `disabled` attribuut van de verstuur knop.
6. Verstuur het formulier.
7. Gefeliciteerd! Je hebt nu een review van 0 sterren achtergelaten. (Zie de review op about pagina (http://localhost:3000/#/about))

## Opdracht 5: Zet een artikel in de winkelwagen van een andere gebruiker

### ASVS:

- **V4.1 | Access control**: Verify that all user and data attributes and policy information used by access controls cannot be manipulated by end users unless specifically authorized.

### Uitleg:

> Na het eventueel bekijken van de network tab in de developer tools van de webbrowser, is het duidelijk dat de winkelwagen van een gebruiker wordt aangepast door middel van een POST request naar `http://localhost:3000/api/BasketItems`.

1. Open postman.
2. Maak een POST request naar `http://localhost:3000/api/BasketItems`.
3. Voeg de volgende body toe:
   - `{"ProductId":1,"BasketId":1,"quantity":1}`
4. Dit zal niet werken omdat de ingelogde gebruiker niet de gebruiker met id 1 is.
5. Voeg nu nog een keer de property BasketId toe aan de body maar nu met de waarde van het originele request:
   - `{"ProductId":1,"BasketId":1,"quantity":1,"BasketId":"INSERT_ORIGINAL_BASKET_ID_HERE"}`

## Opdracht 6: DoS aanval op de Juice Shop

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
5. Gefeliciteerd! Je hebt nu een DoS aanval uitgevoerd op de Juice Shop.

## Opdracht 7: XSS aanval op de Juice Shop

### ASVS:

- V5.3 Validation, Sanitization and Encoding: Verify that all user-controllable input is validated, sanitized and encoded.

### Opdracht:

1. Log in als een gebruiker.
2. Open de order history pagina. (http://localhost:3000/#/order-history)
3. Klik op de "Vrachtauto" knop om een bestelling te traceren. (http://localhost:3000/#/track-order)
4. In de url van de pagina staat het order id. (http://localhost:3000/#/track-result?id=ORDER_ID)
5. Dit order id kan gebruikt worden om een XSS aanval uit te voeren omdat deze rechtstreeks op de pagina wordt getoond.
6. Voer de volgende payload in in het order id veld:

```
<iframe src="javascript:alert(`xss`)">
```

7. Gefeliciteerd! Je hebt nu een XSS aanval uitgevoerd op de Juice Shop.

## Opdracht 8: Voer een DOM XSS aanval uit op de Juice Shop

### ASVS:

- V5.3 Validation, Sanitization and Encoding: Verify that all user-controllable input is validated, sanitized and encoded.

### Opdracht:

1. Open het zoekveld van de Juice Shop. (Rechts bovenaan de pagina)
2. Voer de volgende payload in in het zoekveld:

```
<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>
```

3. Gefeliciteerd! Je hebt nu een DOM XSS aanval uitgevoerd op de Juice Shop.


## Opdracht 9: Vind een confidential document

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


## Opdracht 10: Bekijk iemand anders zijn winkelwagen

### ASVS:

- V4.1 | Access Control: Verify that access controls are contextually appropriate, and that the authenticated user is authorized to access the requested functionality.

### Opdracht:

> Deze opdracht is leuk om te doen in combinatie met een 2e account met items in de winkelwagen.

1. Log in als een gebruiker.
2. Voeg een product toe aan je winkelwagen.
3. Ga naar de winkelwagen pagina. (http://localhost:3000/#/basket)
4. Open de developer tools van de webbrowser.
5. Ga naar het application tab.
6. Open de session storage van de Juice Shop.
7. Hier is te zien dat de winkelwagen van de gebruiker wordt opgeslagen in de session storage, door middel van een `bid` (Basket ID).
8. Verander de `bid` naar een ander getal.
9. Herlaad de pagina.
10. Gefeliciteerd! Je hebt nu iemand anders zijn winkelwagen bekeken.


