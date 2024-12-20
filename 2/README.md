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
![structurizr-SystemContext](https://github.com/user-attachments/assets/da262738-292d-43cf-ba15-03f70b78c461)

### Scenariusze interakcji (C4 Container)
![structurizr-Container-001](https://github.com/user-attachments/assets/e7d28b4e-aae6-441e-a1d4-c07a8b7ccf8c)



### Interfejsy integracyjne

|Aspekt|Opis|
|--------|-----------|
|Aplikacja źródłowa|Deskly FE|
|Aplikacja docelowa|Deskly Location|
|Techinika integracji||
|Mechanizm uwierzytelniania||
|Manipulacja na danych wrazliwych?||
|Strona inicujująca||
|Model komunikacji||
|Wydajność||
|Wolumetria||
|Wymagana dostępność||

## Widok funkcyjny (C4 Component)
![structurizr-Component-001 (1)](https://github.com/user-attachments/assets/36f9e1bf-a9a1-4deb-bf15-8b0a395fba53)
![structurizr-Component-002](https://github.com/user-attachments/assets/50619c36-690b-4ad8-aeee-d7a60bba9579)

## Widok rozmieszczenia (Architekrura Wdrożeniowa)

![image](https://github.com/user-attachments/assets/8854b070-17c7-459a-bbc0-40e0458714e8)

## Widok informacyjny

### Model informacyjny

- Deskly Core
![Model_Informacyjny1 drawio](https://github.com/user-attachments/assets/bdb216ec-4ee0-4529-af15-78f6e6cd4836)

- Deskly Location
![Model_Informacyjny2 drawio](https://github.com/user-attachments/assets/95bb310a-07d1-42f1-bf9d-da256896c141)

### Projekt Bazy Danych

## Widok wytwarzania 

### Frontend

Aplikacja frontendowa zostanie zaimplementowana we frameworku Angular 19. Do zbudowania aplikacji zostanie wykorzystane zostanie narzędzie nx. Aplikacja została podzielona na moduły reprezentujące domeny grupujące funkcjonalności udostępniane uzytkownikom koncowym. Centralnym punktem aplikacji będzie katalog `src` zawierający pliki `index.html` (definiuje wstępną struktruę DOM) oraz  `main.ts` (od tego pliku rozpoczyna sie ładowanie logiki aplikacji). Kazdy z modułów ma zblizoną strukturę obejmującę 1 - 4 katalogów ze zbioru (`feature` - komponenty smart, `ui` - komponenty prezentacyjne, `data` - serwisy biznesowe, zarządzanie stanem, komunikacja z backendem oraz `domain` - modele danych). Moduły są leniwie ładowane, co umozliwia optymalizację wczytywania aplikacji, poprzez ładowanie jedynie tych fragmentów aplikacji, które są potrzebne danemu uzytkownikowi. Ponizej zamieszczono diagram prezentujący widok wytwarzania aplikacji frontendowej.

![Widok wytwarzania](./images/fe.png)

### Backend

## Realizacja przypadku użycia (Przypisanie zasobu do lokacji)

Przypisanie zasobu jest inicjowane przez Location Managera z poziomu klienta Deskly. Polega na przesłaniu zapytania POST zawierającego identyfikatory przypisywanych zasobów.

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
