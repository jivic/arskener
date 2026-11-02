# Šablóna projektu: Spec-Driven & Multi-Agent Framework

Tento dokument slúži ako kompletný vzor (blueprint / prompt) pre AI agenta (alebo vývojára) na inicializáciu nového softvérového projektu. Projekt využíva metodiku **Spec-Driven & Multi-Agent Development**, ktorá striktne oddeľuje fázy návrhu a schvaľovania pred samotným programovaním.

Podporuje súbežnú koexistenciu dvoch AI nástrojov:

1. **GitHub Copilot** (pomocou `.github/agents/*.agent.md` a `.github/copilot-instructions.md`)
2. **Google Antigravity / Gemini CLI** (pomocou `.agents/skills/*/SKILL.md` a `GEMINI.md`)

---

## 1. Stromová štruktúra projektu

AI agent má vytvoriť nasledujúcu štruktúru priečinkov a súborov:

```text
<PROJECT_ROOT>/
├── .agents/
│   └── skills/                         # Zručnosti a roly pre Google Antigravity / Gemini CLI
│       ├── business-analyst/SKILL.md
│       ├── system-architect/SKILL.md
│       ├── security-officer/SKILL.md
│       ├── tech-lead/SKILL.md
│       ├── software-engineer/SKILL.md
│       ├── qa-engineer/SKILL.md
│       ├── devops-engineer/SKILL.md
│       └── technical-writer/SKILL.md
│
├── .github/
│   ├── agents/                         # Custom agenti pre GitHub Copilot (VS Code)
│   │   ├── 01-business-analyst.agent.md
│   │   ├── 02-system-architect.agent.md
│   │   ├── 03-security-officer.agent.md
│   │   ├── 04-tech-lead.agent.md
│   │   ├── 05-software-engineer.agent.md
│   │   ├── 06-qa-engineer.agent.md
│   │   ├── 07-devops-engineer.agent.md
│   │   └── 08-technical-writer.agent.md
│   └── copilot-instructions.md         # Globálne inštrukcie pre GitHub Copilot
│
├── tasks/                              # Sledovanie úloh a schvaľovacie brány
│   └── TASK-YYYYMM-NNN-template.md     # Šablóna pre centrálny ticket úlohy
│
├── docs/                               # Špecifikácie a dokumentačný portál (MkDocs)
│   ├── docs.md                         # Metodika a pracovný tok taskov
│   ├── 01-business/                    # Výstupy Business Analysta
│   │   ├── requirements.md
│   │   ├── domain-glossary.md
│   │   └── acceptance-criteria.md
│   ├── 02-architecture/                # Výstupy System Architecta
│   │   ├── system-design.md
│   │   ├── data-model.md
│   │   └── adr/
│   │       └── ADR-001-template.md
│   ├── 03-technical/                   # Výstupy Tech Leada
│   │   ├── api-specs.md
│   │   ├── coding-standards.md
│   │   └── module-breakdown.md
│   └── 04-security/                    # Výstupy Security Officera
│       ├── threat-model.md
│       ├── secret-management.md
│       └── rate-limits-audit.md
│
├── src/                                # Zdrojový kód (výhradne Software Engineer)
│   └── __init__.py                     # Alebo index.ts podľa technológie
│
├── tests/                              # Testy (výhradne QA Engineer)
│   ├── unit/
│   ├── integration/
│   ├── fixtures/
│   └── reports/
│
├── deploy/                             # Infraštruktúra a CI/CD (DevOps Engineer)
│   ├── docker/
│   │   └── Dockerfile
│   ├── ci-cd/
│   └── systemd/
│
├── .gitattributes                      # Normalizácia koncov riadkov (LF)
├── .gitignore                          # Ignorované súbory (venv, secrets, node_modules)
├── .markdownlint.json                  # Pravidlá formátovania markdownu
├── GEMINI.md                           # Pravidlá pre Google Antigravity / Gemini CLI
├── mkdocs.yml                          # Konfigurácia dokumentačného portálu MkDocs Material
├── requirements.txt                    # Python závislosti pre dokumentáciu
└── README.md                           # Hlavný prehľad projektu a matica zodpovedností
```

