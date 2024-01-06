# Juice shop II opdrachten

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

## Opdracht 9: Vind een confidentieel document

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

## Opdracht 11: Bekijk een