# Konkurenčná analýza a produktový koncept

## Hlavní konkurenti a ich obmedzenia

| Produkt | Zameranie | Obmedzenia |
| --- | --- | --- |
| **Fig (Food is Good)** | Nastavenie špecifických diét a alergií | Spolieha sa na postupné skenovanie jednotlivých čiarových kódov; databáza má medzery na lokálnych európskych trhoch. |
| **Soosee** | OCR a zvýraznenie nežiaducich slov priamo na etikete | Analyzuje jeden produkt zblízka a neposkytuje orientáciu v širšom priestore. |
| **Yuka / CodeCheck** | Zdravotné skóre a základné alergény | Neposkytujú hlbokú personalizáciu zriedkavých krížových intolerancií, etické obmedzenia ani AR navigáciu. |
| **Spoon Guru** | AI kategorizácia potravín podľa diét | Funguje predovšetkým ako B2B integrácia do online obchodov a nepomáha priamo pri fyzickom nákupe. |

## Konkurenčné výhody konceptu

- **Plošné AR rozpoznávanie:** počítačové videnie identifikuje viacero produktov v regáli súčasne. Zákazník nemusí brať každý produkt do ruky a skenovať jeho čiarový kód.
- **Sémantická analýza neznámych položiek:** ak produkt nie je v databáze, kamera prečíta zloženie a jazykový model vyhodnotí jeho kontext vrátane skrytých derivátov alergénov a technických názvov E-čok.
- **Kognitívne odbremenenie:** aplikácia vizuálne zvýrazní vhodné produkty a stlmí rizikové, aby používateľ nemusel porovnávať dlhé tabuľky a zoznamy.

## Cieľová skupina

- Ľudia s viacerými intoleranciami, napríklad s kombináciou histamínovej intolerancie a celiakie.
- Rodičia detí s alergiami, ktorí potrebujú rýchlo a bezpečne vyberať potraviny.
- Ľudia s etickými alebo náboženskými stravovacími pravidlami: vegáni a zákazníci hľadajúci halal alebo kóšer produkty vrátane skrytých živočíšnych zložiek.
- Príbuzní a známi, ktorí nakupujú pre človeka so zložitým diétnym profilom a potrebujú používať jeho zdieľané nastavenia.
- Diabetici a ľudia s inzulínovou rezistenciou, ktorí sledujú pridané a skryté cukry, umelé sladidlá a glykemickú záťaž.

## Technologická architektúra

- **Mobilný frontend a AR:** natívne aplikácie pre iOS s ARKit a Android s ARCore na plynulé prekrytie obrazu kamery v reálnom čase.
- **Rozpoznávanie obrazu a OCR:** lokálne modely v zariadení, napríklad ML Kit, na rýchle čítanie textu etikiet s nízkou latenciou.
- **Backend a sémantická analýza:** jazykový model kontextovo analyzuje nejednoznačné zložky a E-čká, najmä pri produktoch, ktoré nie sú v primárnej databáze.
- **Cloud a dáta:** zabezpečená databáza pre zdieľané profily a cloudová infraštruktúra na agregáciu anonymizovaných B2B analytických dát.

## Monetizácia

### Freemium model pre zákazníkov (B2C)

- **Bezplatná verzia:** manuálne skenovanie čiarových kódov a databáza základných alergénov, ako sú lepok, laktóza a orechy. Slúži na získavanie používateľov.
- **Prémiové mesačné alebo ročné predplatné:** plošné AR skenovanie regálov v reálnom čase, zriedkavé krížové intolerancie, AI analýza neznámych zložiek a zdieľané rodinné profily.

### B2B dátová analytika

Agregované a anonymizované dáta o nákupnom správaní a dopyte po špecifických zložkách môžu výrobcom a obchodným reťazcom pomôcť optimalizovať sortiment a vyvíjať nové produkty.

### Affiliate partnerstvá a cielená reklama

Pri integrácii s e-shopmi a výrobcami špeciálnych potravín môže aplikácia ponúknuť odkaz na vhodný certifikovaný produkt online, ak v predajni nenájde vhodnú alternatívu. Nákup môže priniesť aplikácii affiliate províziu.

## Alternatívne produktové prístupy

### No App – AI (agent-first model)