---

## 2. Základné konfiguračné súbory v koreni projektu

Pri inicializácii vytvor tieto súbory s nasledujúcim obsahom:

### `.gitattributes`

```gitattributes
# Auto-detect text files and normalize line endings
* text=auto

# Explicitly declare files that should always use LF line endings
*.yml text eol=lf
*.yaml text eol=lf
*.json text eol=lf
*.md text eol=lf
*.py text eol=lf
*.ts text eol=lf
*.js text eol=lf
```

### `.gitignore`

```gitignore
# Environment and secrets
.env
.env.*
!.env.example
*.pem
*.key
credentials.json
secrets.json
config.local.*

# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
build/
site/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
*.egg-info/
.installed.cfg
*.egg
.venv/
venv/
ENV/
env/

# Node.js
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.pnpm-debug.log*

# Databases and local storage
*.sqlite
*.sqlite3
*.db
/data/local/

# IDE & OS
.DS_Store
Thumbs.db
*.bak
*.tmp
```

### `.markdownlint.json`

```json
{
  "default": true,
  "MD012": false,
  "MD013": false,
  "MD029": false,
  "MD033": false
}
```

### `requirements.txt`

```text
mkdocs>=1.6.0
mkdocs-material>=9.5.0
pymdown-extensions>=10.7
```

### `GEMINI.md`

```markdown
# Pravidlá pre tento projekt
- Správaj sa ako senior softvérový inžinier / architekt.
- Striktne dodržuj metodiku Spec-Driven vývoja a zručnosti definované v `.agents/skills/`.
- Pri plnení úloh neupravuj zdrojový kód v `src/` bez schválenej špecifikácie v `docs/`.
```

### `mkdocs.yml`

```yaml
site_name: <NÁZOV_PROJEKTU>
site_description: Projektová a technická dokumentácia riadená špecifikáciami
site_author: <AUTOR>
repo_url: https://github.com/<USER>/<REPO>
repo_name: <USER>/<REPO>

theme:
  name: material
  language: sk
  palette:
    - media: "(prefers-color-scheme: light)"
      scheme: default
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-7
        name: Prepnúť na tmavý režim
    - media: "(prefers-color-scheme: dark)"
      scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-4
        name: Prepnúť na svetlý režim
  features:
    - navigation.instant
    - navigation.tracking
    - navigation.sections
    - navigation.expand
    - navigation.top
    - search.suggest
    - search.highlight
    - content.code.copy

markdown_extensions:
  - admonition
  - pymdownx.details
  - pymdownx.superfences:
      custom_fences:
        - name: mermaid
          class: mermaid
          format: !!python/name:pymdownx.superfences.fence_code_format
  - pymdownx.highlight:
      anchor_linenums: true
      line_spans: __span
      pygments_lang_class: true
  - pymdownx.inlinehilite
  - tables
  - toc:
      permalink: true

plugins:
  - search

nav:
  - Pracovný tok: docs.md
  - Biznis:
      - Základné požiadavky: 01-business/requirements.md
      - Slovník pojmov: 01-business/domain-glossary.md
      - Akceptačné kritériá: 01-business/acceptance-criteria.md
  - Architektúra:
      - Systémový návrh: 02-architecture/system-design.md
      - Dátový model: 02-architecture/data-model.md
  - Technický dizajn:
      - API špecifikácia: 03-technical/api-specs.md
      - Štandardy kódu: 03-technical/coding-standards.md
      - Rozpad modulov: 03-technical/module-breakdown.md
  - Bezpečnosť:
      - Model hrozieb: 04-security/threat-model.md
      - Správa tajomstiev: 04-security/secret-management.md
      - Limity a audit: 04-security/rate-limits-audit.md
```

### `README.md`

