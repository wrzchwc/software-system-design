# Architecture Decision Record: Model Reservation

## Kontekst
Opis sytuacji lub problemu który wymaga decyzji. 

Przykład:
The system needs to expose functionality to third-party applications. Various integration patterns were evaluated to determine the most scalable and secure approach.

## Decyzja

Przykład:
We will implement a REST API using JSON as the data format, secured with OAuth 2.0 for authentication.

### Uzasadnienie
Wyjaśnij dlaczego podjąłęś taką decyzję

Przykład: 
REST was chosen for its simplicity, wide adoption, and compatibility with existing client libraries. SOAP was rejected due to higher complexity and lack of alignment with team expertise.

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
### Negatywne

Przykład: 
Positive: Broad compatibility with modern tools and clients.
Negative: Increased effort to handle non-standard client requirements manually.

## Referencje

- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)

## Data

``15/12/2024``