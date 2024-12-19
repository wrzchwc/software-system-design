# Architecture Decision Record: Model Resource Access Control

## Kontekst

System pojedyńczego źródła prawdy zawierającego informację na temat uprawnień do zasobów ze względu na wymagania dotyczące nadawania, odbierania uprawnień:
- Jako klient biznesowy Deskly chciałbym posiadać konto użytkownika, które będzie pozwalać mi jako pracodawcy zarządzać dostępem do zarezerwowanych zasobów dla pracowników.
- Klienci którzy nie uregulowali opłaty po 7 dniach od wystawienia faktury, tracą dostęp do zasobów Deskly i rozpoczyna się naliczanie odsetek od niezapłaconej faktury.

## Decyzja

Logika związana z zarządzaniem uprawniniamu do zasobów będzie realizowana przez oddzielny model. 

### Uzasadnienie

Typ modelu:
- Product

Klasa problemu:
- CRUD

W wyniku analizy event stormingowej zauważono że logika związana z dostępem do zasobów jest wykorzystywana przez wiele procesów biznesowych. Tym samym podjęto decyzję o enkapsulacji tej logiki w oddzielnym modelu.

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Niski coupling na poziomie modułowym, 
- Hermetyzacja logiki i pojedyńcze źródło prawdy na temat uprawnień użytkowników do zasobów (Sepracja odpowiedzialności)
- Większa elastyczność i ponowne użycie
- Testowalność

### Negatywne
- Dodatkowa złożoność
- Musi być wydajna nawet przy dużym obciążeniu  (overhead implementacyjny)

## Referencje

- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)

## Data

``15/12/2024``