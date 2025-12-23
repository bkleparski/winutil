# winutilPLRAV - Dokumentacja adaptacji dla Ravnet

## Cel projektu

Niniejszy fork stanowi adaptację projektu ChrisTitusTech/winutil dla potrzeb organizacji Ravnet. Głównym celem jest dostosowanie narzędzia do wewnętrznych standardów bezpieczeństwa, brandingu i procesów CI/CD obowiązujących w firmie, przy zachowaniu zgodności z upstream i licencją MIT.

## Branding

Aby zapewnić spójność wizualną z identyfikacją Ravnet:

- Utwórz katalog `/branding` w głównym katalogu repozytorium
- Umieść w nim zasoby graficzne (logo, ikony) w formatach PNG/SVG
- Zalecane nazwy plików: `ravnet_logo.png`, `ravnet_icon.ico`, `ravnet_banner.png`
- Dodaj plik `/branding/README.md` z wytycznymi dotyczącymi użycia zasobów graficznych

## Zarządzanie repozytorium

### Widoczność i ochrona

Repozytorium powinno pozostać **publiczne** zgodnie z polityką open source Ravnet. Zalecenia:

- Włącz ochronę gałęzi `main` (branch protection rules)
- Wymagaj review przed merge'em pull requestów
- Włącz automatyczne usuwanie gałęzi po merge'u

### Synchronizacja z upstream

Aby zsynchronizować zmiany z oryginalnego repozytorium ChrisTitusTech/winutil:

```bash
git remote add upstream https://github.com/ChrisTitusTech/winutil.git
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

## Bezpieczeństwo i zarządzanie sekretami

**Krytyczne wytyczne:**

- **Nigdy** nie commituj sekretów, kluczy API, certyfikatów do repozytorium
- Używaj GitHub Secrets lub Organization Secrets dla danych wrażliwych
- Włącz Secret Scanning w ustawieniach repozytorium
- Aktywuj Dependabot dla automatycznych aktualizacji zależności
- Regularnie przeglądaj alerty bezpieczeństwa w zakładce Security

## CI/CD - Przykładowy workflow

Zalecany pipeline CI/CD (plik `.github/workflows/ci.yml`):

```yaml
name: CI
on: [push, pull_request]
jobs:
  build:
    runs-on: windows-latest
    steps:
      - uses: actions/checkout@v4
      - name: Lint PowerShell
        run: Invoke-ScriptAnalyzer -Path . -Recurse
      - name: Test with Pester
        run: Invoke-Pester -Output Detailed
      - name: Package artifact
        run: Compress-Archive -Path *.ps1 -DestinationPath winutil-ravnet.zip
      - name: Sign binaries
        run: # Secure signing on dedicated runner
      - uses: actions/upload-artifact@v3
        with:
          name: winutil-ravnet
          path: winutil-ravnet.zip
```

## Pakowanie i dystrybucja

Dla wdrożeń korporacyjnych zalecamy:

- Tworzenie pakietów ZIP/MSI kompatybilnych z Microsoft Intune i SCCM
- Dodanie katalogu `/ravnet_overrides` z plikami konfiguracyjnymi specyficznymi dla Ravnet
- Dokumentacja overrides w pliku `/ravnet_overrides/README.md`
- Testowanie pakietów w środowisku UAT przed produkcją

## Następne kroki - Pliki do dodania

1. **CONTRIBUTING.md** - Wytyczne dla kontrybutorów (proces PR, code review, style guide)
2. **README_RAVNET.md** - Szczegółowa dokumentacja użytkowania w środowisku Ravnet
3. **.github/workflows/ci.yml** - Kompletny workflow CI/CD (patrz sekcja CI/CD)
4. **ravnet_overrides/README.md** - Dokumentacja nadpisań konfiguracji
5. **branding/README.md** - Wytyczne brandingowe i zasoby graficzne

## Kontakt

- Osoba odpowiedzialna: @bkleparski
- Zespół DevOps: [devops@ravnet.local] (placeholder - należy uzupełnić)

## Licencja

Projekt zachowuje oryginalną licencję MIT z upstream ChrisTitusTech/winutil. Wszelkie zmiany i dodatki również podlegają licencji MIT.

---

*Dokument stworzony: grudzień 2024 | Wersja: 1.0*
