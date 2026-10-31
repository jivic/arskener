# AR Skener

Systém pre AR skenovanie a analýzu potravín podľa diétnych potrieb používateľa, vyvíjaný na základe schválených špecifikácií (**Spec-Driven & Multi-Agent Development**).

## 1. Koncepcia projektu a riadenie agentov

Projekt funguje na princípe **Spec-Driven Development** (vývoj riadený špecifikáciami) a práce rozdelenej medzi špecializované roly. V VS Code používateľ vyberá agenta podľa fázy a pred pokračovaním do ďalšej fázy schvaľuje výstup. Žiaden kód v produkčnom priečinku `src/` sa nevytvára bez predchádzajúceho definovania a schválenia požiadaviek v príslušných špecifikačných vrstvách.

Celý životný cyklus je rozdelený medzi špecializované roly agentov:

| Fáza | Agent / Rola | Vstup (Číta) | Výstup (Zapisuje) | Brána (Approval Gate) |
| :--- | :--- | :--- | :--- | :--- |
| **1. Biznis** | **Business Analyst** | Zadanie od používateľa | `docs/01-business/` | Schválenie biznis logiky a cieľov |
| **2. Architektúra** | **System Architect** | `docs/01-business/` | `docs/02-architecture/` | Schválenie systémového návrhu a ADR |
| **3. Bezpečnosť** | **Security Officer** | `docs/01-business/`, `docs/02-architecture/` | `docs/04-security/` | Schválenie bezpečnostných pravidiel a limitov |
| **4. Technický dizajn** | **Tech Lead** | `docs/01-business/`, `docs/02-architecture/`, `docs/04-security/` | `docs/03-technical/` | Schválenie technického rozpadu a rozhraní |
| **5. Vývoj** | **Software Engineer** | Všetky `docs/` | `src/` | Code review a súlad so špecifikáciou |
| **6. QA & Testy** | **QA Engineer** | `docs/`, `src/` | `tests/` | Úspešné zbehnutie testov a reporty |
| **7. Nasadenie** | **DevOps Engineer** | `src/`, `tests/` | `deploy/` | Konfigurácia kontajnerov a CI/CD |
| **8. Portál & Príručky** | **Technical Writer** | Všetky `docs/`, `src/` | `mkdocs.yml`, príručky | Schválenie portálu a publikovanie |

## 2. Štruktúra repozitára

```text
ARSkener/
├── .github/                       # Inštrukcie a konfigurácia pre GitHub Copilot vo VS Code
│   ├── agents/                    # Workspace custom agents
│   │   ├── business-analyst.agent.md
│   │   ├── system-architect.agent.md
│   │   ├── security-officer.agent.md
│   │   ├── tech-lead.agent.md
│   │   ├── software-engineer.agent.md
│   │   ├── qa-engineer.agent.md
│   │   ├── devops-engineer.agent.md
│   │   └── technical-writer.agent.md
│   └── copilot-instructions.md    # Spoločné pravidlá projektu
│
├── tasks/                         # Voliteľné tickety pre konkrétne úlohy
│   └── TASK-xxx.md                # Zakladá sa iba pre dohodnutú úlohu
│
├── docs/                          # ŠPECIFIKÁCIE & DOKUMENTÁCIA (Pre MkDocs)
│   ├── 01-business/               # Agent: Business Analyst
│   │   ├── competitive-analysis.md # Konkurenčná analýza a produktový koncept
│   │   ├── requirements.md        # Funkčné a nefunkčné požiadavky
│   │   ├── domain-glossary.md     # Slovník pojmov (potraviny, alergény, intolerancie...)
│   │   └── acceptance-criteria.md # Kritérium akceptácie (Definition of Done)
│   │
│   ├── 02-architecture/           # Agent: System Architect
│   │   ├── adr/                   # Architecture Decision Records
│   │   ├── system-design.md       # Blokové schémy, dátové toky, komponenty
│   │   └── data-model.md          # Návrh schémy dát a stavový diagram
│   │
│   ├── 03-technical/              # Agent: Tech Lead / Designer
│   │   ├── api-specs.md           # Interné rozhrania a integrácie
│   │   ├── coding-standards.md    # Konvencie kódu, typovanie, ošetrenie chýb
│   │   └── module-breakdown.md    # Detailný rozpad na moduly a balíčky
│   │
│   └── 04-security/               # Agent: Security Officer
│       ├── threat-model.md        # Analýza rizík (citlivé profily, strata spojenia...)
│       ├── secret-management.md   # Správa hesiel, tokenov, súborov .env
│       └── rate-limits-audit.md   # Ochrana pred zneužitím API, auditné logy
│
├── src/                           # KÓD APLIKÁCIE (Agent: Software Engineer)
│   ├── core/                      # Základná biznis logika
│   ├── product_recognition/       # Rozpoznávanie produktov a OCR
│   ├── storage/                   # Perzistencia dát (DB / súbory)
│   ├── notifications/             # Notifikácie
│   └── main.py (alebo index.ts)   # Vstupný bod aplikácie
│
├── tests/                         # TESTY (Agent: QA Engineer)
│   ├── unit/                      # Jednotkové testy komponentov
│   ├── integration/               # Integračné testy
│   ├── fixtures/                  # Testovacie dáta a vzorové odpovede
│   └── reports/                   # Výstupy a správy z testovania
│
├── deploy/                        # DEPLOYMENT & INFRAŠTRUKTÚRA (Agent: DevOps Engineer)
│   ├── docker/                    # Dockerfile, docker-compose.yml
│   ├── systemd/                   # Služby pre beh na pozadí
│   ├── ci-cd/                     # Automatizované pipelines
│   └── env.example                # Vzorový konfiguračný súbor bez tajných údajov
│
├── .gitignore                     # Ignorované súbory
├── .markdownlint.json             # Pravidlá formátovania dokumentácie
├── mkdocs.yml                     # Konfigurácia dokumentačného portálu
└── README.md                      # Hlavný rozcestník projektu
```

## 3. Pravidlá vývoja (Agent Governance Rules)

1. **Zákaz nešpecifikovaného kódu:** Žiadny modul v `src/` nesmie byť vytvorený skôr, ako má zodpovedajúcu schválenú špecifikáciu v `docs/`.
2. **Izolácia zápisov:** Každý agent modifikuje výhradne svoje pridelené adresáre.
3. **Odovzdanie medzi rolami:** Agenti pracujú po etapách; ďalšia rola pokračuje až po schválení výstupu používateľom. Ticket v `tasks/` sa aktualizuje iba vtedy, ak pre úlohu existuje.
4. **Git operácie:** Agent nevykonáva commit ani push bez výslovnej požiadavky používateľa.
5. **Definition of Done (DoD):** Každá úloha musí spĺňať:
   - Schválenú biznis špecifikáciu (`docs/01-business/`).
   - Architektonické a bezpečnostné posúdenie (`docs/02-architecture/`, `docs/04-security/`).
   - Implementáciu podľa technického dizajnu (`src/`, `docs/03-technical/`).
   - Pokrytie testami (`tests/`).
   - Dokumentáciu k nasadeniu (`deploy/`).
