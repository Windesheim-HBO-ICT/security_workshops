# Juice shop opdrachten

## Opdracht 1: Inloggen als administrator door middel van SQL injection

1. Open de Juice Shop in een webbrowser.
2. Klik op de knop "Login" in de rechterbovenhoek van het scherm.
3. Voer in het veld "E-mailadres" het volgende in: `' or 1=1--`
4. Voer in het veld "Wachtwoord" iets in.
5. Klik op de knop "Login".
6. Gefeliciteerd! Je bent nu ingelogd als administrator.

## Opdracht 2: Registreer een administrator account

1. Open postman.
2. Maak een POST request naar `http://localhost:3000/api/Users`.
3. Voeg de volgende headers toe:
   - `Content-Type: application/json`
4. Voeg de volgende body toe:
   - `{"email":"admin","password":"admin","role":"admin"}`

## Opdracht 3: Ga naar de admin panel

1. Open de Juice Shop in een webbrowser.
2. Open de source code (`main.js`) van de Juice Shop.
3. Zoek naar het woord "path:" in de source code.
4. Nu is het pad naar de admin panel bekend.
5. Open de admin panel in een webbrowser. (http://localhost:3000/#/administration)
6. Gefeliciteerd! Je bent nu in de admin panel.

## Opdracht 4: Laat een review van 0 sterren achter

1. Open de Juice Shop in een webbrowser.
2. Ga naar de contact pagina. (http://localhost:3000/#/contact)
3. Open de developer tools van de webbrowser.
4. Selecteer de verstuur knop.
5. Verwijder het `disabled` attribuut van de verstuur knop.
6. Verstuur het formulier.
7. Gefeliciteerd! Je hebt nu een review van 0 sterren achtergelaten. (Zie de review op about pagina (http://localhost:3000/#/about))

## Opdracht 5: Zet een artikel in de winkelwagen van een andere gebruiker

- Na het eventueel bekijken van de network tab in de developer tools van de webbrowser, is het duidelijk dat de winkelwagen van een gebruiker wordt aangepast door middel van een POST request naar `http://localhost:3000/api/BasketItems`.

1. Open postman.
2. Maak een POST request naar `http://localhost:3000/api/BasketItems`.
3. Voeg de volgende body toe:
   - `{"ProductId":1,"BasketId":1,"quantity":1}`
4. Dit zal niet werken omdat de ingelogde gebruiker niet de gebruiker met id 1 is.
5. Voeg nu nog een keer de property BasketId toe aan de body maar nu met de waarde van het originele request:
   - `{"ProductId":1,"BasketId":1,"quantity":1,"BasketId":"INSERT_ORIGINELE_BASKET_ID_HERE"}`

## Opdracht 6: DoS aanval op de Juice Shop

https://pwning.owasp-juice.shop/companion-guide/latest/appendix/solutions.html#_perform_a_remote_code_execution_that_would_keep_a_less_hardened_application_busy_forever
<!-- not yet working -->

1. Open de swagger documentatie van de Juice Shop API. (http://localhost:3000/api-docs)
2. Haal je auth token op uit de developer tools van de webbrowser.
3. Plak je auth token in de swagger documentatie. (Klik op Authorize rechts bovenaan de pagina en plak je token in het veld)
4. Stuur het orders POST request naar de Juice Shop API met de volgende body:
   - {"orderLinesData": "(function dos() { while(true); })()"}
5. Gefeliciteerd! Je hebt nu een DoS aanval uitgevoerd op de Juice Shop.