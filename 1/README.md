# Wyniki etapu I - Modelowanie biznesowe i specyfikacja wymagań

## Model biznesowy

### Lista symboli, oznaczeń i akronimów

### Cel i zakres projektu

Celem projektu jest stworzenie systemu wspomagającego prowadzenie współdzielonych przestrzeni roboczych (ang. co-working area), oraz rezerwację dostępnych w nich zasobów sprzętowych oraz pomieszczeń biurowych. 
Zakres projektu obejmuje:
- Zarządzanie przestrzeniami biurowymi pod kątem inwentaryzacji zasobów, ich dostępnością, a także kosztami rezerwacji
- Obsługa procesu rezerwacji zasobów biurowych
- Obsługa zawierania umów długoterminowego wynajmu zasobów i przestrzeni biurowych

### Strategia biznesowa

Końcowy produkt będzie dystrybuowany w modelu SaaS (ang. software as a service). Docelowi klienci to firmy prowadzące lub chcące rozpocząć działalność co-workingową.

### Słownik pojęć

| Termin | Definicja terminu |
|--------|-------------------|
| Klient „z ulicy” | Klient, który nie chce wiązać się umowami. Osoba fizyczna. Wykorzystanie zasoby naliczane jest po aktualnym cenniku. Potrzebuje dostępu od zaraz na to co jest aktualnie dostępne bez gwarancji dostępności |
| Klient stały | Klient, który ma podpisana umowę z gwarancją cen na zasoby na rok. Osoba fizyczna. Wykorzystanie zasobów naliczane jest po cenniku zawartym w umowie. Potrzebuje dostępu od zaraz na to co jest aktualnie dostępne bez gwarancji dostępności |
| Klient biznesowy | Firma, która ma podpisaną umowę z gwarancją na zasoby i ceny na 12 miesięcy. Klient, który wie jakie zasoby dokładnie potrzebuje i na jaką długość czasu |
| Potencjalny klient | Każda osoba lub firma, która chce rozpocząć korzystanie z przestrzeni co-working
| Właściciel Deskly	| Interesariusze/Inwestorzy w firmie wykorzystującej Deskly jako narzędzie do rezerwacji i zarządzania w ich przestrzeniach co-workingowych |
| Booking Manager | Pracownik Deskly odpowiadający za ciągłość w rezerwacji zasobów. Śledzi wykorzystanie zasobów. Jego rolą jest optymalizacja rezerwacji w celu maksymalizacji zysków i rozwiązywanie problemów związanych z rezerwacjami. Prowadzi negocjacje z klientami biznesowymi i akceptuje lub odrzuca umowy. Może zarządzać jedną lub wieloma lokacjami. |
| Location Manager	| Pracownik Deskly odpowiadający za stan zasobów oferowanych w jednej lub wielu lokacjach. Zleca kupno i konserwację zasobów. Negocjuje i podpisuje umowy z właścicielami nowych lokacji |
| Cennik | |	
| Topologia | |	

## Specyfikacja i analiza wymagań

## Definicja wymagań funkcjonalnych

1. Klient Deskly (wspólne)
    1. Jako klient Deskly chciałbym mieć możliwość zalogować się do swojego konta użytkownika (Personal Account lub Corporate Account)
    2. Jako klient Deskly chciałbym móc wylogować się z konta użytkownika
    3. Jako klient Deskly chciałbym mieć podgląd kodu QR do otwarcia drzwi z poziomu konta użytkownika
