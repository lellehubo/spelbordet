# Spelbordet

Ett gemensamt spelbord för frågespel på distans. Fyra telefoner öppnar samma
länk och hamnar vid samma bord: gemensam spelplan, allas kategoribrickor
synliga, och en egen panel längst ner.

Byggt för att lösa det som inte fungerar över videosamtal — inte pjäserna,
utan **brickplattorna**. Fyra lag lägger fyra kategoribrickor i vald
poängordning, öppet på bordet, och alla måste se dem för att kunna spela
taktiskt. Fyra plattor utspridda i två hushåll är precis vad en videoruta
inte klarar.

## Så spelar man

1. En person öppnar sidan och delar länken (knappen **Dela**).
2. Alla fyra väljer namn och plats.
3. Dra era kategoribrickor som vanligt och lägg in dem på brickan i appen,
   så ser alla varandras.
4. Spela på. Vid rätt svar väljer man antal steg och trycker **Flytta**.

## Vad appen sköter — och inte

Appen kör inte spelet. Ni drar brickorna ur påsen, ställer frågorna,
håller reda på turordningen och bestämmer själva hur många steg ett
svar var värt. Appen visar bara det ni annars inte kan se hos varandra:

- **Brickan** — lägg in de fyra kategorier ni själva drog, i den ordning
  ni valt. Plats 1 är värd 1 poäng, plats 4 är värd 4.
- **Allas brickor** öppet, samtidigt, på varje telefon
- **Pjäserna** på banan — du flyttar din egen, valfritt antal steg
- **Vem som är där** just nu
- En knackning på bordet, och en delad Spotify Jam-länk

ZWAP och BEZZERWIZZER hanterar ni med de fysiska brickorna och rösten,
precis som när ni sitter i samma rum.

## Teknik

En enda HTML-fil, ingen byggprocess. Realtiden går över Supabase Realtime
**broadcast** — presence är avstängt i projektet, så närvaron är en egen
hello/who/bye-heartbeat. Kategoripåsen delas ut från ett frö byggt på
rumskod + rundnummer, så alla klienter räknar fram samma giv utan att
förhandla om den.

Supabase anon-nyckeln ligger i klartext i filen. Det är avsiktligt: den är
publik by design och appen rör inga tabeller, bara broadcast-kanaler.

## Kör lokalt

    python -m http.server 8777

Öppna sedan http://127.0.0.1:8777/index.html
