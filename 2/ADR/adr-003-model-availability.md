# Architecture Decision Record: Model Availability

## Kontekst
System potrzebuje pojedynczego źródła prawdy temat dostępności zasobów.

## Decyzja

Model dostępności będzie niezależnym generycznym modelem ogólnego przeznaczenia.

### Uzasadnienie
Typ modelu
  - Core Domain (Generic Core)

Klasa problemu
  - Konkurencja o zasoby

W wyniku analizy event stormingowej zuważono że wiele procesów w systemi w celu podjęcia dalszych akcji  musi odpowiedzieć na pytanie: Czy zasób jest dostępny ? Jest to najbardziej stabilna część wszystkich szczególnych wymagań funkcjonalnych stąd powinna być realizowana przez oddzielny generyczny model. Jedną z zasotosowanych heurystych wykorzystanych do podjecia tej decyzji jest analiza wejść i wyjść procesów biznesowych czyli jeśli różne procesy zbiegają się do wykonania konkretnych akcji, a po ich wykonaniu ponownie rozdzielą się w celu wykonywnia innych akcji to jedna z przesłanek do wydzielenia kontekstu logicznego. Inną zasosowana heurystyką jest heurystyka pytań głównych, czyli na jakie jedno ważne pytanie biznesowe powinien odpowiadać dany model i w tym przypadku jest to: Czy zasób jest dostępy ?

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Pojedyńcze źródło prawdy które odpowiada na pytanie: Czy zasób jest dostępny ?
- Brak splątania klas problemów
- Łatwa testowalność i utrzymywalność

### Negatywne
- Wymaga dobrego zrozumienia wielowątkowości i problemów związanych z konkruencja o zasoby
- Model ten wymaga szczególnie wysokiej jakości kodu ponieważ jest wyróżnikiem biznesowym dzięki któremu produkt zarabia


## Referencje
- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)

## Data

``15/12/2024``