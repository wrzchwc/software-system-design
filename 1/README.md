# Wyniki etapu I - Modelowanie biznesowe i specyfikacja wymagań

## Model biznesowy

### Lista symboli, oznaczeń i akronimów
- SaaS - software as a service

### Cel i zakres projektu

Celem projektu jest stworzenie systemu wspomagającego prowadzenie współdzielonych przestrzeni roboczych (ang. coworking area), oraz rezerwację dostępnych w nich zasobów sprzętowych oraz pomieszczeń biurowych. 
Zakres projektu obejmuje:
- Zarządzanie przestrzeniami biurowymi pod kątem inwentaryzacji zasobów, ich dostępnością, a także kosztami rezerwacji
- Usprawninie procesu rezerwacji zasobów biurowych
- Obsługa zawierania umów długoterminowego wynajmu zasobów i przestrzeni biurowych

### Strategia biznesowa

Końcowy produkt będzie dystrybuowany w modelu SaaS. Docelowi klienci to firmy prowadzące lub chcące rozpocząć działalność coworkingową.

### Słownik pojęć

| Termin | Kontekst | Definicja terminu |
|--------|-----------|-------------------|
| Klient „z ulicy” || Klient, który nie chce wiązać się umowami. Osoba fizyczna. Wykorzystanie zasoby naliczane jest po aktualnym cenniku. Potrzebuje dostępu od zaraz na to co jest aktualnie dostępne bez gwarancji dostępności |
| Klient stały | |Klient, który ma podpisaną umowę z gwarancją cen na zasoby na rok. Osoba fizyczna. Wykorzystanie zasobów naliczane jest po cenniku zawartym w umowie. Potrzebuje dostępu od zaraz na to co jest aktualnie dostępne bez gwarancji dostępności |
| Klient biznesowy | |Firma, która ma podpisaną umowę z gwarancją na zasoby i ceny na 12 miesięcy. Klient, który wie jakie zasoby dokładnie potrzebuje i na jaką długość czasu |
| Potencjalny klient | | Każda osoba lub firma, która chce rozpocząć korzystanie z przestrzeni coworking |
| Booking Manager | |Pracownik Deskly odpowiadający za ciągłość w rezerwacji zasobów. Śledzi wykorzystanie zasobów. Jego rolą jest optymalizacja rezerwacji w celu maksymalizacji zysków i rozwiązywanie problemów związanych z rezerwacjami. Prowadzi negocjacje z klientami biznesowymi i akceptuje lub odrzuca umowy. Może zarządzać jedną lub wieloma lokacjami. |
| Location Manager	| |Pracownik Deskly odpowiadający za stan zasobów oferowanych w jednej lub wielu lokacjach. Zleca kupno i konserwację zasobów. Negocjuje i podpisuje umowy z właścicielami nowych lokacji |
| Contract Manager | |Pracownik Deskly odpowiedzialny za pozyskiwanie nowych klientów. Przygotowuje wersje robocze umów oraz prowadzi negacjacje warunków umów. Podejmuje ostateczną decyzję o podpisaniu umowy z klientem. |
| Cennik | |Zbiór cen wypozyczenia zasobów na daną jednostkę czasu (godzina, doba, miesiąc). Moze byc to cennik biezacy lub zdefinionwany w ramach umowy |
| Cena | | Kwota po której klient będzie kasowany po rozpoczęciu rezerwacji |
| Topologia | |Układ pomieszczeń i biurek w lokacji |
| Lokacja | |Miejsce, w którym mozna korzystać z zarezerwowanych zasobów Deskly |
| Kolejka | |Uporządkowana grupa osób oczekująca na mozliwość zarezerwowania zasobu |
| Dostępność zasobu | |Rozkład dostępności zasobu w czasie |
| Kalendarz | |Sposób reprezentacji dostępności zasobu w czasie |
| Zasób | Lokacja | Sprzęt biurowy lub miejsce pracy (biurko lub sala konferencyjna) |
| Zasób | Dostępność | Dobro które użytkownicy mogą rezerwować jeśli jest dostępny  |
| Zasób | Negocjacja Kontraktu | Dobro podlegające negocjacji |
| Zasób | Kontrola Dostępu | Dobro do którego nadawane lub odbierane są uprawnienia |
| Zasób | Lista Oczekujących | Dobro na którego rezerwację oczekują użytkownicy |
| Szkic umowy | |Przygotowany szkic umowy gotowy do udostępnienia klientowi do negocjacji lub podpisania |
| Negocjacja | | Udostępniony klientowi biznesowemu szkic umowy w trakcie negocjowania warunków |
| Umowa | Kontraktowanie | Podpisane przez klienta warunki korzystania z zasobów oferowanych w Deskly |
| Umowa | Negocjacja kontraktu| Zatwierdzone przez klienta i Contract Managera ostateczne warunki negocjacji 
| Parametr umowy | | Najmniejsza jednostwa podlegająca negocjacji w umowie |
| Oferta | | Złożona propozycja zmiany parametru umowy. Podlega akceptacji |
| Użytkownik | Kontrola dostępu | Osoba której przyznawany lub dobierany jest dostęp do zasobu |
| Użytkownik | Lista Oczekujących | Osoba która oczekuje na rezerwację zasobu |
| Dostęp | | Uprawnienie do korzystania z zasobu w danej lokacji Deskly |
| Rezerwacja Tymczasowa | | Rezerwacja podlagająca akceptacji, anulowaniu, tworzona gdy czas do rezerwacji zasobu jest dłuższy niż 24h, oferowana jest klientom oczekującym w kolejce. Blokuje zasób |
| Rezerwacja | | Rezerwacja po akcpetacji Rezerwacji Tymczasowej (manualnej lub automatycznej gdy czas do rozpoczęcia rezerwacji mniejszy niż 24h). Wiąże się z rozpoczęciem naliczania opłat, nie można jej przenieść ani anulować. |
| Opłata | | Kwota do zapłaty przez klienta wynikająca z czasu rezerwacji konkretnego zasobu |
| Faktura | | Dokument wystawiany klientowi w celu zapłaty należności za dany okres rozliczeniowy |
| Zarobek | | Kwota zarobiona w danym okresie rozliczeniowym w danej lokacji Deskly |
| Dłużnik | | Klient który nie opłacił faktury po 10 dniach od momentu jej wystawienia |

