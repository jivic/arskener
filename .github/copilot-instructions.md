# Pokyny pre GitHub Copilot

Tento repozitár obsahuje špecifikácie a vývojový plán AR skenera potravín. Nejde o XTB ani investičný projekt.

## Pracovný postup

- Pred zmenou si prečítaj relevantné schválené dokumenty a dodrž rolu zvoleného custom agenta.
- Pracuj iba v rozsahu danej úlohy. Jedinou výnimkou mimo výstupného priečinka roly je aktualizácia vlastnej fázy v tickete, ktorý používateľ výslovne priradil; iné zmeny mimo rozsahu najprv vysvetli a vyžiadaj si súhlas.
- Schválenie výstupu jednej etapy je potrebné pred pokračovaním ďalšou rolou. VS Code agenti sa vyberajú a prepínajú podľa potreby; tento súbor nevytvára automatický workflow.
- Pre úlohu používaj jeden centrálny súbor `tasks/TASK-YYYYMM-NNN.md`; nikdy ho medzi agentmi nepremiestňuj ani nepremenúvaj.
- Aktualizuj iba vlastnú fázu tasku výslovne priradeného používateľom: stav práce, stručné zhrnutie a odkazy na svoje výstupy. Pole schválenia mení iba používateľ.
- Trvalé špecifikácie udržiavaj pod kanonickými názvami; jednorazové výstupy viazané na task pomenuj `TASK-YYYYMM-NNN-<faza>.md`.
- Vytvorenie alebo zmena task súboru agenta automaticky nespúšťa. Nevymýšľaj chýbajúce tickety ani priečinky.
- Git commit alebo push vykonaj iba na výslovnú požiadavku používateľa.
- Rozsah zápisu v agentových pokynoch je pracovné pravidlo, nie technická izolácia súborov. Neprezentuj ho ako sandbox alebo oprávnenie vynútené VS Code.

## Bezpečnosť produktu

- Produkt pracuje s diétnymi a potenciálne citlivými zdravotnými údajmi. Minimalizuj ich zber a nevkladaj reálne osobné údaje do testovacích dát.
- OCR ani AI vyhodnotenie nepovažuj za záruku bezpečnosti potraviny. Pri neúplných alebo neistých údajoch zachovaj upozornenie na neistotu a odporuč kontrolu etikety.
- Pri návrhoch spracovania profilov, fotografií a analytiky zohľadni súhlas, ochranu údajov, bezpečné ukladanie a anonymizáciu.
