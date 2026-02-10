# Testovací strategie — Happy Bank

## Cíl
Zajistit, že systém bankovních účtů a převodů je funkční, bezpečný, spolehlivý a připravený pro nasazení. Pokrýt kritické funkce, integrace, výkon a datovou integritu.

## Rozsah
- API pro správu účtů, převody, transakce
- Databázová perzistence transakcí a stavů účtů
- End-to-end scénáře (např. převod mezi účty)
- Chybové a okrajové případy (nedostatečný zůstatek, špatné vstupy)

## Testovací úrovně
- Unit tests: obchodní logika, validace vstupů, výpočty zůstatků
- Integration tests: repository/DB, API endpoints, message queues (pokud jsou)
- End-to-end tests: kompletní scénáře přes API (převod, ověření zůstatků, zápis transakcí)
- Smoke tests: základní health checks po nasazení
- Regression tests: kritické scénáře po změnách

## Typy testů
- Funkční: CRUD účtů, převody, seznam transakcí
- API: contract tests, status codes, chybové stavy
- Data integrity: atomické transakce, rollback chyb
- Performance: latence API, zatížení převodů, DB throughput
- Security: ověřování, autorizace, vstupní validace, SQL injection
- Reliability/Concurrency: race conditions při souběžných převodech
- Exploratory a negative testing: neplatné částky, neexistující účty

## Testovací data a prostředí
- Izolované testovací DB (snapshot/containers) + možnost restore/rollback
- Testovací účty/fixures: explicitně definované stavy (např. Vilhem: Secret 2000, Alice: Savings 500)
- Seed + teardown nebo transactional rollback pro idempotentní testy
- Identifikace dat citlivých a jejich masking

## Nástroje a infrastruktura
- Unit: pytest / Jest / xUnit dle stacku
- API/E2E: pytest+requests, Postman/Newman, Playwright/ Selenium (pokud UI)
- DB: testcontainers nebo lokální test DB + migrate tooling
- CI: GitHub Actions / Azure Pipelines — spouštět unit + integration + smoke na PR a nightly runs pro E2E/perf
- Monitoring/reporting: test reports (JUnit), coverage, Sentry/observability pro nasazení

## Test návrh a pokrytí
- Prioritizovat kritické scénáře (peněžní převody, rollback, autorizace)
- Definovat test cases: vstup, očekávaný výstup, cleanup
- Mapovat testy na akceptační kritéria a user stories
- Měřit coverage pro business logic (ne nutně úplné 100% pro infra)

## CI/CD integrace
- PR gate: unit + lint + fast integration
- Merge: kompletní integration + smoke
- Nightly: E2E + performance + security scans
- Fail-fast policy pro kritické testy

## Reporting a metriky
- Test pass rate, flakiness, test duration
- Počet bugů/priority z testů
- Doba do oprav (MTTR)
- Automatizované reporty napojené do PR a Slack/Teams

## Rizika a mitigace
- Flaky tests: izolovat a opravit / quarantine
- Database state drift: používat migrations + seed + teardown
- Souběžné změny v API: contract tests + consumer-driven contracts

## Údržba testů
- Review testů jako součást PR
- Periodická revize a čištění starých/neaktuálních testů
- Dokumentace test fixtures a běhu testovacího prostředí