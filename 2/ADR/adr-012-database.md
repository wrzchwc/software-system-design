# Architecture Decision Record: Wybór silnika bazodanowego

## Kontekst

System wymaga bazy danych, która zapewni wysoką wydajność, niezawodność, zgodność z ACID, a także możliwość skalowania w przyszłości. Wybór odpowiedniego systemu zarządzania bazą danych (DBMS) jest kluczowy dla długoterminowego sukcesu projektu, uwzględniając zarówno aktualne potrzeby, jak i potencjalne przyszłe wymagania.

## Decyzja

Wybieramy PostgreSQL jako silnik bazodanowowy w projekcie

### Uzasadnienie
- Funkcjonalność i zgodność z ACID
- Obsługuje szeroki zakres typów danych, w tym dane przestrzenne (dzięki rozszerzeniu PostGIS), JSON/JSONB, oraz wiele niestandardowych funkcji, takich jak materializowane widoki czy zapytania hierarchiczne.
- Jest open-source, co pozwala na uniknięcie kosztów licencyjnych i uzależnienia od dostawcy.
- Posiada aktywną społeczność i bogatą dokumentację, co ułatwia rozwiązywanie problemów i rozwijanie projektu.
- Obsługuje zarówno poziome, jak i pionowe skalowanie, co czyni go odpowiednim zarówno dla małych, jak i dużych aplikacji.
- Oferuje rozbudowane mechanizmy kontroli dostępu i funkcje takie jak SSL oraz obsługa logowania na podstawie ról.
- Umożliwia tworzenie schematów bazodanowych
- Umożliwia tworzenie oddzielnych baz danych w ramach jednego silnika bazodanowego
- Jest wspierany przez Amazon RDS

Rozpatrywano również OracleDB, MSSQL oraz MySQL. Pierwsze dwie zostału odrzucone ze względu na wysoką złożoność i koszty związane z licencjami. MySQL został odrzucony poniweaż w porównaniu do PostgreSQL posiada mniejsze wsparcie dla operacji wsółbieżnych oraz gorzej radzi sobie z optymalizacją złożonych zapytań. 
## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Stabilność i niezawodność
- Brak kosztów licencyjnych
- Możliwość rozwoju
- Wydajnosć

### Negatywne
- Może być bardziej wymagający pod względem zasobów systemowych
- Aby osiągnąć optymalną wydajność, PostgreSQL wymaga starannej konfiguracji i regularnego monitorowania
- PostgreSQL może być bardziej wymagający dla mniej doświadczonych użytwkoników

## Referencje
- [PostgreSQL Docs](https://www.postgresql.org.pl/)
- [Amazon RDS fo PostgreSQL](https://aws.amazon.com/rds/postgresql/)

## Data

``15/12/2024``