## Specyfikacja i analiza wymagań

## Definicja wymagań funkcjonalnych

1. Klient Deskly (wspólne)
    1. Jako klient Deskly chciałbym mieć możliwość zalogować się do/wylogować się ze swojego konta użytkownika.
    2. Jako klient Deskly chciałbym mieć podgląd kodu QR do otwarcia drzwi z poziomu konta użytkownika.
2. Klient Deskly "z ulicy" i stały
    1. Jako klient Deskly po rezerwacji zasobu chciałbym otrzymać kod QR na maila umożliwiający otwarcie drzwi wejściowych do danej lokacji 24 godziny przed rozpoczęciem rezerwacji.
    2. Jako klient Deskly chciałbym mieć podgląd wszystkich wynajętych zasobów oraz szczegółów każdej z aktywnych rezerwacji.
    3. Jako klient Deskly chciałbym mieć możliwość rezerwacji zasobu w dowolnie wybranej lokacji.
    4. Jako klient Deskly chciałbym podczas rezerwacji biurka lub sali konferencyjnej być w stanie wybrać interesujący mnie zasób korzystając ze schematu topologii lokacji.
    5. Jako klient Deskly chciałbym zapisać się na listę oczekujących na zasób w danym terminie (jeśli jest już zarezerwowany przez kogoś innego), gdy czas do rozpoczęcia rezerwacji jest dłuższy niż 24 godziny.
    6. Jako klient Deskly chciałbym móc wypisać się z kolejki oczekujących na dany zasób w dowolnym momencie.
    7. Jako klient Deskly oczekujący w kolejce na zasób chciałbym zostać poinformowany o rozwiązaniu kolejki i otrzymać propozycję rezerwacji/zakolejkowania się na tożsamy zasób.
