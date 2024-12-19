# Architecture Decision Record: Model Financials

## Kontekst
System musi realizować wymagania dotyczące agregacji i prezentowania danych finansowych w ramach konkretnych lokacji.

## Decyzja

Logika agregacji, transformacji i prezentacji danych finansowych odbywać się będzie w osobnym modelu dla którego źródłem informacji będzie model rezerwacji.

### Uzasadnienie

Typ modelu:
- Product

Klasy problemu:
- Prezentacja
- Transformacja

Model powinien istnieć niezależnie od modelu rezerwacji, pomimo że korzysta z danych w nim zawartych ze względu na inną klasę problemów której dotyczy. Logika dotycząca danych finansowych może ulec rozszerzeniu w przyszłości stąd decyzja o ich wydzieleniu, natomiast obecnie model ten skupia się głównie na wyliczaniu i prezentowaniu danych finansowych. Model będzie realizowany w warstwie aplikacji za czym przemawia łatwa testowalność rozwiązania, natomiast nic nie stoi na przeszkodzie żeby w przyszłości wyliczenia transformat odbywały się już na poziomie bazy danych. W przypadku dużych zbiorów rozwiązanie tego problemu na poziomie bazy danych może okazać się skuteczniejsze, natomiast na ten moment nie ma takiej potrzeby.

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Separacja odpowiedzialności
- Brak splątania klas problemów
- Może być łatwo optymalizowany pod kątem wydajności

### Negatywne
- Wymaga wiedzy z zakresu finansów, statystyki, analizy dużych zbiorów danych.

## Referencje
- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)

## Data

``15/12/2024``