Tento prístup využíva existujúceho multimodálneho asistenta v smartfóne, napríklad ChatGPT, Gemini alebo Apple Intelligence, namiesto samostatnej aplikácie.

**Príležitosti:**

- Odpadá vývoj natívnych aplikácií a vlastného používateľského rozhrania; potenciálna úspora na vývoji MVP je 40 000–70 000 €.
- Používateľ nemusí inštalovať ďalšiu aplikáciu a môže odfotiť regál alebo spustiť video cez svojho asistenta.
- Hotový jazykový model poskytuje kontextové porozumenie neznámym zložkám bez tréningu vlastného modelu.

**Hrozby a obmedzenia:**

- Spracovanie statických fotografií alebo videa má latenciu a neposkytuje stabilné priestorové zvýraznenie desiatok produktov v reálnom čase ako natívny ARKit/ARCore.
- Monetizácia cez vlastné predplatné alebo affiliate odkazy je v platformách cudzích asistentov technicky aj zmluvne obmedzená.
- Produkt závisí od podmienok poskytovateľa AI platformy; zdieľanie citlivých údajov o intoleranciách v otvorených konverzáciách môže vyvolávať obavy o súkromie.

### Progresívna webová aplikácia (PWA) oproti natívnemu vývoju

PWA s WebAR beží v mobilnom prehliadači pod vlastnou doménou, nevyžaduje inštaláciu a obchádza zdĺhavé schvaľovanie v obchodoch s aplikáciami. Mobilné prehliadače však nemajú plný prístup k natívnym modulom ARKit a ARCore, preto môže živé skenovanie mnohých produktov v plynulom videu byť nepresné alebo sekané.

Pre PWA MVP používateľ odfotí regál a aplikácia farebne vyznačí vhodné a rizikové produkty na statickej fotografii. Frontend môže byť postavený napríklad na Reacte alebo Vue s HTML5 a WebRTC pre prístup ku kamere; OCR a sémantická AI analýza prebiehajú prevažne v cloude a vyžadujú internetové pripojenie.

PWA je vhodná na rýchle a lacnejšie overenie trhu. Po potvrdení ochoty zákazníkov platiť za prémiové funkcie je možný prechod na natívnu aplikáciu s plnohodnotným AR. Pri väčšom počte používateľov môžu rásť náklady PWA na cloudové spracovanie fotografií.

## Go-To-Market stratégia pre natívny variant

1. **Mesiace 1–3 – predspustenie a komunita:** vytvoriť landing page na zber e-mailov, osloviť administrátorov komunitných skupín (celiatici, ľudia s histamínovou intoleranciou, vegáni) a spustiť uzavreté beta testovanie pre prvých 500 používateľov.
2. **Mesiace 4–6 – spustenie a akvizícia:** optimalizovať prezentáciu v obchodoch s aplikáciami (ASO) pre výrazy ako „skener alergií“ a „bezlepková diéta“, spolupracovať s mikroinfluencermi a spustiť cielené reklamy na sociálnych sieťach.
3. **Mesiace 7–12 – expanzia a B2B partnerstvá:** nadviazať spoluprácu s lokálnymi reťazcami a e-shopmi so špeciálnymi potravinami, integrovať affiliate odkazy a začať predaj B2B dátovej analytiky.

## Odhad prvotných nákladov a rozpočet

| Fáza | Rozsah | Odhad |
| --- | --- | ---: |
| Vývoj a testovanie MVP | UI/UX, natívny vývoj pre iOS a Android, AR a OCR moduly, integrácia LLM a zabezpečený backend | 40 000–70 000 € |
| Marketing a uvedenie na trh | Výkonnostný marketing, PR pre cieľové komunity a spolupráca s odborníkmi na výživu | 15 000–25 000 € |
| Prevádzkové náklady počas prvého roka | Cloud, API tretích strán, priebežná údržba aplikácie a aktualizácia databáz | 20 000–30 000 € |
| **Spolu: spustenie a prvý rok prevádzky** | | **75 000–125 000 €** |

Samostatný odhad vývoja PWA MVP je 15 000–30 000 €. Nejde o súčasť vyššie uvedeného rozpočtu natívneho variantu. PWA môže znížiť počiatočné náklady na vývoj, jej cloudové prevádzkové náklady však môžu rásť s používaním.
