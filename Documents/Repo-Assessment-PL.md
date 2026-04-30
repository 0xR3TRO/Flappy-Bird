# 1. Executive Summary
- Typ projektu: prosta gra przeglądarkowa (HTML/CSS/JS + Canvas), statyczna aplikacja bez widocznego backendu w repo.
- Największe problemy:
  1) Rozjazd między dokumentacją a repo (README deklaruje React/Node/SQLite, ale w repo brak kodu backendu i frameworka).
  2) Brak narzędzi jakości (testy, lint/format, CI/CD).
  3) Brak procesu wydawniczego i standardów PR.
  4) Brak obserwowalności i logowania błędów.
  5) Brak formalnego zarządzania zależnościami/bezpieczeństwem (brak package managera).
- Największe dźwignie poprawy (top 5):
  1) Ujednolicić dokumentację ze stanem repo (albo wdrożyć backend, albo skorygować opis).
  2) Dodać minimalny toolchain frontendu (package.json + lint/format + testy unit).
  3) Zbudować prosty pipeline CI (lint + test + build).
  4) Zdefiniować strukturę modułów gry i kontrakty między nimi.
  5) Wprowadzić podstawowy monitoring błędów i metryki jakości.

# 2. Odczyt repo z samej struktury i dokumentacji
- Co wiadomo na pewno:
  - Repo to statyczna gra w przeglądarce: index.html + katalog „Directories/” (script.js, style.css).
  - Wykorzystuje Canvas, obrazy są w katalogu „Media & Images”.
  - Brak package.json, brak konfiguracji CI/CD, brak testów i zależności.
  - README/README(PL) opisują projekt i deklarują architekturę MVC oraz technologie (React/Node/SQLite).
- Założenia (jawnie):
  - Założenie: leaderboard jest docelowo wymagany (wynika z README), ale nie ma implementacji w kodzie.
  - Założenie: docelowy hosting to statyczny (np. GitHub Pages), bo brak backendu w repo.
  - Założenie: brak wymagań compliance/regulacji (brak danych w repo).
- Luki informacyjne:
  - Brak informacji o docelowym środowisku uruchomieniowym, hostingu i domenie.
  - Brak SLA/SLO, brak polityk bezpieczeństwa i retencji danych.
  - Brak informacji o zespole i procesie (role, code review, release).
  - Brak wymagań dotyczących leaderboardu (anonimowy? logowanie? przechowywanie danych?).

# 3. Ocena dojrzałości (0–5)
| Obszar | Ocena | Uzasadnienie | Priorytet |
| --- | --- | --- | --- |
| Architektura | 1 | Jednoplikowa logika gry, brak modułów i kontraktów. | Wysoki |
| Jakość kodu | 2 | Kod działa, ale brak standardów, lintu i typów. | Wysoki |
| Testy | 0 | Brak infrastruktury testowej. | Wysoki |
| Bezpieczeństwo | 1 | Brak CSP, brak skanowania zależności, brak procesów. | Średni |
| CI/CD | 0 | Brak workflow. | Wysoki |
| Observability | 0 | Brak monitoringu, logów błędów. | Średni |
| DX | 1 | Brak narzędzi developerskich, brak komend. | Wysoki |
| Dokumentacja | 2 | Jest opis produktu, ale niezgodny ze stanem kodu. | Wysoki |
| Skalowalność | 1 | Brak backendu i warstw, ograniczona rozbudowa. | Średni |

# 4. Rekomendowany stack i narzędzia
| Obszar | Obecnie | Rekomendacja | Dlaczego | Koszt zmiany | Ryzyko |
| --- | --- | --- | --- | --- | --- |
| Runtime/framework | HTML/CSS/JS (vanilla) | Wariant A: utrzymać vanilla + modularizacja; Wariant B: Vite + TypeScript | A: najniższy koszt. B: lepsza jakość i skalowalność. | Niski/Średni | Niskie |
| Testy | Brak | Vitest (unit) + Playwright (e2e) | Szybka walidacja logiki i regresji UI. | Średni | Niskie |
| Lint/format | Brak | ESLint + Prettier | Standaryzacja, mniej błędów. | Niski | Niskie |
| Dependency/security scanning | Brak | Dependabot + npm audit (jeśli pojawi się package.json) | Wczesne wykrywanie CVE. | Niski | Niskie |
| CI/CD | Brak | GitHub Actions: lint + test + build + deploy | Automatyzacja jakości i publikacji. | Średni | Średnie |
| Monitoring/logging/tracing | Brak | Sentry (frontend) + proste eventy telemetryczne | Wgląd w błędy i stabilność. | Niski | Niskie |
| IaC / środowiska | Brak | Wariant A: GitHub Pages bez IaC; Wariant B: Terraform dla hostingu w chmurze | Dobór wg wymogów skali i polityk. | Niski/Średni | Średnie |
| Zarządzanie sekretami | Brak | GitHub Secrets (CI) + rotacja kluczy | Bezpieczne deploye i integracje. | Niski | Niskie |

**Warianty dla leaderboardu (brak danych w repo):**
- Wariant 1: localStorage (brak backendu) — wybór gdy ranking lokalny wystarczy i nie ma wymagań dot. kont.
- Wariant 2: lekki backend (Node/SQLite lub serverless) — wybór gdy potrzebny globalny ranking.
- Wariant 3: zewnętrzny backend-as-a-service — wybór gdy minimalny DevOps i szybki time-to-market.