```markdown
# <NÁZOV_PROJEKTU>

Systém vyvíjaný na základe schválených špecifikácií (**Spec-Driven & Multi-Agent Development**).

## 1. Koncepcia projektu a riadenie agentov

Projekt funguje na princípe **Spec-Driven Development** (vývoj riadený špecifikáciami) a práce rozdelenej medzi špecializované roly. Používateľ vyberá agenta podľa fázy a pred pokračovaním do ďalšej fázy schvaľuje výstup. Žiaden kód v produkčnom priečinku `src/` sa nevytvára bez predchádzajúceho definovania a schválenia požiadaviek v príslušných špecifikačných vrstvách.

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

## 2. Inštalácia dokumentačného portálu

```bash
python -m venv .venv
source .venv/bin/activate  # alebo .\.venv\Scripts\activate na Windows
pip install -r requirements.txt
mkdocs serve
```

---

## 3. Roly agentov pre GitHub Copilot (`.github/`)

### `.github/copilot-instructions.md`

```markdown
# Pokyny pre GitHub Copilot

Tento repozitár používa špecifikáciami riadený vývoj (Spec-Driven Development).

## Pracovný postup
- Pred zmenou si prečítaj relevantné schválené dokumenty a dodrž rolu zvoleného custom agenta.
- Pracuj iba v rozsahu danej úlohy. Jedinou výnimkou mimo výstupného priečinka roly je aktualizácia vlastnej fázy v tickete `tasks/TASK-YYYYMM-NNN.md`, ktorý používateľ výslovne priradil.
- Schválenie výstupu jednej etapy je potrebné pred pokračovaním ďalšou rolou. Agenti sa vyberajú ručne.
- Pre úlohu používaj jeden centrálny súbor `tasks/TASK-YYYYMM-NNN.md`; nikdy ho medzi agentmi nepremiestňuj ani nepremenúvaj.
- Aktualizuj iba vlastnú fázu tasku: stav práce, stručné zhrnutie a odkazy na svoje výstupy. Pole schválenia mení iba používateľ.
- Git commit alebo push vykonaj iba na výslovnú požiadavku používateľa.
```

### Šablóny súborov `.github/agents/*.agent.md`

Každý agent má YAML frontmatter špecifický pre GitHub Copilot:

```text
---
name: <Názov Roly>
description: "<Popis zodpovednosti>"
target: github-copilot
tools: [read, search, edit]   # pre vývojárske roly aj: [read, search, edit, execute]
---
# Rola: <Názov Roly>

## Poslanie
...

## Zodpovednosti
...

## Hranice a postup
- Čítaj vstupné dokumenty prislúchajúce tvojej fáze.
- Zapisuj výstupy výhradne do tvojho vyhradeného priečinka v `docs/` (alebo `src/`, `tests/`, `deploy/`).
- Ak používateľ priradil task v `tasks/`, aktualizuj iba záznam svojej fázy. Schválenie vypĺňa výlučne používateľ.
- Pred odovzdaním ďalšej roli počkaj na schválenie používateľom.
```

Zoznam 8 agentov pre `.github/agents/`:

1. `01-business-analyst.agent.md` (tools: `[read, search, edit]`, výstup: `docs/01-business/`)
2. `02-system-architect.agent.md` (tools: `[read, search, edit]`, výstup: `docs/02-architecture/`)
3. `03-security-officer.agent.md` (tools: `[read, search, edit]`, výstup: `docs/04-security/`)
4. `04-tech-lead.agent.md` (tools: `[read, search, edit]`, výstup: `docs/03-technical/`)
5. `05-software-engineer.agent.md` (tools: `[read, search, edit, execute]`, výstup: `src/`)
6. `06-qa-engineer.agent.md` (tools: `[read, search, edit, execute]`, výstup: `tests/`)
7. `07-devops-engineer.agent.md` (tools: `[read, search, edit, execute]`, výstup: `deploy/`, `.github/workflows/`)
8. `08-technical-writer.agent.md` (tools: `[read, search, edit, execute]`, výstup: `docs/`, `mkdocs.yml`)

---

## 4. Roly agentov pre Google Antigravity / Gemini CLI (`.agents/skills/`)

Pre Antigravity a Gemini CLI sa roly definujú ako **Skills** pod priečinkom `.agents/skills/<nazov-roly>/SKILL.md`. Tým získajú plnú podporu automatickej detekcie a lomítkových príkazov (napr. `/tech-lead`).

### Šablóna súboru `SKILL.md`

```markdown
---
name: <nazov-roly>
description: Use for <stručný popis účelu a kedy má model túto rolu aktivovať>.
---

# Rola: <Názov Roly>

## Poslanie
<Poslanie roly v kontexte projektu>

## Zodpovednosti
- <Zodpovednosť 1>
- <Zodpovednosť 2>

## Hranice a postup
- Čítaj schválené materiály z predchádzajúcich fáz.
- Zapisuj výstupy iba do vyhradeného priečinka.
- Ak používateľ priradil task v `tasks/`, aktualizuj výhradne svoju fázu v ňom.
- Pred odovzdaním ďalšej roli zhrň výstupy a vyžiadaj si schválenie používateľom.

## Očakávaný výstup
<Zoznam konkrétnych výstupných súborov>
```

Zoznam 8 zručností:

* `.agents/skills/business-analyst/SKILL.md` (príkaz: `/business-analyst`)
* `.agents/skills/system-architect/SKILL.md` (príkaz: `/system-architect`)
* `.agents/skills/security-officer/SKILL.md` (príkaz: `/security-officer`)
* `.agents/skills/tech-lead/SKILL.md` (príkaz: `/tech-lead`)
* `.agents/skills/software-engineer/SKILL.md` (príkaz: `/software-engineer`)
* `.agents/skills/qa-engineer/SKILL.md` (príkaz: `/qa-engineer`)
* `.agents/skills/devops-engineer/SKILL.md` (príkaz: `/devops-engineer`)
* `.agents/skills/technical-writer/SKILL.md` (príkaz: `/technical-writer`)

---

## 5. Správa úloh (`tasks/`)

### `tasks/TASK-YYYYMM-NNN-template.md`

```markdown
# TASK-YYYYMM-NNN: <Stručný názov úlohy>

**Stav:** Nový  
**Aktuálna fáza:** 1. Biznis špecifikácia  
**Priradený agent:** Business Analyst  
**Vytvorené:** YYYY-MM-DD HH:mm  
**Dokončené:** —

## Cieľ a rozsah

Opíš požadovaný výsledok, hranice úlohy a dôležité predpoklady.

## Akceptačné kritériá

- [ ] Doplň merateľné kritérium akceptácie.

## Fázy a výstupy

Každý agent dopĺňa iba záznam svojej fázy a odkazy na vlastné výstupy. Stav schválenia vypĺňa používateľ.

### 1. Biznis špecifikácia (Business Analyst)
**Stav:** Čaká  
**Zhrnutie:**  
**Výstupy:** Doplň relatívne odkazy do `../docs/01-business/`.  
**Schválenie používateľom:** Čaká

### 2. Systémová architektúra (System Architect)
**Stav:** Čaká  
**Zhrnutie:**  
**Výstupy:** Doplň relatívne odkazy do `../docs/02-architecture/`.  
**Schválenie používateľom:** Čaká

### 3. Bezpečnostné posúdenie (Security Officer)
**Stav:** Čaká  
**Zhrnutie:**  
**Výstupy:** Doplň relatívne odkazy do `../docs/04-security/`.  
**Schválenie používateľom:** Čaká

### 4. Technický dizajn (Tech Lead)
**Stav:** Čaká  
**Zhrnutie:**  
**Výstupy:** Doplň relatívne odkazy do `../docs/03-technical/`.  
**Schválenie používateľom:** Čaká

### 5. Implementácia (Software Engineer)
**Stav:** Čaká  
**Zhrnutie:**  
**Výstupy:** Uveď zmenené súbory v `../src/`.  
**Schválenie používateľom:** Čaká

### 6. Testovanie a verifikácia (QA Engineer)
**Stav:** Čaká  
**Zhrnutie:**  
**Výstupy:** Uveď testy v `../tests/` a zbehnuté príkazy.  
**Schválenie používateľom:** Čaká

### 7. Nasadenie a prevádzka (DevOps Engineer)
**Stav:** Čaká  
**Zhrnutie:**  
**Výstupy:** Doplň relatívne odkazy do `../deploy/`.  
**Schválenie používateľom:** Čaká

### 8. Dokumentácia (Technical Writer)
**Stav:** Čaká  
**Zhrnutie:**  
**Výstupy:** Doplň odkazy na stránky v `../docs/` a zmeny v `mkdocs.yml`.  
**Schválenie používateľom:** Čaká

## Uzavretie
**Výsledok:**  
**Dokončené:** YYYY-MM-DD HH:mm
```

---

## 6. Predvolená štruktúra špecifikácií (`docs/`)

Vytvor súbor `docs/docs.md` a základné prázdne kostry pre jednotlivé špecifikácie:

### `docs/docs.md`

```markdown
# Pracovný tok taskov

Projekt používa špecifikácie a roly agentov na rozdelenie práce do kontrolovateľných etáp.

## Zásady
1. Každá úloha má jeden kanonický súbor `tasks/TASK-YYYYMM-NNN.md`.
2. Výstupy agentov patria do priečinkov určených ich rolou.
3. Task eviduje stav, stručné zhrnutie fázy a odkazy na výstupy.
4. Schválenie každej fázy vykonáva výhradne používateľ.
```

### Základné šablóny v podpriečinkoch

* **`docs/01-business/requirements.md`**: Obsahuje ciele projektu, používateľské príbehy (User Stories), funkčné a nefunkčné požiadavky.
* **`docs/01-business/domain-glossary.md`**: Slovník pojmov a entít domény.
* **`docs/01-business/acceptance-criteria.md`**: Definícia hotového (Definition of Done) a akceptačné kritériá.
* **`docs/02-architecture/system-design.md`**: Komponentová schéma, diagramy dátových tokov (Mermaid).
* **`docs/02-architecture/data-model.md`**: Dátové entity, vzťahy a schéma databázy.
* **`docs/02-architecture/adr/ADR-001-template.md`**: Šablóna pre architektonické rozhodnutia (Kontext, Rozhodnutie, Dôsledky).
* **`docs/03-technical/api-specs.md`**: OpenAPI / REST / RPC rozhrania a dátové zmluvy.
* **`docs/03-technical/coding-standards.md`**: Dohodnuté konvencie kódu, linting, formátovanie a ošetrenie chýb.
* **`docs/03-technical/module-breakdown.md`**: Rozdelenie zdrojového kódu na moduly a balíčky.
* **`docs/04-security/threat-model.md`**: Model hrozieb (STRIDE / riziká a ich mitigácie).
* **`docs/04-security/secret-management.md`**: Pravidlá pre nakladanie s kľúčmi, heslami a `.env`.
* **`docs/04-security/rate-limits-audit.md`**: Pravidlá obmedzovania volaní a auditné logovanie.

---

## 7. Inštrukcie pre AI generátor (Ako vygenerovať projekt)

Ak dostane AI agent požiadavku: *„Inicializuj nový projekt podľa project-template.md“*, má vykonať tieto kroky:

1. **Vytvoriť strom priečinkov**:
   * `.agents/skills/` (vrátane 8 podpriečinkov)
   * `.github/agents/`
   * `tasks/`
   * `docs/01-business/`, `docs/02-architecture/adr/`, `docs/03-technical/`, `docs/04-security/`
   * `src/`, `tests/unit/`, `tests/integration/`, `tests/fixtures/`, `tests/reports/`
   * `deploy/docker/`, `deploy/ci-cd/`, `deploy/systemd/`
2. **Vygenerovať konfiguračné súbory** v koreni (`.gitattributes`, `.gitignore`, `.markdownlint.json`, `requirements.txt`, `GEMINI.md`, `mkdocs.yml`, `README.md`).
3. **Vygenerovať agentov pre Copilot** do `.github/agents/*.agent.md` a inštrukcie do `.github/copilot-instructions.md`.
4. **Vygenerovať zručnosti pre Gemini / Antigravity** do `.agents/skills/*/SKILL.md`.
5. **Vygenerovať šablónu úloh** do `tasks/TASK-YYYYMM-NNN-template.md`.
6. **Vygenerovať základné špecifikácie** do `docs/`.
7. **Skontrolovať konce riadkov** tak, aby všetky textové súbory mali striktne LF (`\n`).

