# Pracovný tok taskov

Projekt používa špecifikácie a roly agentov na rozdelenie práce do kontrolovateľných etáp. Custom agenti sú uložené v `.github/agents/`; tasky patria do samostatného priečinka `tasks/`. Vytvorenie alebo zmena task súboru agenta vo VS Code automaticky nespúšťa.

## Zásady

- Každá úloha má jeden kanonický súbor `tasks/TASK-YYYYMM-NNN.md`. Počas práce sa nepremiestňuje ani nemení jeho názov.
- Výstupy agentov patria do priečinkov určených ich rolou, napríklad `docs/01-business/` alebo `docs/02-architecture/`.
- Task eviduje stav, stručné zhrnutie každej fázy a relatívne odkazy na jej výstupy; nenahrádza odborné špecifikácie.
- Trvalé špecifikácie si zachovávajú názvy ako `requirements.md` a `system-design.md`. Samostatné výstupy viazané len na jeden task môžu mať názov `TASK-YYYYMM-NNN-<faza>.md`.
- Agenti sa vyberajú a prepínajú ručne. Ďalšia fáza sa začína až po kontrole a výslovnom schválení výstupu používateľom.

## Postup

1. Používateľ vytvorí task zo šablóny `tasks/TASK-YYYYMM-NNN-template.md`, doplní cieľ, rozsah a akceptačné kritériá a určí agenta aj cestu k tasku.
2. Používateľ vyberie agenta príslušnej fázy a v zadaní uvedie cestu k task súboru.
3. Agent vytvorí alebo aktualizuje výstupy vo svojom určenom priečinku. Ak bol task výslovne priradený, aktualizuje iba záznam svojej fázy a odkazy na svoje výstupy v centrálnom tasku.
4. Používateľ skontroluje výstup a sám zaznamená rozhodnutie o schválení. Agent nesmie označiť fázu za schválenú v mene používateľa.
5. Po schválení používateľ ručne vyberie ďalšieho agenta. Task zostáva na pôvodnej ceste a po dokončení všetkých požadovaných fáz sa uzavrie.

## Názvy a citlivé údaje

Číslovanie taskov má tvar `TASK-YYYYMM-NNN`, kde `YYYYMM` je rok a mesiac a `NNN` poradové číslo. Do taskov, výstupov ani testovacích dát nevkladaj reálne osobné alebo zdravotné údaje; používaj syntetické príklady a odkazy na schválené dokumenty.