# 5. Docelowa architektura i struktura repo
- Proponowane bounded contexts / moduły:
  - `game-core` (fizyka, kolizje, stan gry)
  - `rendering` (Canvas, sprite’y)
  - `input` (klawiatura, mobile)
  - `score` (licznik, persistencja)
  - `ui` (ekrany start/koniec/leaderboard)
  - `assets` (obrazy, dźwięki)
  - `api` (opcjonalny backend leaderboardu)
- Kontrakty między modułami:
  - `game-core` publikuje stan gry; `rendering` wyłącznie renderuje; `score` subskrybuje zdarzenia (np. zaliczenie przeszkody, koniec gry).
- Docelowe drzewo katalogów (przykładowe):
  - `src/`
    - `game-core/`
    - `rendering/`
    - `input/`
    - `score/`
    - `ui/`
    - `assets/`
  - `public/` (statyczne assety)
  - `docs/` (ADR, architektura)
  - `tests/` (unit/e2e)
  - `api/` (opcjonalny backend)
- Zasady „co gdzie trafia”:
  - Logika gry tylko w `game-core`.
  - Render i assety bez logiki domenowej w `rendering` i `assets`.
  - Persistencja wyników w `score` lub `api`.

# 6. Proces wytwarzania end-to-end
- Git workflow i standard PR:
  - GitHub Flow (main + krótkie feature branches), PR z checklistą jakości.
- Definition of Ready / Definition of Done:
  - DoR: opis celu, akceptacja kryteriów, brak otwartych zależności.
  - DoD: testy zielone, lint zielony, opis zmian, aktualizacja docs.
- Quality gates przed mergem:
  - Lint + testy unit/e2e + skan zależności.
- Wersjonowanie i release strategy:
  - SemVer + tagi release; automatyczny release notes.
- Plan rollback i hotfix:
  - Rollback przez revert release tagu; hotfix przez szybki PR z targetem `main`.

# 7. Plan wdrożenia (30-60-90)
**Quick Wins (1–2 tyg.)**
- Uporządkowanie dokumentacji i struktury katalogów.
- Dodanie minimalnego lint/format.
- Skonfigurowanie CI lint/test.

| Faza | Zadania | Owner (rola) | Zależności | Ryzyko | Kryterium ukończenia |
| --- | --- | --- | --- | --- | --- |
| 0–30 | Ujednolicenie docs vs kod; dodanie package.json + lint/format; prosty CI | Tech Lead | Brak | Niskie | CI zielone + zaktualizowane docs |
| 31–60 | Modularizacja kodu gry; testy unit; wstępny e2e | Staff Engineer | Wariant toolchain | Średnie | Pokrycie logiki gry testami |
| 61–90 | Decyzja o leaderboardzie (warianty); monitoring błędów; release pipeline | Architect/DevOps | Decyzja produktowa | Średnie | Stabilny release + metryki |

# 8. Rejestr ryzyk i mitigacje
| Ryzyko | Prawdopodobieństwo | Wpływ | Mitigacja | Trigger |
| --- | --- | --- | --- | --- |
| Rozjazd docs vs kod | Wysokie | Średni | Audyt dokumentacji i aktualizacja | Każdy release |
| Brak testów i regresje | Wysokie | Wysoki | Wprowadzić unit/e2e | Wzrost liczby bugów |
| Brak backendu dla leaderboardu | Średnie | Średni | Decyzja wariantu + prototyp | Wymaganie globalnego rankingu |
| Brak CSP i ochrony frontendu | Średnie | Średni | Dodać CSP i nagłówki | Incydent bezpieczeństwa |

# 9. Backlog techniczny (priorytetyzowany)
**P0**
- Ujednolicić dokumentację z repo (usunąć/uzupełnić rozjazdy) — uzasadnienie: redukcja błędnych decyzji; złożoność: S; efekt: spójna wiedza.
- Dodać lint/format + podstawowe testy unit — uzasadnienie: jakość; złożoność: M; efekt: mniej regresji.

**P1**
- Modularizacja logiki gry — uzasadnienie: maintainability; złożoność: M; efekt: łatwiejszy rozwój.
- Pipeline CI/CD z release notes — uzasadnienie: stabilne wydania; złożoność: M; efekt: automatyzacja.

**P2**
- Wariant backendu leaderboardu — uzasadnienie: funkcja produktu; złożoność: M/L; efekt: globalny ranking.
- Observability (Sentry + metryki) — uzasadnienie: niezawodność; złożoność: S/M; efekt: szybsza diagnoza.

# 10. Metryki sukcesu
- Bazowe KPI + targety po wdrożeniu:
  - DORA (Lead Time < 1 dzień, Deployment Frequency >= 1/tydzień, Change Failure Rate < 15%, MTTR < 1 dzień).
  - Jakość: coverage unit >= 60% (Założenie), 0 krytycznych problemów z lint.
  - Stabilność: crash rate < 1% sesji (Założenie).
  - Wydajność: stabilne FPS > 50 na typowym urządzeniu (Założenie).
- Jak mierzyć postęp co sprint:
  - Raport z CI (czas build/test), trend coverage, liczba defektów produkcyjnych, telemetryka błędów (Sentry).
