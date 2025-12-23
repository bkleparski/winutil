# Ravnet — adaptacja winutil (winutilPLRAV)

Ten dokument opisuje założenia i podstawowe wytyczne dla forka projektu ChrisTitusTech/winutil dostosowanego do użytku w firmie Ravnet. Projekt oryginalny jest na licencji MIT — nie zmieniamy pliku LICENSE w tym repo.

## Cel projektu
Celem jest utrzymanie funkcjonalności upstream (instalatory, tweak'i, skrypty PowerShell) oraz dodanie firmowego brandingu, konfiguracji i procesów umożliwiających bezpieczne i powtarzalne wdrożenie w środowisku Ravnet.

## Branding i zasoby
- Dodaj katalog `branding/` w repo i wstaw tam logo w formatach `logo-ravnet.svg` i `logo-ravnet.png`.
- W nagłówkach skryptów umieszczaj krótkie informacje:
  - Copyright © 2025 Ravnet
  - Link do repo: https://github.com/bkleparski/winutil
- Dokumentacja brandingu: `branding/README.md` (instrukcja użycia assetów).

## Przechowywanie repo i synchronizacja z upstream
- Repo jest publiczne: `bkleparski/winutil`.
- Rekomendacja branch protection na `main` (wymóg review i przejścia CI).
- Jak synchronizować z upstream:
  - git remote add upstream https://github.com/ChrisTitusTech/winutil.git
  - git fetch upstream
  - git checkout main
  - git merge upstream/main  (albo rebase, zgodnie z polityką)

## Bezpieczeństwo i zarządzanie sekretami
- Nie commitować sekretów/poświadczeń do repo.
- Używać GitHub Secrets / Organization Secrets dla certyfikatów i tokenów.
- Włączyć Secret Scanning i Dependabot Alerts.
- Przeskanować historię repo na obecność tajnych danych przed wdrożeniem.

## CI/CD — minimalne wymagania
Zalecane kroki w pipeline:
1. Lint: PSScriptAnalyzer (konfiguracja w `lint/`).
2. Testy: Pester (katalog `pester/`).
3. Package: wygenerowanie artefaktu ZIP/MSI dla dystrybucji.
4. Code signing: wykonywane na bezpiecznym runnerze z dostępem do certyfikatu.
- Przykład workflow: `.github/workflows/ci.yml` zawierający powyższe kroki.

## Pakowanie i dystrybucja
- Twórz artefakty: ZIP oraz opcjonalnie MSI (do Intune/SCCM).
- Dodaj katalog `ravnet_overrides/` z plikami konfiguracyjnymi (proxy, mirror pakietów, telemetry off).
- Wersjonowanie: stosować tagi semver i Draft Releases przed publikacją.

## Pliki do dodania w następnych krokach
- CONTRIBUTING.md — zasady PR i review.
- README_RAVNET.md — instrukcja wdrożenia wewnętrznego.
- .github/workflows/ci.yml — pipeline CI.
- ravnet_overrides/README.md — opis opcji konfiguracyjnych.
- branding/README.md — zasady użycia logo i assetów.

## Uwagi prawne
- Zachowaj oryginalne informacje o licencji MIT w pliku LICENSE.
- Jeżeli modyfikacje będą istotne, skonsultuj je z działem prawnym Ravnet.

## Kontakt
Osoba kontaktowa: @bkleparski
Zespół DevOps (placeholder): devops@ravnet.example

---
