# Juice shop I opdrachten

## Opdracht 1: Vind het scorebord

### ASVS:

---

### Opdracht:

1. Open de Juice Shop in een webbrowser.
2. Open de source code (`main.js`) van de Juice Shop.
3. Zoek naar het woord "score" in de source code.
4. Nu is het pad naar het scorebord bekend.
5. Open het scorebord in een webbrowser.
6. Gefeliciteerd! Je hebt nu het scorebord gevonden.

## Opdracht 2: Inloggen als administrator door middel van SQL injection

### ASVS:

- **V5.1 | Input Validation**: Verify that security features protecting against SQL Injection are enabled and effective.

### Uitleg:

1. Open de Juice Shop in een webbrowser.
2. Klik op de knop "Login" in de rechterbovenhoek van het scherm.
3. Voer in het veld "E-mailadres" het volgende in: `' or 1=1--`
4. Voer in het veld "Wachtwoord" iets in.
5. Klik op de knop "Login".
6. Gefeliciteerd! Je bent nu ingelogd als administrator.

## Opdracht 3: Registreer een administrator account

### ASVS:

- **V13.2 | API and Web Service**: The request and response data structures should be designed to be as simple as possible to reduce the likelihood of input validation bypasses and output encoding mistakes.

1. Open postman.
2. Maak een POST request naar `http://localhost:3000/api/Users`.
3. Voeg de volgende headers toe:
   - `Content-Type: application/json`
4. Voeg de volgende body toe:
   - `{"email":"admin","password":"admin","role":"admin"}`

## Opdracht 4: Ga naar de admin panel

### ASVS:

- **V4.1 | Access Control**: Verify that access controls are contextually appropriate, and that the authenticated user is authorized to access the requested functionality.

### Uitleg:

1. Open de Juice Shop in een webbrowser.
2. Open de source code (`main.js`) van de Juice Shop.
3. Zoek naar het woord "path:" in de source code.
4. Nu is het pad naar de admin panel bekend.
5. Open de admin panel in een webbrowser. (http://localhost:3000/#/administration)
6. Gefeliciteerd! Je bent nu in de admin panel.

## Opdracht 5: Bekijk iemand anders zijn winkelwagen

### ASVS:

- V4.1 | Access Control: Verify that access controls are contextually appropriate, and that the authenticated user is authorized to access the requested functionality.

### Opdracht:

> Deze opdracht is leuk om te doen in combinatie met een 2e account met items in de winkelwagen.

1. Log in als een gebruiker.
2. Voeg een product toe aan je winkelwagen.
3. Ga naar de winkelwagen pagina. (http://localhost:3000/#/basket)
4. Open de developer tools van de webbrowser.
5. In chrome: Ga naar het application tab. In firefox: Ga naar de storage tab.
6. Open de session storage van de Juice Shop.
7. Hier is te zien dat de winkelwagen van de gebruiker wordt opgeslagen in de session storage, door middel van een `bid` (Basket ID).
8. Verander de `bid` naar een ander getal.
9. Herlaad de pagina.
10. Gefeliciteerd! Je hebt nu iemand anders zijn winkelwagen bekeken.

## Opdracht 6: Zet een artikel in de winkelwagen van een andere gebruiker

### ASVS:

- **V4.1 | Access control**: Verify that all user and data attributes and policy information used by access controls cannot be manipulated by end users unless specifically authorized.

### Uitleg:

> Na het eventueel bekijken van de network tab in de developer tools van de webbrowser, is het duidelijk dat de winkelwagen van een gebruiker wordt aangepast door middel van een POST request naar `http://localhost:3000/api/BasketItems`.

1. Open postman.
2. Kopieer je bearer token vanuit de Juice Shop. Deze kun je vinden in de header van het toevoegen aan de basket request. Ook is deze te vinden in je local storage.
3. Voeg dit token toe als bearer token in het authentication tabje in postman.
4. Maak een POST request naar `http://localhost:3000/api/BasketItems`.
5. Voeg de volgende body toe:
   - `{"ProductId":1,"BasketId":1,"quantity":1}`
6. Dit zal niet werken omdat de ingelogde gebruiker niet de gebruiker met id 1 is.
7. Voeg nu nog een keer de property BasketId toe aan de body maar nu met de waarde van het originele request:
   - `{"ProductId":1,"BasketId":1,"quantity":1,"BasketId":"INSERT_ORIGINAL_BASKET_ID_HERE"}`