3. Klient stały
    1. Jako klient stały chciałbym zostać poinformowany mailowo o zbliżającym się końcu umowy.
    2. Jako klient stały chciałbym otrzymać propozycję automatycznego przedłużenia umowy wraz ze szczegółami o aktualnym cenniku. 
4. Klient Deskly Biznesowy
    1. Jako klient biznesowy Deskly chciałbym mieć podgląd wszystkich wynajętych zasobów oraz szczegółów każdej z aktywnych rezerwacji.
    2. Jako klient biznesowy Deskly chciałbym, żeby po akceptacji umowy przez Contract Managera wynegocjowane zasoby zostały zarezerwowane w imieniu firmy z datą rozpoczęcia umowy dla wskazanych pracowników firmy i żeby dla tych pracowników zostały automatycznie wygenerowane konta użytkownika z dostępem do zasobów.
    3. Jako klient biznesowy Deskly chciałbym posiadać konto użytkownika, które będzie pozwalać mi jako pracodawcy zarządzać dostępem do zarezerwowanych zasobów dla pracowników. 
    4. Jako klient biznesowy Deskly chciałbym móc stworzyć konto nowemu pracownikowi i nadać mu uprawnienia do korzystania z zarezerwowanych zasobów.
5. Location Manager
    1. Jako Location Manager chciałbym móc dodać lokację i zdefiniować zasoby w danej lokacji (rodzaj zasobu, zdjęcia, dane seryjne (w przyadku biurek oraz sprzętu audio-wideo), liczba miejsc (w przypadku sali konferencyjnej), opis).
    2. Jako Location Manager mogę zlecić konserwację zasobu.
    3. Jako Location Manager mogę zlecić automatyczną konserwację dla konkretnego typu zasobu (np. po każdym wynajęciu sali 30 minut na sprzątanie)
    4. Jako Location Manager mogę wyłączyć dany zasób z użytkowania (nawet jeśli jest aktualnie zarezerwowany).
    5. Jako Location Manager chciałbym zdefiniować godziny otwarcia danej lokacji.
    6. Jako Location Manager chciałbym móc zdefiniować topologię zasobów w danej lokacji (dodać/usunąć/modyfikować)
    7. Jako Location Manager chiałbym mieć możliwość aktualizacji danych lokalizacji oraz dostępnych zasobów.
6. Contract Manager
    1. Jako Contract Manager chciałbym mieć możliwość wysłania do edycji wersji roboczej umowy do wcześniej zweryfikowanego klienta.
    2. Jako Contract Manager chciałbym mieć możliwość akceptacji oraz proponowania zmian w umowie udostępnionej klientowi.
    3. Jako Contract Manager chciałbym mieć możliwość akceptacji oraz odrzucenia umowy z potencjalnym klientem.     
7. Finance Manager
    1. Jako Finance Manager chciałbym mieć podgląd do klientów, którzy nie uregulowali faktury na czas.
    2. Jako Finance Manager chciałbym wysłać fakturę do klienta zgodną z rzeczywistym wykorzystaniem przez niego zasobów w danym okresie rozliczeniowym.
    3. Jako Finance Manager chciałbym mieć podgląd do wszystkich wystawionych faktur.
    4. Jako Finance Manager chciałbym mieć podgląd do cenników, według których naliczane są opłaty w danej lokacji dla danych klientów.
    5. Jako Finance Manager chciałbym mieć wgląd do wszystkich zawartych umów.
