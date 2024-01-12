# Juice Shop II opdrachten

## Opdracht 7: Laat een review van 0 sterren achter

### ASVS:

- **V4.1 | Access Control**: Verify that the application enforces access control rules on a trusted service layer, especially if client-side access control is present and could be bypassed.

### Uitleg:

1. Open de Juice Shop in een webbrowser.
2. Ga naar de contact pagina. (http://localhost:3000/#/contact)
3. Open de developer tools van de webbrowser.
4. Selecteer de verstuur knop.
5. Verwijder het `disabled` attribuut van de verstuur knop.
6. Verstuur het formulier.
7. Gefeliciteerd! Je hebt nu een review van 0 sterren achtergelaten. (Zie de review op about pagina (http://localhost:3000/#/about))

## Opdracht 8: Veroorzaak een error die niet goed wordt afgehandeld en verkrijg informatie over de database

### ASVS:

- V7.3.3 Verify that security logs are protected from unauthorized access and modification.
- V7.4.1 Verify that a generic message is shown when an unexpected or security sensitive error occurs, potentially with a unique ID which support personnel can use to investigate.

### Opdracht:

Dit is maar een van de vele manieren om een error te veroorzaken. Er zijn er nog veel meer, welke allemaal een slechte afhandeling hebben.

1. Ga naar de Juice Shop login pagina. (http://localhost:3000/#/login)
2. Vul een "`'`" in bij het email adres en een willekeurig wachtwoord. Hierbij probeer je een SQL error te veroorzaken.
3. De Juice Shop geeft nu een error terug met een SQL query.
4. In de error is de query `SELECT \* FROM Users WHERE email = ''' AND password = '5ff798c672bc0c029edcdc699231dc9f' AND deletedAt IS NULL` te vinden.
5. Hierdoor kan je informatie krijgen over de database die de Juice Shop gebruikt.

## Opdracht 9: XSS aanval op de Juice Shop

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

## Opdracht 10: Voer een DOM XSS aanval uit op de Juice Shop

### ASVS:

- V5.3 Validation, Sanitization and Encoding: Verify that all user-controllable input is validated, sanitized and encoded.

### Opdracht:

1. Open het zoekveld van de Juice Shop. (Rechts bovenaan de pagina)
2. Voer de volgende payload in in het zoekveld:

```
<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/771984076&color=%23ff5500&auto_play=true&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>
```

3. Gefeliciteerd! Je hebt nu een DOM XSS aanval uitgevoerd op de Juice Shop.

## Opdracht 11: Maak een ongeldige JWT token

### ASVS:

- V3.2 | Session Management: Verify that session tokens are generated using approved cryptographic algorithms.

### Opdracht:

1. Log in als een gebruiker
2. Open het netwerk tab van de developer tools
3. Kopieer de JWT uit de `Authorization` header (Alles na `Bearer`)
4. Ga naar [https://jwt.io](https://jwt.io) en plak de JWT in het `encoded` veld
5. Verander het e-mail van de token
6. Verander het algoritme (`alg` in de header) van `HS256` naar `None`
7. Encode de `header` en `payload` naar `Base64url`
8. Voeg de `header` en `payload` samen met een `.` ertussen
9. Voeg een `.` toe aan het einde van de string
10. Verander je cookie `token` naar de nieuwe JWT token
11. Gefeliciteerd! Je hebt nu een ongeldige JWT token gemaakt

## Opdracht 12: Laat 10 reviews achter in minder dan 10 seconden

### ASVS:

- V2.2 | Authentication: Verify that anti-automation controls are effective at mitigating breached credential testing, brute force, and account lockout attacks. Such controls include blocking the most common breached passwords, soft lockouts, rate limiting, CAPTCHA, ever increasing delays between attempts, IP address restrictions, or risk-based restrictions such as location, first login on a device, recent attempts to unlock the account, or similar. Verify that no more than 100 failed attempts per hour is possible on a single account.

### Opdracht:

https://github.com/bmanning1/captchaRequests/
