# Wyniki etapu II - Decyzja architektury systemu

- Kamil Bońkowski, 252727
- Szymon Walasik, 283393
- Jakub Wierzchowiec, 252738

## Cel

Dokument przedstawia decyzje i ich uzasadnienie oraz ograniczenia i ważne elementy projektu systemu rozwiązania, które wpływają na jego implementację.

## Cele architektoniczne

- System będzie udostępniać funkcjonalność rezerwacji zasobów biurowych.
- System będzie umozliwiać zarządzanie zasobami biurowymi w zakresie mozliwosci ich rezerwacji oraz inwentaryzacji.
- System będzie umozliwiać zawieranie umów najmu zasobów oraz korzystania z zasobów będących przedmiotem ww. umów.
- System umozliwi kontakt z klientami za pośrednictwem wiadomości e-mail.
- Oczekiwana dostępność systemu to 99% czasu jego działania.
- System powinien być w stanie obsłuzyc zmienną liczbę uzytkowników w ciągu doby, siegajacą 10000 jednoczesnych uzytkowników w godzinach szczytu.
- System zapewni bezpieczeństwo danych wrazliwych oraz zgodność z przepisami RODO.
- Archietktura systemu umozliwi łatwe skalowalnie i rozszerzanie rozwiązania.
- Uytkownicy koncowi będą wchodzić w interakcję z systemem za pośrednictwem intuicyjnych i responsywnych interfejsów uzytkownika.

## Ograniczenia architektoniczne

- System musi działać w oparciu o rozwiązania chmurowe dostarczone przez AWS.
- Wersja MVP powinna powstać w ciągu 12 miesięcy.
- Aplikacja frontendowa musi zostać zaimplementowana we frameworku Angular, z wykorzystaniem języka TypeScript.
- Aplikacje backendowe muszą zostać zaimplementowane we frameworku Spring Boot, z wykorzystaniem języka Java.
- Warstwa backendowa systemu powstanie w architekturze mikroserwisowej.
- Średni czas odpowiedzi dla mikroserwisów nie moze przekraczać 10s.
 
## Mechanizmy architektoniczne

### Architektura Warstowa
Dla problemów klasy CRUD zostanie 

### Architektura Heksagonalna 

### ORM

### Spring Security



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
|Techinika integracji|HTTPS|
|Mechanizm uwierzytelniania|JWT|
|Manipulacja na danych wrazliwych?|nie|
|Strona inicujująca|Deskly FE|
|Model komunikacji|synchroniczny, REST|
|Wydajność|1000 zapytań / s|
|Wolumetria|250 kB / s|
|Wymagana dostępność|99.9%|

|Aspekt|Opis|
|--------|-----------|
|Aplikacja źródłowa|Deskly FE|
|Aplikacja docelowa|Deskly Core|
|Techinika integracji|HTTPS|
|Mechanizm uwierzytelniania|JWT|
|Manipulacja na danych wrazliwych?|tak|
|Strona inicujująca|Deskly FE|
|Model komunikacji|synchroniczny, REST|
|Wydajność|1000 zapytań / s|
|Wolumetria|250 kB / s|
|Wymagana dostępność|99.9%|

|Aspekt|Opis|
|--------|-----------|
|Aplikacja źródłowa|Deskly Location|
|Aplikacja docelowa|Deskly Core|
|Techinika integracji|AWS SDK|
|Mechanizm uwierzytelniania|access key, secret access key|
|Manipulacja na danych wrazliwych?|nie|
|Strona inicujująca|Deskly Location|
|Model komunikacji|asynchroniczny, SQS|
|Wydajność|500 zapytań / s|
|Wolumetria|100 kB / s|
|Wymagana dostępność|99.9%|

|Aspekt|Opis|
|--------|-----------|
|Aplikacja źródłowa|Deskly Core|
|Aplikacja docelowa|Deskly Location|
|Techinika integracji|AWS SDK|
|Mechanizm uwierzytelniania|access key, secret access key|
|Manipulacja na danych wrazliwych?|nie|
|Strona inicujująca|Deskly Core|
|Model komunikacji|asynchorniczny, SQS|
|Wydajność|500 zapytań / s|
|Wolumetria|100 kB / s|
|Wymagana dostępność|99.9%|

|Aspekt|Opis|
|--------|-----------|
|Aplikacja źródłowa|Deskly Core, Deskly Location|
|Aplikacja docelowa|Deskly DB|
|Techinika integracji|JDBC|
|Mechanizm uwierzytelniania|nazwa uytkownika, hasło|
|Manipulacja na danych wrazliwych?|tak|
|Strona inicujująca|Deskly Core, Deskly Location|
|Model komunikacji|synchorniczny|
|Wydajność|500 zapytań / s|
|Wolumetria|100 kB / s|
|Wymagana dostępność|99.9%|

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