8. Booking Manager
    1. Jako Booking Manager chciałbym przesuwać dowolnych klientów w kolejce na oczekiwany zasób.
    2. Jako Booking Manager chciałbym mieć podgląd do obłożenia rezerwacjami w danej lokacji (ile aktualnie jest zarezerwowanych zasobów przez kogo i na jak długo).
    3. Jako Booking Manager chciałbym mieć możliwość przeniesienia rezerwacji klienta na tożsamy zasób.
    4. Jako Booking Manager chciałbym mieć możliwość dodania/usunięcia z puli zasobów klienta biznesowego.
    5. Jako Booking Manager mogę rozwiązać kolejkę oczekującą na zasób.
9. Potencjalny Klient
    1. Jako potencjalny klient Deskly chciałbym mieć możliwość stworzenia konta użytkownika.
    2. Jako potencjalny klient Deskly chciałbym mieć możliwość akceptacji umowy/proponowania zmian w umowie/odrzucenia umowy.

## Definicja wymagań niefunkcjonalnych

###	Wymagania systemowe
1. System działa na urządzeniach z systemem operacyjnym Linux (Ubuntu od wersji 20.04 LTS), MacOS (od wersji 15.0), Windows (Windows 10, Windows 11) oraz przeglądarkach internetowych (Chrome, Frirefox, Safari, Edge)
2. System działa na urządzeniach mobilnych z systemem operacyjnym Android(od wersji 11.0) oraz iOS (od wersji 15.0)
3. System powinien obsługiwać bazę danych o wysokiej wydajności, wspierającą relację pomiędzy obiektami (PostgreSQL, Oracle, MSSQL, MySQL)
4. Wszystkie usługi powinny działać w chmurze AWS i wspierać mechanizmy auto-skalowania
5. System powinien integrować się z zewnętrznymi dostawcami poczty elektorniczne oraz systemami kontroli dostępu (generowanie kodów QR)

###	Wydajność
1. System powinien być w stanie obsłużyć jednoczesne logowanie i rezerwacje dokonywane przez co najmniej 10.000 użytkowników (1000 zapytań na sekundę przy założeniu że użytkownik wykonuje zapytanie średnio co 10 sekund) 
2. Czas odpowiedzi na operacje związane z rezerwacjami i dostpem od zasobów nie powinien przekraczać 2 sekund
3. Czas wyszukiwania zasobów oraz generowania raporów finansowych powinen trwać poniżej 3 sekund

###	Prawo
1. System powinien spełniać regulację GDPR (General Data Protection Regulation) w zakresie przetwarzania, przechowywania i usuwania danych osobowych użytkowników
2. Mysi istnieć możliwość prowadzenia logów audytowych dla wszystkich danych związanych z negocjacją umowy oraz danych związanych z rezerwacjami

### Bezpieczeństwo
1. Dane osobowe i dane związane z rezerwacjami powinny być szyfrowane w bazie danych oraz podczas przesyłania (TLS)

### Dostępność
1. System powinie mieć dostępność na poziomie minimum 99,9%
2. W przypadku awarii, system powinien być w stanie przywrócić dostępność w ciągu maksymalnie 1h
3. Dopuszczalna jest spójność ostateczna na replikach baz danych w przypadkach takich jak:
    1.  Informacje o dostępnych zasobach
    2.  Podgląd szczegółów rezerwacji
    3.  Zarządzanie kolejkami oczekujączych na zasoby
    4.  Informacje o cennikach
    5.  Powiedomienia o zbliżających się końcach umów

### Skalowalność
- System powinien automatycznie skalować się w górę lub w dół w zależności od liczby aktywnych użytkowników oraz zapotrzebowania na zasoby
- Skalowanie horyzontalne owinno umożliwiwać dodawania nowych instancji w przypadku dużego obciążenia i równomiernie dystrybułować do nich ruch
- Architektura wdrożeniowa systemu poiwnn być podzielona na mikroserwisy umożliwiając niezależne skalowanie krytycznych usług (np. obsługa rezerwacji, wysyłanie kodów QR, rozliczenia)

