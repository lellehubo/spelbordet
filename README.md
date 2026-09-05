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
3. Frågekorten läses från den fysiska spelasken — appen håller inga frågor.
   Laget näst på tur läser, som reglerna säger. Appen visar vem det är.
4. Rätt svar: tryck **Rätt** — pjäsen flyttas frågans poängvärde.

## Vad appen sköter

- Kategoribrickor: dras ur en gemensam påse, läggs i poängordning 1–4
- ZWAP: byt två uppåtvända brickor var som helst på bordet
- BEZZERWIZZER: två per omgång, 1- eller 3-poängsattack, alla utfall
- Upploppet: en vunnen attack där kan knuffa försvararen bakåt i stället
- Turordning, rundor och nya givar enligt reglerna
- Delad Spotify Jam-länk

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