2. Klient Deskly "z ulicy" i "stały"
    1. Jako klient Deskly po rezerwacji zasobu chciałbym otrzymać kod QR na maila umożliwiający otwarcie drzwi wejściowych do danej lokacji 24 h przed rozpoczęciem rezerwacji
    2. Jako klient Deskly jeśli zarezerwowałem salkę konferencyjną to chciałbym móc otworzyć salkę konferencyjną tym samym kodem QR co do otwarcia drzwi wejściowych
    3. Jako klient Deskly chciałbym mieć podgląd wszystkich wynajętych zasobów oraz szczegółów każdej z aktywnych rezerwacji
    4. Jako klient Deskly chciałbym mieć możliwość rezerwacji zasobu w dowolnie wybranej lokacji wybierając biurko hotdesk/biuro prywatne/salkę ze schematu ułożenia zasobów w danej lokacji
    5. Jako klient Deskly chciałbym anulować rezerwację na dany zasób, jeśli czas do rozpoczęcia rezerwacji jest dłuży niż 24 h
    6. Jako klient Deskly chciałbym zapisać się na listę oczekujących na zasób w danym terminie (jeśli jest już zarezerwowany przez kogoś innego) gdy czas do rozpoczęcia rezerwacji jest dłuży niż 24 h
    7. Jako klient Deskly chciałbym móc wypisać się z kolejki oczekujących na dany zasób w dowolnym momencie
    8. Jako klient Deskly oczekujący w kolejce na zasób chciałbym zostać poinformowany o rozwiązaniu kolejki i otrzymać propozycję rezerwacji/zakolejkowania się na tożsamy zasób.
    9. Jako klient Deskly chciałbym zostać poinformowany mailowo o zbliżającym się końcu umowy (jeśli to nie jest klient z ulicy).
    10.	Jako klient Deskly chciałbym otrzymać propozycję automatycznego przedłużenia umowy (wraz ze szczegółami o aktualnym cenniku)
3. Klient Deskly Biznesowy
    1. Jako klient biznesowy Deskly chciałbym mieć podgląd wszystkich wynajętych zasobów oraz szczegółów każdej z aktywnych rezerwacji
    2. Jako klient biznesowy Deskly chciałbym, żeby po akceptacji umowy przez Booking Managera wynegocjowane zasoby zostały zarezerwowane w imieniu firmy z datą rozpoczęcia umowy dla wskazanych pracowników firmy (case dla klientów biznesowych) i żeby dla tych pracowników zostały automatycznie wygenerowane konta użytkownika z dostępem do zasobów.
    3. Jako klient biznesowy Deskly chciałbym posiadać konto użytkownika które będzie pozwalać mi jako pracodawcy zarządzać dostępem do zarezerwowanych zasobów dla danych pracowników. Jako klient biznesowy Deskly jeśli wśród zarezerwowanych zasobów znajduje się salkę konferencyjna to chciałbym móc otworzyć salkę konferencyjną (lub moi pracownicy) tym samym kodem QR co do otwarcia drzwi wejściowych
    4. Jako klient biznesowy Deskly chciałby móc stworzyć konto nowemu pracownikowi i nadać mu uprawnienia do korzystania z zarezerwowanych zasobów
    5. Jako klient biznesowy Deskly chciałbym, żeby moi pracownicy nie mogli korzystać z innych zasobów Deskly niż te które zostały wynegocjowane przez firmę
    6. Jako klient biznesowy Deskly chciałbym, żeby moi pracownicy mogli korzystać z wynegocjowanych zasobów bez konieczności rezerwacji i kolejkowania się na te zasoby
4. Location Manager
    1. Jako Location Manager chciałbym móc stworzyć lokację i zdefiniować zasoby w danej lokacji (rodzaj zasobu, zdjęcie, dane seryjne (jeśli jakieś biurko, albo monitor), metraż (jeśli salka) itd.)
    2. Jako Location Manager mogę zlecić konserwacje zasobu.
    3. Jako Location Manager mogę zlecić automatyczną konserwację dla konkretnego typu zasobu (np. po każdym wynajęciu salki 30 min na sprzątanie)
    4. Jako Location Manager mogę wyłączyć dany zasób z użytkowania (nawet jeśli jest aktualnie zarezerwowany)
    5. Jako Location Manager mogę rozwiązać kolejkę oczekującą na zasób
    6. Jako Location Manager chciałbym zdefiniować godziny otwarcia danej lokacji
    7. Jako Location Manager chciałbym zdefiniować cennik zasobów w danej lokacji (dodać/usunąć/zmodyfikować). Zdefiniowany cennik może obowiązywać dopiero od zdefiniowanej daty
    8. Jako Location Manager chciałbym móc zdefiniować topologię zasobów w danej lokacji (dodać/usunąć/modyfikować)
