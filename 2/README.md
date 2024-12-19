# Wyniki etapu II - Decyzja architektury systemu

- Kamil Bońkowski, 252727
- Szymon Walasik, 283393
- Jakub Wierzchowiec, 252738

## Cel

Dokument przedstawia decyzje i ich uzasadnienie oraz ograniczenia i ważne elementy projektu systemu rozwiązania, które wpływają na jego implementację.

## Cele i ograniczenia architektoniczen

## Mechanizmy architektoniczne

## Widoki architekotniczne

### Widok kontekstowy (C4 Context)

### Scenariusze interakcji (C4 Container)

### Interfejsy integracyjne

## Widok funkcyjny (C4 Component)

## Widok rozmieszczenia (Architekrura Wdrożeniowa)

## Widok informacyjny

### Model informacyjny

### Projekt Bazy Danych

## Widok wytwarzania 

### Frontend

### Backend

## Realizacja przypadku użycia (Przypisanie zasobu do lokacji)

Przypisanie zasobu jest inicjowane przez Location Manager z poziomu klienta Deskly. Polega na przesłaniu zapytania POST zawierającego identyfikatory przypisywanych zasobów.

Przykład zapytania
```
curl --location 'localhost:8080/api/v1/location/6f0a36c6-6814-4e38-b40b-0a65b2f7c3c6/resource/assign' \
--header 'Content-Type: application/json' \
--data '{
    "resourceIds": ["db37fe1a-ab0e-4f9d-8b43-5bf84dcc3648", "7f446172-971e-48c1-b5bc-0538b96dfc20"]
}'
```

Diagram sekwencji

![Diagram sekwencji](./images/sequence-diagram.png)