### Wsparcie
- System powinien mieć wdrożony proces wsparcia technicznego dla klientów z możliwiwością zgłoszeń przez aplikację
- Zautomatyzowane monitorowanie wydajności i dostępności aplikacji oraz natychmiastowe powiadomienia dla zespołu wsparcia w przypadku wykrycia anomalii

## Mapa kontekstów

![Screenshot 2024-11-08 at 12 10 22](https://github.com/user-attachments/assets/5823c825-4018-4be6-b901-20f1462f7d9a)

[Mapa kontekstów na Miro](https://miro.com/app/board/uXjVNLyFXXE=/?share_link_id=140829908257&shareablePresentation=1) 

### Definicja relacji pomiędzy kontekstami
- Upstream
    - Dostawca inforamcji, zachowń, konceptów, zmian do kontestów które są z nim w realcji Downstream
    - Ma większą kontrolę w relacji Upstream - Downstream ponieważ nie jest zależny od Downstream
  
- Downastream
    - Kontekst zależy od informacji z kontektu Upstream
    - Nie wpływa na kontekst który jest z nim relacji Upstream

### Definicja Wzorców mapowania kontekstów
- OHS (Open Host Service)
    - Oferuje wspólny model i wspólną funkcjonalność dla wielu zastosowań
    - Może być rozumiany jako publiczne API dla wielu konsumentów
 
- Customer - Supplier
    - Wzorzez organizacyjny, nie techniczny 
    - Typ relacji gdzie downastream może mieć wpływ na upstream
    - Wymagania przekazane przez downstream powinny być wzięte pod uwagę przez upstream team

- PL (Published Language)
    - Dobrze udokumentowany język współdzielony przez konteksty
    - Każdy kontekst może tłumaczyć na jego język
 
- Partnership
    - Wzorzec organizacyjny, nie techniczny
    - Polega na sytuacji gdzie dwa zespoły wspólnie koordunują procesem i tylko rezem mogą dostarczać wartość biznesową
 
- ACL (Anti-Corruption Layer)
    - Strefa zgniotu - propagacja logiki do innego modelu w celu jej przemapowania na język tego modelu
    - Miejsce przetłumaczenia innego modelu na swój tym samym redukcja ryzyka zmiany do jednej cienkiej warstwy
    - Często stosowany żeby odgrodzić logikę modelu od modelu legacy lub po prostu logiki innego modelu
 


## Reguły biznesowe i ograniczenia systemowe

- Klienci którzy nie uregulowali opłaty po 7 dniach od wystawienia faktury, tracą dostęp do zasobów Deskly i rozpoczyna się naliczanie odsetek od niezapłaconej faktury.
- Klient otrzymuje przypomnienie o opłaceniu faktury, 3 dni po dacie jej wystawienia.
- Klient (stały lub "z ulicy"), który zarezerwuje zasób nie może anulować rezerwacji, jeśli do rozpoczęcia rezerwacji pozostało mniej niż 24 godziny. W przeciwnym przypadku anulowanie rezerwacji jest mozliwe.
- Klienci "z ulicy" i klienci "stali" mogą mieć maksymalnie 5 aktywnych rezerwacji jednocześnie.
- Klienci biznesowi nie mogą rezerwować innych zasobów i kolejkować się na inne zasoby niż te które zostały do im przypisane w wyniku negocjacji umowy.
- Kolejka do danego zasobu trwa do momentu, gdy potencjalny rezerwujący (ostatni w kolejce który otrzymał możliwość rezerwacji) nie zaakceptuje oferty rezerwacji.
- Kolejka do zarezerwoanego zasobu zostaje rozwiązana jezeli akceptacja rezerwacji następuje mniej niz 24 godziny przed planowaną datą rezerwacji.
- Pracownicy klienta biznesowego Deskly nie muszą rezerwować zasobów, aby z nich skorzystać.
- Pracownicy klienta biznesowego Deskly nie mogą korzystać z innych zasobów, niz wynegocjowane przez firmę.
- Kod QR umozliwiający wejście do lokacji umozliwia wejście do sali konferencyjnej jezeli jest ona przedmiotem rezerwacji lub umowy.

## Prototypy interfejsów użytkownika

### Jako klient Deskly chciałbym mieć możliwość zalogować się do/wylogować się ze swojego konta użytkownika.

Mapa nawigacyjna

![Auth](./images/navigation-maps/auth.png)

Strona domowa

![Strona domowa](./images/user-interfaces/home-page.png)

Strona logowania

![Strona logowania](./images/user-interfaces/sign-in-page.png)

Ekran domowy (szablon)

![Ekran domowy](./images/user-interfaces/sign-out.png)

### Jako potencjalny klient Deskly chciałbym mieć możliwość stworzenia konta użytkownika.

Mapa nawigacyjna

![Register](./images/navigation-maps/register.png)

Panel rejestracji
![Panel rejestracji](./images/user-interfaces/sign-up-page.png)

### Jako klient Deskly po rezerwacji zasobu chciałbym otrzymać na maila kod QR umożliwiający otwarcie drzwi wejściowych do danej lokacji 24 godziny przed rozpoczęciem rezerwacji.

Przykład wiadomości e-mail

![E-mail kod QR](./images/user-interfaces/email-qr.png)

### Jako klient stały chciałbym zostać poinformowany mailowo o zbliżającym się końcu umowy.
### Jako klient stały chciałbym otrzymać propozycję automatycznego przedłużenia umowy wraz ze szczegółami o aktualnym cenniku.

Mapa nawigacyjna

![Przedłuzenie kontraktu](./images/navigation-maps/contract-extension.png)

Przykład wiadomości e-mail

![E-mail koniec umowy](./images/user-interfaces/contract-end-email.png)

Ekran przedłuzenia umowy

![Ekran przedłuzenia umowy](./images/user-interfaces/contract-extension.png)

### Jako klient Deskly chciałbym mieć podgląd wszystkich wynajętych zasobów oraz szczegółów każdej z aktywnych rezerwacji.
### Jako klient Deskly chciałbym mieć podgląd kodu QR do otwarcia drzwi z poziomu konta użytkownika.

Mapa nawigacyjna

![Rezerwacje](./images/navigation-maps/bookings.png)

Lista rezerwacji

![List rezerwacji](./images/user-interfaces/reservations-list-page.png)

Podgląd rezerwacji

![Podgląd rezerwacji](./images/user-interfaces/booking-details.png)

### Jako klient Deskly chciałbym mieć możliwość rezerwacji zasobu w dowolnie wybranej lokacji.
### Jako klient Deskly chciałbym podczas rezerwacji biurka lub sali konferencyjnej być w stanie wybrać interesujący mnie zasób korzystając ze schematu topologii lokacji.
### Jako klient Deskly chciałbym zapisać się na listę oczekujących na zasób w danym terminie (jeśli jest już zarezerwowany przez kogoś innego), gdy czas do rozpoczęcia rezerwacji jest dłuży niż 24 godziny.

Mapa nawigacyjna

![Rezewacja zasobu](./images/navigation-maps/booking.png)

Strona rezerwacji

![Strona rezerwacji zasobu](./images/user-interfaces/booking-page.png)

Modal kolejkowania się

![Modal kolejkowwania się](./images/user-interfaces/enqueue-modal.png)

### Jako klient Deskly chciałbym móc wypisać się z kolejki oczekujących na dany zasób w dowolnym momencie.

Mapa nawigacyjna

![Kolejki na zasoby](./images/navigation-maps/queues.png)

Kolejki na zasoby

![Kolejki](./images/user-interfaces/queues-page.png)

Podgląd zakolejkowanego zasobu

![Podgląd zakolejkowanego zasobu](./images/user-interfaces/queue-item.png)

### Jako klient Deskly oczekujący w kolejce na zasób chciałbym zostać poinformowany o rozwiązaniu kolejki i otrzymać propozycję rezerwacji/zakolejkowania się na tożsamy zasób.

Mapa nawigacyjna

![Alternatywna rezerwacja](./images/navigation-maps/alternate-booking.png)

Przykład wiadomości e-mail

![Kolejka rozwiązana](./images/user-interfaces/queue-cancelled-email.png)

Alternatywa rezerwacja

![Alternatywna rezerwacja](./images/user-interfaces/alternate-booking.png)

### Jako Location Manager chciałbym móc dodać lokację i zdefiniować zasoby w danej lokacji (rodzaj zasobu, zdjęcia, dane seryjne (w przyadku biurek oraz sprzętu audio-wideo), liczba miejsc (w przypadku sali konferencyjnej), opis).
### Jako Location Manager chciałbym zdefiniować godziny otwarcia danej lokacji.

![Add location dialog](https://github.com/user-attachments/assets/2ad35499-2453-4a74-a25b-ca813a0400ae)
![Add hot desk dialog](https://github.com/user-attachments/assets/54832443-811b-4d73-a5cb-86fdeb10a563)
![Add conference room dialog](https://github.com/user-attachments/assets/efe69261-00d4-48cd-b255-bbd3d84eab9d)
![Add audio device dialog](https://github.com/user-attachments/assets/098eca8a-5cf5-4cfb-ba3b-74e96ce2fe0f)
![Add private desk dialog](https://github.com/user-attachments/assets/58751d0a-5b8c-4ed7-920a-323afb7971bb)
![Add private room dialog](https://github.com/user-attachments/assets/3d98f72c-2276-49b2-a3bd-12321a3196c1)

### Jako Location Manager mogę zlecić konserwację zasobu.
### Jako Location Manager mogę zlecić automatyczną konserwację dla konkretnego typu zasobu (np. po każdym wynajęciu sali 30 minut na sprzątanie)
### Jako Location Manager mogę wyłączyć dany zasób z użytkowania (nawet jeśli jest aktualnie zarezerwowany).

![Order maintenance](https://github.com/user-attachments/assets/76e29ad1-fc7e-4bca-a2e0-0633bb5f49b1)
![Order maintenance dialog](https://github.com/user-attachments/assets/cc1241c8-c49b-4888-8052-c4413ce1887e)

### Jako Location Manager chciałbym móc zdefiniować topologię zasobów w danej lokacji (dodać/usunąć/modyfikować)
### Jako Location Manager chiałbym mieć mozliwosc aktualizacacji danych lokalizacji oraz dostępnych zasobów.

![Edit location (2)](https://github.com/user-attachments/assets/9133f42e-5923-4cf0-a455-a0b437331768)
![Resources in location](https://github.com/user-attachments/assets/493005a1-11fb-411a-95b7-a68c0fc499e6)

Mapa nawigacyjna

![LocationManager drawio (1)](https://github.com/user-attachments/assets/df4bf010-c895-4477-b0dd-ff7549ed3de8)

### Jako Contract Manager chciałbym mieć możliwość wysłania do edycji wersji roboczej umowy do wcześniej zweryfikowanego klienta.
### Jako Contract Manager chciałbym mieć możliwość akceptacji oraz proponowania zmian w umowie udostępnionej klientowi.
### Jako Contract Manager chciałbym mieć możliwość akceptacji oraz odrzucenia umowy z potencjalnym klientem.

![Draft version of the contract](https://github.com/user-attachments/assets/73e4bcdc-0935-4bcd-b40d-6e4671b2acb7)

Mapa nawigacyjna

![ContractManager drawio](https://github.com/user-attachments/assets/269610bd-4fd5-4c98-8183-7bb0e956989d)

### Jako Finance Manager chciałbym mieć podgląd do klientów, którzy nie uregulowali faktury na czas.
### Jako Finance Manager chciałbym wysłać fakturę do klienta zgodną z rzeczywistym wykorzystaniem przez niego zasobów w danym okresie rozliczeniowym.

![List of clients](https://github.com/user-attachments/assets/69bd9e3f-421a-42d1-b38a-ca542ea38652)

### Jako Finance Manager chciałbym mieć podgląd do wszystkich wystawionych faktur.

![List of invoices](https://github.com/user-attachments/assets/3f7e45e6-4005-4bf0-b4c6-a99c930423b4)

### Jako Finance Manager chciałbym mieć podgląd do cenników, według których naliczane są opłaty w danej lokacji dla danych klientów.

![Costs preview](https://github.com/user-attachments/assets/80f0786f-dcf6-430b-98d3-8e7be0559eac)

### Jako Finance Manager chciałbym mieć wgląd do wszystkich zawartych umów.

![List od contracts](https://github.com/user-attachments/assets/ad18204d-1cbd-42a4-9cf5-bbbd4f0241c3)

Mapa nawigacyjna

![FinanseManager drawio](https://github.com/user-attachments/assets/d05a599d-7e86-4b6e-b64b-7555cf224cdf)

### Jako Booking Manager chciałbym przesuwać dowolnych klientów w kolejce na oczekiwany zasób.

![Queue for resource](https://github.com/user-attachments/assets/0b829526-53ea-498e-ba7f-fda2104d3b8a)

### Jako Booking Manager chciałbym mieć podgląd do obłożenia rezerwacjami w danej lokacji (ile aktualnie jest zarezerwowanych zasobów przez kogo i na jak długo).

![List of booked resources](https://github.com/user-attachments/assets/76414cf6-28b7-4315-bcc1-c669bdc69155)

### Jako Booking Manager chciałbym mieć możliwość przeniesienia rezerwacji klienta na tożsamy zasób.
### Jako Booking Manager chciałbym mieć możliwość dodania/usunięcia z puli zasobów klienta biznesowego.

![List of business clients (1)](https://github.com/user-attachments/assets/fe9dcefa-363c-46be-a165-5df038bce244)
![List of resources for client (1)](https://github.com/user-attachments/assets/ce63f4b1-3263-440c-9bc0-21ad60040a12)
![Add resource for client dialog](https://github.com/user-attachments/assets/a2cb6c37-ef56-44ed-b111-8d8ecb2eb283)

### Jako Booking Manager mogę rozwiązać kolejkę oczekującą na zasób.

![List of queued resources](https://github.com/user-attachments/assets/1d217779-a866-41de-9dcd-ed4631df88f6)

Mapa nawigacyjna

![BookingManager drawio](https://github.com/user-attachments/assets/698070d9-e2ed-4640-8e1e-7fd2011bcd0f)

### Jako klient biznesowy Deskly chciałbym móc stworzyć konto nowemu pracownikowi i nadać mu uprawnienia do korzystania z zarezerwowanych zasobów.

Mapa nawigacyjna

![Pracownicy](./images/navigation-maps/employees.png)

Wszyscy pracownicy

![Pracownicy](./images/user-interfaces/employees-list.png)

Nowy pracownik

![Nowy pracownik](./images/user-interfaces/employee-enrollment.png)


### Jako klient biznesowy Deskly chciałbym posiadać konto użytkownika, które będzie pozwalać mi jako pracodawcy zarządzać dostępem do zarezerwowanych zasobów dla pracowników.
### Jako klient biznesowy Deskly chciałbym mieć podgląd wszystkich wynajętych zasobów oraz szczegółów każdej z aktywnych rezerwacji.

Mapa nawigacyjna

![Zasoby firmowe](./images/navigation-maps/enterprise-resources.png)

Zarezerwowane zasoby

![Zarezerwowane zasoby](./images/user-interfaces/booked-resources.png)

Zarezerwowany zasób

![Zarezerwowany zasób](./images/user-interfaces/booked-resouce.png)
