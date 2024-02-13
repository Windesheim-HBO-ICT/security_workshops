# Juice Shop I opdrachten

## Opdracht 1: Vind het scorebord

### ASVS

- Startopdracht, geen ASVS-item

### Opdracht

1. Open de Juice Shop in een webbrowser.
2. Open de source code (`main.js`) van de Juice Shop.
3. Zoek naar het woord "score" in de source code.
4. Nu is het pad naar het scorebord bekend.
5. Open het scorebord in een webbrowser.
6. Gefeliciteerd! Je hebt nu het scorebord gevonden.

## Opdracht 2: Inloggen als administrator door middel van SQL injection

### ASVS

- **V5.1 | Input Validation**: Verify that security features protecting against SQL Injection are enabled and effective. [ASVS for dummies V5.3.4](https://asvs-for-dummies.pages.dev/item/V5_3_4)

### Uitleg

1. Open de Juice Shop in een webbrowser.
2. Klik op de knop "Login" in de rechterbovenhoek van het scherm.
3. Voer in het veld "E-mailadres" het volgende in: `' or 1=1--`
4. Voer in het veld "Wachtwoord" iets in.
5. Klik op de knop "Login".
6. Gefeliciteerd! Je bent nu ingelogd als administrator.

## Opdracht 3: Registreer een administrator account

### ASVS

- **V13.2 | API and Web Service**: The request and response data structures should be designed to be as simple as possible to reduce the likelihood of input validation bypasses and output encoding mistakes. [ASVS for dummies V13.1.1](https://asvs-for-dummies.pages.dev/item/V13_1_1)

1. Open postman.
2. Maak een POST request naar `http://localhost:3000/api/Users`.
3. Voeg de volgende headers toe:
   - `Content-Type: application/json`
4. Voeg de volgende body toe:
   - `{"email":"admin","password":"admin","role":"admin"}`

## Opdracht 4: Ga naar de admin panel

### ASVS

- **V4.1 | Access Control**: Verify that access controls are contextually appropriate, and that the authenticated user is authorized to access the requested functionality. [ASVS for dummies V4.1.3](https://asvs-for-dummies.pages.dev/item/V4_1_3)

### Uitleg

1. Open de Juice Shop in een webbrowser.
2. Open de source code (`main.js`) van de Juice Shop.
3. Zoek naar het woord "path:" in de source code.
4. Nu is het pad naar de admin panel bekend.
5. Open de admin panel in een webbrowser. (<http://localhost:3000/#/administration>)
6. Gefeliciteerd! Je bent nu in de admin panel.

## Opdracht 5: Bekijk iemand anders zijn winkelwagen

### ASVS

- V4.1 | Access Control: Verify that access controls are contextually appropriate, and that the authenticated user is authorized to access the requested functionality. [ASVS for dummies V4.1.3](https://asvs-for-dummies.pages.dev/item/V4_1_3)

### Opdracht

> Deze opdracht is leuk om te doen in combinatie met een 2e account met items in de winkelwagen.

1. Log in als een gebruiker.
2. Voeg een product toe aan je winkelwagen.
3. Ga naar de winkelwagen pagina. (<http://localhost:3000/#/basket>)
4. Open de developer tools van de webbrowser.
5. In chrome: Ga naar het application tab. In firefox: Ga naar de storage tab.
6. Open de session storage van de Juice Shop.
7. Hier is te zien dat de winkelwagen van de gebruiker wordt opgeslagen in de session storage, door middel van een `bid` (Basket ID).
8. Verander de `bid` naar een ander getal.
9. Herlaad de pagina.
10. Gefeliciteerd! Je hebt nu iemand anders zijn winkelwagen bekeken.

## Opdracht 6: Zet een artikel in de winkelwagen van een andere gebruiker

### ASVS

- **V4.1 | Access control**: Verify that all user and data attributes and policy information used by access controls cannot be manipulated by end users unless specifically authorized. [ASVS for dummies V4.1.2](https://asvs-for-dummies.pages.dev/item/V4_1_2)

### Opdracht

> Na het eventueel bekijken van de network tab in de developer tools van de webbrowser, is het duidelijk dat de winkelwagen van een gebruiker wordt aangepast door middel van een POST request naar `http://localhost:3000/api/BasketItems`.

Zorg ervoor dat je ingelogd bent met een gebruiker die niet de admin-gebruiker is.

1. Open postman.
2. Kopieer je bearer token vanuit de Juice Shop. Deze kun je vinden in de header van het toevoegen aan de basket request. Ook is deze te vinden in je local storage.
3. Voeg dit token toe als bearer token in het authentication tabje in postman.
4. Maak een POST request naar `http://localhost:3000/api/BasketItems`.
5. Voeg de volgende body toe:
   - `{"ProductId":1,"BasketId":1,"quantity":1}`
6. Dit zal niet werken omdat de ingelogde gebruiker niet de gebruiker met id 1 is.
7. Voeg nu nog een keer de property BasketId toe aan de body maar nu met de waarde van het originele request:
   - `{"ProductId":1,"BasketId":1,"quantity":1,"BasketId":"INSERT_ORIGINAL_BASKET_ID_HERE"}`

## Opdracht 7: Laat een review van 0 sterren achter

### ASVS

- **V4.1 | Access Control**: Verify that the application enforces access control rules on a trusted service layer, especially if client-side access control is present and could be bypassed. [ASVS for dummies V4.1.1](https://asvs-for-dummies.pages.dev/item/V4_1_1)

### Opdracht

1. Open de Juice Shop in een webbrowser.
2. Ga naar de contact pagina. (<http://localhost:3000/#/contact>)
3. Open de developer tools van de webbrowser.
4. Selecteer de verstuur knop.
5. Verwijder het `disabled` attribuut van de verstuur knop.
6. Verstuur het formulier.
7. Gefeliciteerd! Je hebt nu een review van 0 sterren achtergelaten. (Zie de review op about pagina (<http://localhost:3000/#/about>))

## Opdracht 8: Veroorzaak een error die niet goed wordt afgehandeld en verkrijg informatie over de database

### ASVS

- V7.3.3 Verify that security logs are protected from unauthorized access and modification.
[ASVS for dummies V7.3.3](https://asvs-for-dummies.pages.dev/item/V7_3_3)
- V7.4.1 Verify that a generic message is shown when an unexpected or security sensitive error occurs, potentially with a unique ID which support personnel can use to investigate.
[ASVS for dummies V7.4.1](https://asvs-for-dummies.pages.dev/item/V7_4_1)

### Opdracht

Dit is maar een van de vele manieren om een error te veroorzaken. Er zijn er nog veel meer, welke allemaal een slechte afhandeling hebben.

1. Ga naar de Juice Shop login pagina. (<http://localhost:3000/#/login>)
2. Vul een "`'`" in bij het email adres en een willekeurig wachtwoord. Hierbij probeer je een SQL error te veroorzaken.
3. Open het network tabje in je devtools voordat je op login drukt. Hier kun je straks de SQL-query vinden.
4. De Juice Shop geeft nu een error terug met een SQL query. Deze vindt je terug in de response van dit request. In de error is de query `SELECT \* FROM Users WHERE email = ''' AND password = '5ff798c672bc0c029edcdc699231dc9f' AND deletedAt IS NULL` te vinden.
5. Hierdoor kan je informatie krijgen over de database die de Juice Shop gebruikt.

## Opdracht 9: XSS aanval op de Juice Shop

### ASVS

- V5.3 Validation, Sanitization and Encoding: Verify that all user-controllable input is validated, sanitized and encoded. [ASVS for dummies V5.1.3](https://asvs-for-dummies.pages.dev/item/V5_1_3)

### Opdracht

1. Log in als een gebruiker.
2. Open de order history pagina. (<http://localhost:3000/#/order-history>)
3. Klik op de "Vrachtauto" knop om een bestelling te traceren. (<http://localhost:3000/#/track-order>)
4. In de url van de pagina staat het order id. (<http://localhost:3000/#/track-result?id=ORDER_ID>)
5. Dit order id kan gebruikt worden om een XSS aanval uit te voeren omdat deze rechtstreeks op de pagina wordt getoond.
6. Voer de volgende payload in in het order id veld:

```HTML
<iframe src="javascript:alert(`xss`)">
```

De totaal-URL wordt hiermee: <http://localhost:3000/#/track-result?id=%3Ciframe%20src%3D%22javascript:alert(%60xss%60)%22%3E>

7. Gefeliciteerd! Je hebt nu een XSS aanval uitgevoerd op de Juice Shop.
