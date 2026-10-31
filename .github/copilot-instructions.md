# Pokyny pre GitHub Copilot

Tento repozitár obsahuje špecifikácie a vývojový plán AR skenera potravín. Nejde o XTB ani investičný projekt.

## Pracovný postup

- Pred zmenou si prečítaj relevantné schválené dokumenty a dodrž rolu zvoleného custom agenta.
- Pracuj iba v rozsahu danej úlohy. Ak je potrebná zmena mimo výstupného priečinka roly, najprv vysvetli dôvod a vyžiadaj si súhlas.
- Schválenie výstupu jednej etapy je potrebné pred pokračovaním ďalšou rolou. VS Code agenti sa vyberajú a prepínajú podľa potreby; tento súbor nevytvára automatický workflow.
- Ticket v `tasks/` aktualizuj iba vtedy, ak existuje a používateľ ho priradil k úlohe. Nevymýšľaj chýbajúce tickety ani priečinky.
- Git commit alebo push vykonaj iba na výslovnú požiadavku používateľa.
- Rozsah zápisu v agentových pokynoch je pracovné pravidlo, nie technická izolácia súborov. Neprezentuj ho ako sandbox alebo oprávnenie vynútené VS Code.

## Bezpečnosť produktu

- Produkt pracuje s diétnymi a potenciálne citlivými zdravotnými údajmi. Minimalizuj ich zber a nevkladaj reálne osobné údaje do testovacích dát.
- OCR ani AI vyhodnotenie nepovažuj za záruku bezpečnosti potraviny. Pri neúplných alebo neistých údajoch zachovaj upozornenie na neistotu a odporuč kontrolu etikety.
- Pri návrhoch spracovania profilov, fotografií a analytiky zohľadni súhlas, ochranu údajov, bezpečné ukladanie a anonymizáciu.
