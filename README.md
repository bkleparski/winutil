# winutil — Ravnet Toolbox

Graficzne narzędzie PowerShell do kompleksowej konfiguracji systemu Windows. Uruchamia się jako okno WPF z pięcioma zakładkami, umożliwiając instalację aplikacji, optymalizację systemu, zarządzanie usługami i tworzenie odchudzonego obrazu ISO.

## Uruchomienie

### Bezpośrednio z internetu (zalecane)

```powershell
iwr -useb https://raw.githubusercontent.com/bkleparski/winutil/main/winutil.ps1 | iex
```

### Z lokalnego pliku

```powershell
.\winutil.ps1
```

> Skrypt wymaga uprawnień **Administratora** — jeśli zostanie uruchomiony bez nich, automatycznie ponownie uruchomi się z podwyższonymi uprawnieniami.

### Parametry

| Parametr          | Typ      | Opis                                                             |
|-------------------|----------|------------------------------------------------------------------|
| `-Debug`          | switch   | Włącza tryb debugowania (szczegółowe logi w konsoli)             |
| `-Config <ścieżka>` | string | Ładuje konfigurację z podanego pliku JSON                       |
| `-Run`            | switch   | Natychmiast wykonuje zadania z załadowanego pliku konfiguracji   |

## Zakładki

### Install
Instalator aplikacji z obsługą **Winget** i **Chocolatey**. Aplikacje pogrupowane w kategorie:

| Kategoria         | Zawiera m.in.                                         |
|-------------------|-------------------------------------------------------|
| Browsers          | Chrome, Firefox, Brave, Edge                          |
| Communications    | Discord, Slack, Teams, Zoom                           |
| Development       | VS Code, Git, Node.js, Python, Docker                 |
| Document          | LibreOffice, Obsidian, Notepad++                      |
| Games             | Steam, Epic Games, GOG Galaxy                         |
| Microsoft Tools   | PowerToys, WSL, .NET Runtime                          |
| Multimedia Tools  | VLC, OBS Studio, GIMP, Audacity                       |
| Pro Tools         | 7-Zip, Everything, Process Hacker, WireShark          |
| Remote Access     | TightVNC, RustDesk, AnyDesk                           |
| Utilities         | Narzędzia systemowe i pomocnicze                      |

### Tweaks
Optymalizacje systemu pogrupowane według poziomu ryzyka:

- **Essential Tweaks** — zalecane ustawienia poprawiające wydajność i prywatność (wyłączenie telemetrii, Cortany, Copilota, ustawienia pamięci wirtualnej)
- **Performance Plans** — plany zasilania zoptymalizowane pod gaming lub pracę biurową
- **Powershell Profile** — instalacja/deinstalacja niestandardowego profilu PowerShell
- **Features** — włączanie/wyłączanie funkcji systemu Windows
- **Fixes** — poprawki dla typowych problemów (uprawnienia, resetowanie Store, naprawa sieci)
- **Legacy Windows Panels** — szybki dostęp do klasycznych paneli systemowych
- **Customize Preferences** — personalizacja interfejsu (pasek zadań, menu Start, Eksplorator)
- **Advanced Tweaks — CAUTION** — zaawansowane modyfikacje rejestru wymagające ostrożności

### Config
Konfiguracja usług systemowych Windows — włączanie, wyłączanie i zmiana trybu uruchamiania. Możliwość importu i eksportu ustawień do pliku JSON.

### Updates
Zarządzanie trybem aktualizacji systemu Windows:
- Wyłączenie automatycznych aktualizacji
- Tryb bezpieczeństwa (tylko krytyczne poprawki)
- Domyślne ustawienia Microsoft
- Wyłączenie aktualizacji sterowników przez Windows Update

### MicroWin
Tworzenie **odchudzonego obrazu ISO** systemu Windows bezpośrednio z zainstalowanej kopii lub dostarczonego ISO. Funkcje:

- Usuwanie bloatware, zbędnych pakietów i funkcji opcjonalnych
- Iniekcja sterowników (z bieżącego systemu lub wskazanego folderu)
- Obsługa VirtIO (maszyny wirtualne)
- Generowanie pliku `unattend.xml` z predefiniowanym kontem użytkownika
- Pominięcie wymagań sprzętowych (TPM, Secure Boot, CPU) — opcja `Unsupported Hardware`
- Wyłączenie animacji pierwszego logowania
- Wyłączenie wykonywania WPBT
- Zapis gotowego obrazu ISO na dysk lub pendrive

## Dodatkowe funkcje

- **Motywy** — Dark / Light / Auto (wykrywanie z systemu)
- **Import / Export** — zapis i wczytywanie kompletnej konfiguracji tweaków i aplikacji z pliku JSON
- **Konfiguracja DNS** — zmiana serwerów DNS na popularne alternatywy (Cloudflare, Google, Quad9 i inne)
- **Serwer SSH** — włączenie usługi OpenSSH Server
- **Skalowanie czcionek** — dostosowanie rozmiaru UI do rozdzielczości ekranu

## Wymagania

- Windows 10 / Windows 11
- PowerShell 5.1+ (lub PowerShell 7+)
- Uprawnienia **Administratora**
- Połączenie z Internetem (do pobierania aplikacji)

## Logi

Pełny log każdego uruchomienia zapisywany jest automatycznie w:

```
%LOCALAPPDATA%\winutil\logs\winutil_<data-godzina>.log
```
