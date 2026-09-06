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
- **Videon** — alla fyra i bild, i stort sett hela skärmen. Det är
  huvudupplevelsen; spelet fälls fram när ni vill se det.
- **Vem som är där** just nu
- En knackning på bordet, och en delad Spotify Jam-länk

ZWAP och BEZZERWIZZER hanterar ni med de fysiska brickorna och rösten,
precis som när ni sitter i samma rum.

## Som vid ett bord

Ni tittar på varandra, och ner på brädet när ni vill. Så är appen byggd:

- **Ansiktena fyller skärmen.** Det är utgångsläget och det enda läget
  som behöver något aktivt för att lämnas.
- **Din bricka ligger framför dig** — de fyra kategorierna syns längst
  ner hela tiden, utan att du öppnar något. Som brickan på bordet.
- **Sänk blicken** genom att dra upp bladet, eller trycka på greppet.
  Där ligger allas plattor, kontrollerna och vägen till banan.
- **Titta upp igen** genom att dra ner, eller bara röra ansiktena.
  Videon har legat kvar bakom hela tiden.

Banan öppnas i sin tur som ett eget lager, för de gånger ni verkligen
vill se pjäserna mot varandra.

## Videon

Daily.co, ett fast rum inbäddat i en iframe.

Rummet är `https://lellehubo.daily.co/Sportboll`, satt i `DAILY_ROOM`
högst upp i skriptet. Det måste vara **Public** i Dailys panel — ett
privat rum med knocking kräver att ägaren är inne och släpper in var och
en. Ett annat rum kan testas med `?video=https://…daily.co/rummet`.

Namnet skrivs i Dailys egen förhandsruta (Prebuilt läser inte `userName`
ur URL:en). Samma ruta är stället att stänga av mikrofonen på — vilket
den ena av två telefoner i samma rum måste göra, annars blir det
rundgång.

Låg först på meet.jit.si, men den publika instansen sätter
`disableIframeAPI: true` och **kastar ut inbäddade samtal efter fem
minuter**, plus att den kräver inloggat konto för att skapa rum. Ett
parti på 45 minuter gick alltså inte att genomföra.

Egen WebRTC valdes bort tidigare: fyra telefoner i två hushåll behöver
ofta en TURN-server för att alls koppla upp, och det felet dyker upp
precis när ni satt er för att spela.

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
