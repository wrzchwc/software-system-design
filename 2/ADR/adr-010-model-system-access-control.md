# Architecture Decision Record: Model System Access Control

## Kontekst
System wymaga modelu który będzie realizował wymagania związane z uwierzytelnianie użytkowników i zarządzaniem ich kontami. 

## Decyzja

Model będzie realizowany poprzez integrację z AWS Cognito.

### Uzasadnienie

Typ:
- Product

Klasa Problemu:
- Integracja

Wybrano integracje z gotowym rozwiązaniem ze względu na mniejsze koszta implementacji. AWS Congito w pełni spełnia wymagania takie jak uwierzytelnianie użytkowników, tworzenie/modyfikowanie/usuwanie kont użytkowników, 2FA, weryfikację konta poprzez email. Rozpatrywano wykorzystanie Spring Security do tych wymagań natomiast implementacja tego okazałaby się droższa pod kątem czasowym. Spring Security dalej będzie wykorzystywane w systemie, ale jedynie do autoryzacji oparacji wykonywanych przez uwierzytelnionych już użytkowników.

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- wykorzystanie gotowego rozwiązania z rynku
- wysoka konfigurowalność narzędzia
- mniejsze koszta

### Negatywne
- uzależnienie się od dostawcy usług (vendor lock-in)

## Referencje

Include links or citations to supporting materials:
- Research papers
- Meeting notes
- Alternatives comparison
- Standards or guidelines

## Data

``15/12/2024``