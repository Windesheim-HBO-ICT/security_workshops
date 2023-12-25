## Opdracht 0: Vind het scoreboard

De student moet zoeken in de JS van de Juice shop, waarbij gezocht wordt naar het woord "score". De student vindt hiermee een URL naar het scoreboard, welke hij/zij moet openen in de webbrowser. Hierna zijn de scores gevonden!

## Opdracht 1: Inloggen als administrator door middel van SQL injection

Door een simpele sql injectie (' or 1=1-- in een input field) kan de student toegang krijgen tot een administrator account. Hier mee wordt verder gewerkt in opdracht 2.

## Opdracht 2: Registreer een administrator account

De student doet nu een request naar de juiceshop API met Postman, met custom headers en body. Als het goed is is er nu een nieuwe admin gebruiker geregistreerd.

## Opdracht 3: Ga naar de admin panel

Nu dat de student een admin account heeft is het tijd om te vinden waar de admin panel verstopt is. Zodra deze gevonden is door in de source code van de juice shop te kijken, kan er worden ingelogd met de nieuwe account

## Opdracht 4: Laat een review van 0 sterren achter

De student gaat naar de contactpagina en maakt de "verstuur" knop actief d.m.v. Javascript. Hierna kan de student een review achterlaten met 0 sterren.

## Opdracht 5: Zet een artikel in de winkelwagen van een andere gebruiker

De student maakt gebruikt van de "Network tab" om te zien hoe de winkelwagen van de gebruiker wordt opgeslagen. Vervolgens wordt postman gebruikt om een request te sturen naar de API om de winkelwagen van een andere gebruiker te veranderen.

## Opdracht 6: DoS aanval op de Juice Shop

De auth token wordt uit de swagger API van de juiceshop gehaald. Vervolgens wordt er een POST request gestuurd naar de API met een oneindige while loop. Nu heeft de student een DoS aanval uitgevoerd op de Juice Shop.