5. Finance Manager
    1. Jako Finance Manager chciałbym mieć podgląd do klientów, którzy nie uregulowali faktury na czas
    2. Jako Finance Manager chciałbym wysłać fakturę do klienta zgodną z rzeczywistym wykorzystaniem przez niego zasobów w danym okresie rozliczeniowym
    3. Jako Finance Manager chciałbym mieć podgląd do wszystkich wystawionych faktur
    4. Jako Finance Manager chciałbym mieć podgląd do cenników, według których naliczane są opłaty w danej lokacji dla danych klientów
    5. Jako Finance Manager chciałbym mieć wgląd do wszystkich zawartych umów
6. Booking Manager
    1. Jako Booking Manager chciałbym przesuwać dowolnych klientów w kolejce na oczekiwany zasób
    2. Jako Booking Manager chciałbym mieć możliwość wysłania do edycji wersji roboczej umowy do wcześniej zweryfikowanego klienta
    3. Jako Booking Manager chciałbym mieć możliwość akceptacji zmian, proponowania zmian w udostępnionej umowie klientowi
    4. Jako Booking Manager chciałbym mieć możliwość akceptacji oraz odrzucenia umowy z potencjalnym klientem.
    5. Jako Booking Manager chciałbym mieć podgląd do obłożenia rezerwacjami w danej lokacji (ile aktualnie jest zarezerwowanych zasobów przez kogo i na jak długo)
    6. Jako Booking Manager chciałbym mieć możliwość przeniesienia rezerwacji klienta na tożsamy zasób.
    7. Jako Booking Manager chciałbym mieć możliwość dodania/usunięcia z puli zasobów klienta biznesowego
7. Potencjalny Klient
    1. Jako potencjalny klient Deskly chciałbym mieć możliwość stworzenia konta użytkownika
    2. Jako potencjalny klient Deskly chciałbym mieć możliwość akceptacji umowy/proponowania zmian w umowie/odrzucenia umowy.
8. Właściciel Deskly
    1. Jako właściciel Deskly chciałbym, żeby klientom, którzy nie uregulowali opłaty po 7 dniach od wystawienia faktury odebrano automatycznie dostęp do zasobów Deskly i rozpoczęto naliczanie odsetek.
    2. Jako właściciel Deskly chciałbym, żeby klient, który zarezerwuje zasób nie mógł anulować rezerwacji, jeśli termin wynosi mniej niż 24 godziny od daty rozpoczęcia rezerwacji.
    3. Jako właściciel Deskly chciałbym, żeby klienci "z ulicy" i klienci "stali" mogli mieć maksymalnie 5 aktywnych rezerwacji jednocześnie.
    4.	Jako właściciel Deskly chciałbym, żeby w momencie, gdy do danego zasobu jest kolejka to, żeby trwała ona aż do momentu, gdy potencjalny rezerwujący (ostatni w kolejce który otrzymał możliwość rezerwacji) nie zaakceptuje oferty rezerwacji.
    5.	Jako właściciel Deskly chciałbym, żeby w momencie, gdy zasób został zarezerwowany, ale jest do niego kolejka to kolejka została rozwiązana, jeśli czas rozpoczęcia rezerwacji będzie mniejszy niż 24 h

## Definicja wymagań niefunkcjonalnych

###	Wymagania systemowe

###	Wydajność

###	Prawo

### Bezpieczeństwo

### Dostępność

### Skalowalność

### Wsparcie

## Model informacyjny (Mapa kontekstów)

## Reguły biznesowe i ograniczenia systemowe

## Prototypy interfejsów użytkownika
