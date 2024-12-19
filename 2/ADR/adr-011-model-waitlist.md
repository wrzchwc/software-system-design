# Architecture Decision Record: Model Waitlist

## Kontekst

System musi pozwalać klientom na zakolejkowanie się na dany termin do konkretnego zasobu, a pracownikom na zarządzanie kolejkami tzn. przesuwanie klientów w razie potrzeby lub rozwiązywanie kolejek gdy termin będzie niedostępny z przyczyn niezależnych.  

## Decyzja

- Model będzie realizowany z wykorzystaniem priorytetyzowanej kolejki FIFO (First In First Out). 
- Logika rozwiązywania kolejek będzie realizowana w ramach tego samego kontekstu ale przez inny model. 

### Uzasadnienie

Typy modeli:
- Capability (Model Kolejek)
- Product (Model Rozwiązywania Kolejek)

Klasy Problemów:
- CRUD (Model Kolejek)
- Integracja (Model Rozwiązywanie Kolejek)

Priorytetyzacja kolejki wynika z potrzeby biznesowej przesuwania klientów w kolejce, natomiast każdy klient który zakolejkuje się na dany termin do konkretnego zasoby otrzyma propozycję rezerwacji w zalezności od kolejności zgłoszenia. Model ten jest łatwo rozwijalny, a dzięki priorytetyzacji gotowy na przyjęcie nowych wymagań funkcjonalnych w tym zakresie. Rozwiązywanie kolejek to problem integracyjny stąd zostanie zrealizowany przez inny model, ale w ramach tego samego kontekstu.

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Brak splątania klas problemów
- Separacje dopowiedzialności
- Testowalność
- W przyszlości możliwe wędzie wydzielenie modelu kolejek w celu reużycia go przez inne modele.

### Negatywne
- Większa złożoność

## Referencje
- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)
- [Key Data Structures Explained](https://levelup.gitconnected.com/queue-deque-and-priority-queue-key-data-structures-explained-1509f133d4c5)

## Data

``15/12/2024``