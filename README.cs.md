# Mission Control 0.4.2 — Codex + Zoo Code

**Jeden projekt, jeden řádek.** Přehled skutečných požadavků na vývojáře, práce a
výsledků. Windows, WSL a Remote SSH; samostatný místní hub bez npm závislostí.

## Nové: Run / Deny pro původní Codex

V detailu projektu lze rozhodnout o živém požadavku původního Codexu pomocí
PermissionRequest hooku: Run, Deny nebo předání zpět běžnému schvalování.
Nevzniká druhý chat. **Jednorázové zapnutí a důvěra hooku v Codexu jsou nutné.**
Samotná instalace nic automaticky neschválí. [Podrobný postup](docs/CODEX-CONTROLS_042.cs.md).

Aktualizujte celý balíček přes `MissionControl-Setup-0.4.2-x64.exe`, ponechte
Connection + Bridge, po doběhnutí agentů načtěte okna znovu. Ve WSL/SSH také
vzdálený Bridge. V připojeném projektu spusťte
`Mission Control: Enable Codex Dashboard Controls`, potvrďte změnu a důvěru
hooků v Codexu (dokumentovaný přehled: `/hooks` v Codex CLI ve stejném prostředí).
Teprve první skutečný callback znamená ověřené spojení. Identita běžícího Bridge
je `0.4.2-codex-hooks.1`; diagnostika: `Mission Control: Copy Connection Report`.

Hook běží před nativním schválením. Již otevřený starý dotaz vyřiďte ve VS Code.
Po 5 minutách bez rozhodnutí, při odpojení nebo po „Vyřídit v Codexu“ pokračuje
původní politika — nejde o automatické Deny ani Run. Vyžaduje se kompatibilní
Codex, místní orchestrace, společný host/kořen a povolené hooky. Cloudová
orchestrace, volné textové odpovědi a ovládání rozběhlého terminálu nejsou podporované.

## Zachované funkce

Zoo Run / Deny, projektové souhrny, Teď / Změny / Historie, jedinečné připojení,
odpojení a vědomé obnovení projektu, aktualizace/oprava/odinstalace, autostart a
vyhledání VS Code. Data ani token při aktualizaci nemažte. Upozornění u lišty
standardně 60 sekund; kliknutí vybírá právě původní událost a nikdy nic neschvaluje.

Ovládání Zoo používá kontrolované vnitřní Task API. Codex hook nový veřejný
kontrakt. Pozorování starých JSONL zůstává pouze pro čtení. [Zoo podrobnosti](docs/ZOO_ACTIONS_041.cs.md).

## Vývoj a balíček

`node src/server.mjs` (Node.js 22+), `npm test`,
`python3 tests/codex_browser.py /tmp/mc-browser`,
`python3 scripts/build-windows.py`. Výchozí spuštění Windows obsluhuje tray.
`dashboard-demo.html` je samostatná ukázka, ne živé připojení.

[Windows návod](windows/Navod.html) · [Testy 0.4.2](docs/WINDOWS_TEST_REPORT-0.4.2.md)

EXE a VSIX jsou nepodepsané. Windows instalátor, reálný VS Code/Codex Extension
Host a Windows PowerShell nebyly zde spuštěné. Linuxové HTTP/hook/browser testy
nenahrazují cílové ověření. Ochrany Windows ani důvěru hooků kvůli balíčku neobcházejte.
