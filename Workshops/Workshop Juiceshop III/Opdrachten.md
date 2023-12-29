# Juice shop III opdrachten

## Opdracht 13: XSS aanval op de Juice Shop

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

## Opdracht 14: Voer een DOM XSS aanval uit op de Juice Shop

### ASVS:

### Opdracht:

```
<iframe src="javascript:alert(`xss`)">
```

3. Gefeliciteerd! Je hebt nu een DOM XSS aanval uitgevoerd op de Juice Shop.
