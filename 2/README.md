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
- Uytkownicy końcowi będą wchodzić w interakcję z systemem za pośrednictwem intuicyjnych i responsywnych interfejsów uzytkownika.

## Ograniczenia architektoniczne

- System musi działać w oparciu o rozwiązania chmurowe dostarczone przez AWS.
- Wersja MVP powinna powstać w ciągu 12 miesięcy.
- Aplikacja frontendowa musi zostać zaimplementowana we frameworku Angular, z wykorzystaniem języka TypeScript.
- Aplikacje backendowe muszą zostać zaimplementowane we frameworku Spring Boot, z wykorzystaniem języka Java.
- Warstwa backendowa systemu powstanie w architekturze mikroserwisowej.
- Średni czas odpowiedzi dla mikroserwisów nie moze przekraczać 10s.

## Decyzje i ich uzasadnienia

| Drivery architektoniczne | Decyzje                                                                                     |
| ------------------------ | ------------------------------------------------------------------------------------------ |
| `asdf`, `asdf`           | [`D/01` Architektura heksagonalna](#architektura-heksagonalna)                             |
| `asdf`, `asdf`           | [`D/02` Architektura warstwowa](#architektura-warstwowa)                                   |
| `asdf`, `asdf`           | [`D/03` Architektura mikroserwisowa](#architektura-mikroserwisowa)                         |
| `asdf`, `asdf`           | [`D/04` Optimistic Locking](#architektura-mikroserwisowa)                                  |
| `asdf`, `asdf`           | [`D/05` Wzorzec Agregat](#wzorzec-agregat)                                                 |
| `asdf`, `asdf`           | [`D/06` Wzorzec Fasady](#wzorzec-fasady)                                                   |
| `asdf`, `asdf`           | [`D/07` Strkuktury Dużej Skali](#struktury-dużej-skali)                                    |
| `asdf`, `asdf`           | [`D/08` Load Balancing](#load-balancing)                                                   |
| `asdf`, `asdf`           | [`D/09` Amazon Simple Queue Service](#amazon-simple-queue-service)                         |
| `asdf`, `asdf`           | [`D/10` Wzorzez API Gateway](#wzorzec-api-gateway)                                         |
| `asdf`, `asdf`           | [`D/11` Sieć wewnętrzna VPC](#siećwewnętrzna-vpc)                                          |
| `asdf`, `asdf`           | [`D/12` Oddzielne bazy danych dla mikroserwisów](#oddzielne-bazy-danych-dla-mikroserwisów) |
| `asdf`, `asdf`           | [`D/13` Amazon S3 Bucket](#amazon-s3-bucket)                                               |
| `asdf`, `asdf`           | [`D/14` Nat Gateway](#nat-gateway)                                                         |
| `asdf`, `asdf`           | [`D/15` Amazon Lambda](#amazon-lambda)                                                     |
| `asdf`, `asdf`           | [`D/16` Internet Gateway](#internet-gateway)                                               |
| `asdf`, `asdf`           | [`D/17` Autoryzacja z wykorzystaniem JWT](#autoryzacja-z-wykorzystaniem-jwt)               |
| `asdf`, `asdf`           | [`D/17` Wdrożenie w chmurze AWS](#wdrożenie-w-chmurze-aws)                                 |



## Mechanizmy Architektoniczne

### Infrastrukturalne

#### Wdrożenie w chmurze AWS
Zagadnienie: Wybór infrastruktury wdrożeniowej stanowi strategiczne wyzwanie, które wpływa na późniejszą wydajność i elastyczność systemu. Kluczowe są tutaj takie kwestie, jak skalowalność, optymalizacja kosztów oraz zdolność do adaptacji wobec zmieniających się wymagań biznesowych. Tradycyjna infrastruktura lokalna (on-premise) często ogranicza możliwości szybkiej reakcji na te zmiany, co rodzi potrzebę poszukiwania bardziej elastycznych rozwiązań, takich jak infrastruktura chmurowa.

Rozwiązanie: W ramach projektu postanowiono wykorzystać chmurę Amazon Web Services (AWS) jako podstawową platformę wdrożeniową. Decyzja ta opierała się na analizie kluczowych wymagań projektu, takich jak szybka dostępność zasobów, globalny zasięg, a także szeroki wachlarz usług umożliwiających zaawansowaną personalizację infrastruktury.
AWS pozwala na elastyczne zarządzanie zasobami w oparciu o model „pay-as-you-go”. Dzięki temu unika się kosztów związanych z nadmiarową infrastrukturą, co jest szczególnie istotne w projektach, które charakteryzują się dużymi wahaniami obciążenia. Ponadto, AWS oferuje zaawansowane funkcje zabezpieczeń oraz dostępność na poziomie globalnym.

Różnice między podejściami wdrożeniowymi:

- Infrastruktura lokalna (on-premise):
Wybór infrastruktury lokalnej zapewnia pełną kontrolę nad danymi i fizycznym sprzętem, co bywa kluczowe w przypadku organizacji o szczególnych wymogach bezpieczeństwa. Jednak wdrożenie tego modelu wiąże się z wysokimi kosztami początkowymi, koniecznością zatrudnienia wykwalifikowanego zespołu IT oraz ograniczeniami w elastyczności skalowania.

- Chmura publiczna (AWS):
Z kolei infrastruktura oparta na chmurze publicznej umożliwia dynamiczne skalowanie w zależności od potrzeb, co pozwala na optymalizację kosztów i zasobów. AWS daje także dostęp do globalnej sieci centrów danych, co minimalizuje opóźnienia i zwiększa komfort użytkowników końcowych. Chmura publiczna eliminuje również konieczność zakupu sprzętu oraz ponoszenia kosztów jego utrzymania.

### Porównanie dostawców chmurowych  

| **Dostawca**               | **Zalety**                                                                                          | **Wady**                                                                                       |
| -------------------------- | -------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| `Amazon Web Services (AWS)`| - Największy wybór usług<br>- Globalna sieć centrów danych<br>- Dojrzały ekosystem i renoma<br>- Wysoka niezawodność i bezpieczeństwo<br>- Elastyczne ceny w modelu „pay-as-you-go” | - Brak pełnego wsparcia dla hybrydowych rozwiązań<br>- Kompleksowość może utrudnić początkową konfigurację |
| `Microsoft Azure`          | - Doskonała integracja z ekosystemem Microsoft (np. Active Directory, Office 365)<br>- Wsparcie dla hybrydowej infrastruktury<br>- Szerokie możliwości PaaS<br>- Popularność w środowiskach korporacyjnych | - Mniejszy wybór usług w porównaniu z AWS<br>- Mniejsza liczba globalnych centrów danych<br>- Koszty licencji Microsoft mogą zwiększać wydatki |
| `Google Cloud (GCP)`       | - Lider w zakresie big data i uczenia maszynowego (BigQuery, TensorFlow)<br>- 100% infrastruktury zasilanej odnawialną energią<br>- Najlepsze wsparcie dla Kubernetes<br>- Wysoka jakość narzędzi analitycznych | - Mniejszy zasięg globalny niż AWS i Azure<br>- Skupienie na big data, co może ograniczać przydatność w innych środowiskach<br>- Mniej popularny na rynku korporacyjnym |

Kluczowe cechy AWS:
AWS oferuje setki usług, takich jak przechowywanie danych (Amazon S3), maszyny wirtualne (EC2), systemy bazodanowe (RDS) oraz narzędzia do analizy danych. Dodatkowo, platforma wyróżnia się:

- Globalnym zasięgiem: AWS posiada centra danych w wielu regionach świata, co zapewnia niskie opóźnienia i wysoką niezawodność.
- Elastycznością: Użytkownicy mogą łatwo dostosowywać zasoby do zmieniających się wymagań.
- Bezpieczeństwem: Zaawansowane mechanizmy szyfrowania oraz certyfikaty zgodności z międzynarodowymi standardami (np. ISO 27001).
- Innowacyjnością: AWS regularnie wprowadza nowe usługi wspierające innowacyjne technologie, takie jak uczenie maszynowe czy Internet Rzeczy (IoT).

Podsumowanie:
Wybór AWS jako infrastruktury wdrożeniowej wynikał z potrzeby elastyczności, niezawodności oraz globalnego wsparcia. Dzięki różnorodności oferowanych usług i możliwości szybkiego skalowania, AWS okazał się optymalnym rozwiązaniem dla tego projektu.

#### Load Balancing

Zagadnienie: W systemach rozproszonych lub aplikacjach obsługujących dużą liczbę użytkowników kluczowym wyzwaniem jest równomierne rozdzielanie ruchu sieciowego. Brak odpowiedniego mechanizmu prowadzi do przeciążenia jednych serwerów, podczas gdy inne pozostają niewykorzystane. Przeciążone serwery mogą skutkować opóźnieniami, błędami aplikacji lub całkowitą niedostępnością usług.

Rozwiązanie: Load Balancing (równoważenie obciążenia) to technika dystrybucji ruchu sieciowego pomiędzy wiele serwerów w celu zapewnienia optymalnego wykorzystania zasobów, minimalizacji opóźnień oraz zapewnienia wysokiej dostępności aplikacji. Mechanizm ten może być wdrażany na różnych poziomach, takich jak warstwa aplikacyjna, sieciowa lub infrastrukturalna.

### Zalety i wady różnych rozwiązań Load Balancing  

| **Rodzaj**                | **Zalety**                                                                                          | **Wady**                                                                                     |
| -------------------------- | -------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Sprzętowy Load Balancer**| - Bardzo wysoka wydajność<br>- Dedykowane urządzenia z wyspecjalizowanym oprogramowaniem<br>- Dobre wsparcie dla dużych sieci korporacyjnych | - Wysoki koszt zakupu i utrzymania<br>- Trudności z elastycznym skalowaniem<br>- Zależność od dostawcy sprzętu |
| **Programowy Load Balancer**| - Możliwość wdrożenia na serwerach w chmurze lub lokalnych<br>- Wysoka elastyczność i integracja z narzędziami DevOps<br>- Niższe koszty niż rozwiązania sprzętowe | - Może nie osiągać wydajności sprzętowych rozwiązań<br>- Wymaga odpowiedniej konfiguracji i optymalizacji |
| **Load Balancing w chmurze** | - Automatyczne skalowanie i łatwość konfiguracji<br>- Integracja z innymi usługami chmurowymi<br>- Rozliczenie w modelu pay-as-you-go | - Zależność od dostawcy chmury<br>- Opóźnienia związane z komunikacją między regionami<br>- Koszty mogą rosnąć wraz z ruchem |

Mechanizm Load Balancingu dostępny w wybranej chmurze - AWS Elastic Load Balancing (ELB):
- AWS oferuje kilka rodzajów Load Balancerów, takich jak Application Load Balancer (ALB), Network Load Balancer (NLB) oraz Gateway Load Balancer (GLB). Dzięki temu możliwe jest dostosowanie rozwiązania do specyficznych wymagań aplikacji (np. warstwa aplikacji, TCP/UDP).
- Zalety: Automatyczna integracja z EC2, wysokie bezpieczeństwo, globalna dostępność.
- Wady: Koszty mogą być wysokie w przypadku dużego ruchu.

#### Amazon Simple Queue Service

Zagadnienie: W aplikacjach rozproszonych oraz mikroserwisowych, często pojawia się konieczność niezawodnego i skalowalnego przesyłania wiadomości między komponentami. Bez odpowiednich mechanizmów, ryzyko utraty danych, przeciążenia systemu czy trudności w zarządzaniu kolejnością i priorytetem wiadomości znacząco rośnie.

Rozwiązanie: Amazon Simple Queue Service (SQS) to w pełni zarządzana usługa kolejkowania wiadomości, która umożliwia aplikacjom rozproszonym komunikację w sposób asynchroniczny. Dzięki temu różne komponenty systemu mogą działać niezależnie, skalować się w różnym tempie i przetwarzać dane w odpowiednim momencie, co zwiększa elastyczność i odporność całej infrastruktury.

Rodzaje kolejek w SQS
1. Standard Queue
- Zapewnia wysoką przepustowość przesyłania wiadomości.
- Gwarantuje co najmniej jednokrotne dostarczenie wiadomości, ale ich kolejność nie jest gwarantowana.
- Idealne do aplikacji, w których kolejność wiadomości nie jest kluczowa.
2. FIFO Queue (First-In-First-Out)
- Zapewnia kolejność wiadomości zgodnie z ich wysyłaniem.
- Gwarantuje dokładnie jednokrotne dostarczenie wiadomości.
- Odpowiednie dla aplikacji wymagających ścisłej kontroli kolejności.

### Zalety Amazon Simple Queue Service (SQS)

| **Zaleta**                                   | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Brak zarządzania infrastrukturą**         | SQS jest w pełni zarządzaną usługą, co eliminuje konieczność obsługi serwerów.                   |
| **Skalowalność**                             | Automatycznie skaluje się, aby obsłużyć dowolną ilość wiadomości i obciążenie systemu.            |
| **Bezpieczeństwo**                           | Integracja z AWS IAM umożliwia kontrolę dostępu do kolejek.                                       |
| **Elastyczność**                             | Obsługuje zarówno kolejki Standard, jak i FIFO, co pozwala dostosować się do potrzeb aplikacji.   |
| **Niezawodność**                             | Dane są przechowywane na wielu serwerach w centrach danych AWS, co minimalizuje ryzyko ich utraty.|
| **Integracja**                               | Działa bezproblemowo z innymi usługami AWS, np. Lambda, EC2 czy SNS.                             |

### Wady Amazon Simple Queue Service (SQS)

| **Wada**                                    | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Koszty**                                  | W przypadku dużej liczby operacji koszty mogą rosnąć.                                             |
| **Opóźnienia w dostarczaniu wiadomości**    | W przypadku kolejek Standard, wiadomości mogą być dostarczone więcej niż raz i w innej kolejności.|
| **Limit długości wiadomości**               | Maksymalny rozmiar wiadomości wynosi 256 KB, co może wymagać podziału dużych danych.              |

Decyzja: W projekcie Amazon SQS został wybrany jako rozwiązanie do zarządzania asynchroniczną komunikacją między mikroserwisami. Usługa ta zapewnia skalowalność, niezawodność oraz integrację z innymi komponentami AWS, co ułatwia rozwój i utrzymanie systemu.

#### Architektura mikroserwisowa

Zagadnienie: W miarę jak aplikacje rosną, stają się coraz bardziej złożone i trudne do zarządzania. Monolityczne podejście, w którym cały system jest jednym, dużym komponentem, staje się coraz mniej efektywne, gdy chodzi o rozwój, skalowanie czy utrzymanie. Zwiększa się ryzyko awarii, trudności w zarządzaniu zespołami deweloperskimi, a także problematyczna staje się elastyczność w implementacji nowych funkcji.

Rozwiązanie: Architektura mikroserwisowa to podejście, w którym aplikacja jest rozdzielona na szereg niezależnych, małych serwisów, które komunikują się ze sobą za pomocą interfejsów API. Każdy mikroserwis odpowiada za konkretną funkcjonalność i może być rozwijany, wdrażany oraz skalowany niezależnie od innych. W ramach tej architektury zespół deweloperski może skoncentrować się na mniejszych częściach aplikacji, co przyspiesza rozwój i zwiększa niezawodność systemu.

Kluczowe cechy mikroserwisów:
- Rozdzielenie funkcji: Każdy mikroserwis realizuje jeden, dobrze zdefiniowany aspekt biznesowy lub techniczny aplikacji.
- Autonomiczność: Mikroserwisy są niezależne w zakresie wdrożeń, testów i skalowania.
- Komunikacja między serwisami: Mikroserwisy komunikują się za pomocą API, często przy użyciu REST lub gRPC.
- Niezależność technologiczna: Każdy mikroserwis może być napisany w innej technologii, języku programowania czy bazie danych.
- Skalowalność: Możliwość skalowania każdego mikroserwisu niezależnie w odpowiedzi na zmieniające się potrzeby.
- Zarządzanie awariami: W przypadku awarii jednego mikroserwisu reszta systemu nie musi przestawać działać.

### Zalety architektury mikroserwisowej

| **Zaleta**                                  | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Skalowalność**                           | Możliwość skalowania poszczególnych serwisów w zależności od ich obciążenia.                      |
| **Niezależność wdrożeń**                    | Każdy mikroserwis może być rozwijany i wdrażany niezależnie od innych.                           |
| **Elastyczność technologiczna**             | Każdy mikroserwis może być oparty na innym stosie technologicznym.                               |
| **Zwiększona niezawodność**                 | Awaria jednego mikroserwisu nie powoduje awarii całego systemu.                                  |
| **Szybszy rozwój i czas reakcji na zmiany**  | Zespoły mogą pracować nad różnymi mikroserwisami równolegle, co skraca czas implementacji nowych funkcji. |

### Wady architektury mikroserwisowej

| **Wada**                                    | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Złożoność zarządzania**                   | Większa liczba usług może prowadzić do trudności w monitorowaniu i zarządzaniu całą infrastrukturą. |
| **Kompleksowość komunikacji między serwisami**| Konieczność zarządzania i monitorowania komunikacji oraz zapewnienia niezawodności API.           |
| **Wydajność**                               | Możliwość opóźnień wynikających z komunikacji między mikroserwisami, zwłaszcza przy dużej liczbie serwisów. |
| **Zarządzanie danymi**                       | Rozproszone bazy danych mogą prowadzić do trudności w synchronizacji i zarządzaniu stanem aplikacji. |
| **Dodatkowe wymagania na infrastrukturę**   | Większe wymagania dotyczące infrastruktury, np. zarządzanie kontenerami, orkiestracja (np. Kubernetes). |

Decyzja: Architektura mikroserwisowa została wybrana w projekcie, aby zapewnić elastyczność w rozwoju i zarządzaniu aplikacją, a także umożliwić skalowanie jej poszczególnych elementów. Dzięki rozdzieleniu odpowiedzialności na mniejsze, niezależne serwisy, aplikacja jest bardziej odporna na awarie i łatwiejsza w rozwoju.

#### Wzorzec API Gateway

Zagadnienie: W dużych systemach rozproszonych, szczególnie w architekturze mikroserwisowej, zarządzanie komunikacją między wieloma serwisami może stać się trudne. Każdy mikroserwis może mieć różne interfejsy API, co prowadzi do złożoności w obsłudze połączeń, uwierzytelniania, monitorowania i zarządzania ruchem. Brak centralnego punktu kontroli w systemie powoduje konieczność replikowania tych funkcji w każdym mikroserwisie, co jest nieefektywne.

Rozwiązanie: Wzorzec API Gateway to podejście, w którym cała komunikacja między klientami a mikroserwisami przechodzi przez jeden centralny punkt, który pełni funkcje proxy. API Gateway odpowiada za przekazywanie zapytań do odpowiednich serwisów, zarządzanie bezpieczeństwem, logowaniem, monitorowaniem oraz transformacją danych. Może także oferować mechanizmy cache'owania, load balancing czy throttlingu.

Kluczowe cechy API Gateway;
- Centralizacja komunikacji: Wszystkie zapytania przychodzące do systemu są kierowane do API Gateway, który następnie rozdziela je do odpowiednich mikroserwisów.
- Ujednolicone API: Klient komunikuje się z jednym API, a nie z wieloma mikroserwisami.
- Bezpieczeństwo: API Gateway może przejąć odpowiedzialność za uwierzytelnianie i autoryzację, np. za pomocą tokenów JWT.
- Monitorowanie i logowanie: API Gateway może agregować dane o ruchu w systemie, zapewniając centralne logowanie i monitorowanie.
- Load balancing: Może pełnić funkcję load balancera, rozdzielając obciążenie między różne instancje mikroserwisów.
- Modyfikacja danych: API Gateway może również transformować dane przed ich wysłaniem do mikroserwisów lub przed przekazaniem odpowiedzi do klienta.

### Zalety wzorca API Gateway

| **Zaleta**                                  | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Centralizacja zarządzania**               | API Gateway centralizuje komunikację i kontrolę nad ruchem do wszystkich mikroserwisów.          |
| **Redukcja złożoności dla klientów**        | Klient łączy się z jednym API zamiast z wieloma mikroserwisami, co upraszcza interfejs.           |
| **Bezpieczeństwo**                          | Ujednolicenie mechanizmów uwierzytelniania i autoryzacji w jednym miejscu (np. OAuth, JWT).        |
| **Łatwiejsze monitorowanie**                | Łatwiejsze zbieranie logów, metryk i monitorowanie ruchu w jednym miejscu.                        |
| **Optymalizacja wydajności**                | API Gateway może implementować cache'owanie, co zmniejsza liczbę zapytań do mikroserwisów.          |

### Wady wzorca API Gateway

| **Wada**                                    | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Pojedynczy punkt awarii**                 | Jeśli API Gateway ulegnie awarii, może to sparaliżować całą komunikację z mikroserwisami.          |
| **Wąskie gardło**                           | Może stanowić wąskie gardło, jeśli nie jest odpowiednio skalowany, szczególnie przy dużym ruchu.   |
| **Złożoność zarządzania**                   | Dodanie warstwy API Gateway może zwiększyć złożoność infrastruktury, wymagając dodatkowego zarządzania.|
| **Opóźnienia**                              | Może wprowadzać dodatkowe opóźnienie w komunikacji, zwłaszcza gdy wykonuje dodatkowe operacje, takie jak transformacja danych. |

Decyzja: W projekcie zdecydowano się na zastosowanie wzorca API Gateway, aby uprościć komunikację między klientami a mikroserwisami, zapewniając centralne zarządzanie ruchem, bezpieczeństwem oraz monitorowaniem. Dzięki temu możliwe jest łatwiejsze zarządzanie całą aplikacją oraz zapewnienie jej elastyczności i skalowalności.

#### Sieć wewnętrzna VPC

Zagadnienie: W tradycyjnych infrastrukturach IT, sieć wewnętrzna jest zarządzana w obrębie firmy, gdzie wszystkie urządzenia są połączone w obrębie jednej sieci lokalnej (LAN). W przypadku rozwiązań chmurowych, gdzie zasoby są rozproszone geograficznie i mogą być zarządzane przez różne podmioty, zarządzanie siecią wewnętrzną staje się wyzwaniem. Wymaga to zapewnienia bezpiecznej, izolowanej sieci, która pozwala na komunikację między usługami w chmurze, zapewniając jednocześnie ochronę przed nieautoryzowanym dostępem z zewnątrz.

Rozwiązanie: VPC (Virtual Private Cloud) to rozwiązanie oferowane przez dostawców chmurowych, które pozwala na tworzenie prywatnych sieci w chmurze. VPC umożliwia pełną kontrolę nad tym, jak są połączone zasoby w chmurze, jakie mają adresy IP, jakie usługi są dostępne, oraz jak wygląda komunikacja z innymi sieciami (np. z Internetem). VPC zapewnia izolację od innych klientów chmury oraz możliwość konfiguracji zaawansowanych mechanizmów zabezpieczeń, takich jak firewalle, subnets, czy VPN.

Kluczowe cechy VPC
- Izolacja i prywatność: Użytkownicy mogą tworzyć izolowane sieci, które są oddzielone od innych klientów chmury.
- Kontrola nad konfiguracją: Umożliwia dokładną konfigurację podsieci, routingu, bramek internetowych, połączeń VPN i innych elementów sieciowych.
- Skalowalność: VPC może być łatwo skalowane w miarę wzrostu potrzeb organizacji.
- Bezpieczeństwo: Wbudowane mechanizmy kontroli dostępu (ACL, security groups) pozwalają na zarządzanie dostępem do zasobów w VPC.
- Integracja z innymi usługami chmurowymi: VPC umożliwia łatwą integrację z innymi usługami chmurowymi, takimi jak bazy danych, load balancers, czy usługi obliczeniowe.

### Zalety VPC

| **Zaleta**                                  | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Izolacja i prywatność**                   | VPC zapewnia pełną izolację zasobów, co umożliwia większe bezpieczeństwo aplikacji i danych.       |
| **Skalowalność**                            | Możliwość łatwego skalowania zasobów w chmurze, dostosowując je do zmieniających się potrzeb organizacji. |
| **Zaawansowane zarządzanie ruchem**         | Pełna kontrola nad ruchem przychodzącym i wychodzącym, w tym konfiguracja subnets, route tables, VPN. |
| **Integracja z innymi usługami chmurowymi** | Łatwa integracja z szeroką gamą usług chmurowych, co umożliwia elastyczność i adaptację infrastruktury. |
| **Bezpieczeństwo**                          | Mechanizmy takie jak firewalle, security groups oraz ACL zapewniają kontrolę nad dostępem i ochronę zasobów. |

### Wady VPC

| **Wada**                                    | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Złożoność konfiguracji**                  | Konfiguracja VPC, podsieci, routingu i polityk zabezpieczeń może być skomplikowana, szczególnie w dużych systemach. |
| **Potrzebna wiedza specjalistyczna**        | Aby poprawnie zaprojektować i zarządzać VPC, potrzebna jest znajomość sieci i zasad chmurowych usług. |
| **Ograniczenia wydajności**                 | W przypadku niewłaściwej konfiguracji VPC mogą wystąpić problemy z wydajnością, np. z opóźnieniami w komunikacji. |
| **Potrzebna infrastruktura do integracji**  | Integracja z innymi sieciami lub systemami on-premise może wymagać dodatkowej infrastruktury (np. VPN, Direct Connect). |


Decyzja: W projekcie zdecydowano się na wdrożenie VPC, aby zapewnić pełną kontrolę nad siecią wewnętrzną, zwiększyć bezpieczeństwo zasobów w chmurze oraz umożliwić łatwą integrację z innymi usługami chmurowymi. Dzięki tej architekturze możliwe było uzyskanie pełnej izolacji sieci oraz precyzyjnej konfiguracji polityk dostępu.

#### Oddzielne bazy danych dla mikroserwisów

Zagadnienie: W tradycyjnych monolitycznych aplikacjach często stosuje się jedną wspólną bazę danych dla całej aplikacji. W architekturze mikroserwisowej, gdzie każdy mikroserwis jest niezależnym bytem, współdzielenie jednej bazy danych może prowadzić do silnych zależności między serwisami, co utrudnia ich niezależny rozwój i skalowanie. Dodatkowo, różne mikroserwisy mogą mieć różne wymagania dotyczące przechowywania danych, co sprawia, że jedna wspólna baza danych nie zawsze jest optymalnym rozwiązaniem.

Rozwiązanie: Każdy mikroserwis powinien posiadać własną, dedykowaną bazę danych. Takie podejście zapewnia pełną autonomię mikroserwisów, umożliwiając im niezależny rozwój, skalowanie oraz wybór najbardziej odpowiedniego typu bazy danych dla swoich potrzeb. Dodatkowo, izolacja danych między mikroserwisami zwiększa bezpieczeństwo i ułatwia zarządzanie danymi.

Kluczowe cechy:
- Autonomia mikroserwisów: Każdy mikroserwis zarządza swoimi danymi, co pozwala na niezależny rozwój i wdrażanie.
- Izolacja danych: Brak współdzielenia bazy danych między mikroserwisami zwiększa bezpieczeństwo i ułatwia zarządzanie danymi.
- Optymalny dobór technologii: Możliwość wyboru najbardziej odpowiedniego typu bazy danych (SQL, NoSQL) dla konkretnego mikroserwisu.
- Skalowalność: Niezależne bazy danych pozwalają na skalowanie poszczególnych mikroserwisów zgodnie z ich wymaganiami.

### Zalety

| **Zaleta**                                  | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Niezależność mikroserwisów**              | Każdy mikroserwis może być rozwijany, wdrażany i skalowany niezależnie od innych.                |
| **Izolacja danych**                         | Brak współdzielenia bazy danych zwiększa bezpieczeństwo i ułatwia zarządzanie danymi.              |
| **Optymalny dobór technologii**             | Możliwość wyboru najbardziej odpowiedniego typu bazy danych (SQL, NoSQL) dla konkretnego mikroserwisu. |
| **Skalowalność**                            | Niezależne bazy danych pozwalają na skalowanie poszczególnych mikroserwisów zgodnie z ich wymaganiami. |

### Wady

| **Wada**                                    | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Złożoność zarządzania danymi**            | Rozproszenie danych może prowadzić do trudności w zarządzaniu spójnością i integracją danych między mikroserwisami. |
| **Brak transakcji rozproszonych**           | Brak wspólnej bazy danych uniemożliwia stosowanie tradycyjnych transakcji ACID między mikroserwisami. |
| **Potrzebna synchronizacja danych**         | Wymaga implementacji mechanizmów synchronizacji i spójności danych między mikroserwisami. |

Decyzja: W projekcie zdecydowano się na implementację oddzielnych baz danych dla każdego mikroserwisu, aby zapewnić pełną autonomię, bezpieczeństwo oraz optymalny dobór technologii dla poszczególnych komponentów systemu.

#### Amazon S3 Bucket

Zagadnienie: Amazon S3 (Simple Storage Service) to usługa przechowywania obiektów, która pozwala na łatwe przechowywanie i odzyskiwanie dowolnych ilości danych z dowolnego miejsca w Internecie. Problem pojawia się, gdy aplikacje potrzebują przechowywać duże pliki, takie jak obrazy, filmy, pliki tekstowe czy pliki dzienników w sposób bezpieczny, skalowalny i dostępny z wielu różnych lokalizacji. Rozwiązaniem jest użycie usługi S3 w celu zarządzania przechowywaniem danych w sposób bardziej elastyczny i wydajny.

Rozwiązanie: Amazon S3 Bucket pozwala na tworzenie "wiader" (buckets), w których przechowywane są dane. Dzięki wysokiej dostępności, skalowalności, bezpieczeństwu i integracji z innymi usługami AWS, S3 stało się podstawowym rozwiązaniem do przechowywania danych w chmurze. Zaletą jest również możliwość ustawiania polityk dostępu, integracja z AWS Lambda oraz łatwa integracja z systemami zewnętrznymi.

Kluczowe cechy
- Skalowalność: Amazon S3 jest wysoce skalowalne i może pomieścić dowolną ilość danych.
- Bezpieczeństwo: S3 zapewnia zaawansowane mechanizmy ochrony danych, takie jak szyfrowanie oraz kontrola dostępu.
- Dostępność: S3 zapewnia wyjątkową dostępność danych dzięki rozproszeniu danych w wielu centrach danych.
- Integracja: S3 dobrze współpracuje z innymi usługami AWS, takimi jak Lambda, CloudFront, Glacier.

### Zalety

| **Zaleta**                                  | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Skalowalność**                            | Amazon S3 automatycznie dostosowuje się do wzrostu ilości danych bez konieczności manualnej interwencji. |
| **Bezpieczeństwo**                          | Możliwość szyfrowania danych i kontrolowania dostępu do obiektów za pomocą polityk IAM oraz kluczy szyfrowania. |
| **Wysoka dostępność**                       | Dane przechowywane w S3 są automatycznie replikowane w wielu regionach, zapewniając wysoką dostępność. |
| **Prostota użytkowania**                    | Łatwe w użyciu API oraz interfejs użytkownika do zarządzania danymi. |
| **Niskie koszty**                           | Płacisz tylko za przechowywaną ilość danych i liczbę operacji, co pozwala na optymalizację kosztów. |

### Wady

| **Wada**                                    | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Koszty mogą wzrosnąć przy dużym ruchu**   | Wysokie koszty przy dużej liczbie operacji na plikach, zwłaszcza przy korzystaniu z różnych klas przechowywania. |
| **Ograniczenia rozmiaru obiektu**          | Maksymalny rozmiar pojedynczego obiektu to 5 TB, co może być niewystarczające w przypadku bardzo dużych plików. |
| **Brak wsparcia dla zaawansowanych baz danych** | S3 jest usługą przechowywania obiektów, a nie bazą danych, co oznacza, że nie nadaje się do przechowywania danych wymagających transakcji. |

Decyzja: Zdecydowano się na wykorzystanie Amazon S3 Bucket jako rozwiązania do przechowywania danych w chmurze ze względu na jego wysoką dostępność, łatwość integracji oraz skalowalność.

#### Nat Gateway

Zagadnienie: W architekturach chmurowych często pojawia się potrzeba udostępniania instancji w prywatnych subnetach dostępu do Internetu, bez konieczności bezpośredniego narażania tych instancji na dostęp z sieci publicznej. To wyzwanie rozwiązuje NAT Gateway. NAT (Network Address Translation) pozwala na przekierowanie ruchu wychodzącego z prywatnych instancji do Internetu, ale uniemożliwia dostęp do tych instancji z zewnątrz. Jest to szczególnie istotne w przypadku, gdy chcemy zapewnić bezpieczeństwo, izolując zasoby od publicznego Internetu, ale nadal umożliwiając im pobieranie aktualizacji, pakietów lub innych zasobów online.

Rozwiązanie: NAT Gateway to zarządzana usługa AWS, która pozwala na łatwe konfiguracje trasowania i translacji adresów IP w chmurze. W konfiguracji, instancje w prywatnym subnetcie mogą komunikować się z Internetem za pomocą NAT Gateway umieszczonego w publicznym subnetcie. NAT Gateway obsługuje automatyczne skalowanie, co zapewnia wysoką dostępność i niezawodność. Dzięki tej usłudze można utrzymać instancje w prywatnych subnetach w pełni zabezpieczone, a jednocześnie umożliwić im dostęp do zasobów zewnętrznych. 

Kluczowe cechy
- Bezpieczeństwo: NAT Gateway zapewnia bezpieczeństwo, ponieważ nie pozwala na dostęp z Internetu do instancji w prywatnym subnetcie.
- Skalowalność: Automatyczne skalowanie w odpowiedzi na wzrost obciążenia.
- Wysoka dostępność: Dostępność przez cały czas z automatycznym failoverem.
- Łatwość integracji: Łatwe w konfiguracji w ramach architektury AWS, szczególnie w przypadku VPC (Virtual Private Cloud).

### Zalety

| **Zaleta**                                  | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Bezpieczeństwo**                          | NAT Gateway umożliwia instancjom w prywatnym subnetcie dostęp do Internetu, ale nie umożliwia im bezpośredniego dostępu z sieci publicznej. |
| **Automatyczne skalowanie**                 | Usługa automatycznie skalowalna, co oznacza, że nie trzeba ręcznie dostosowywać jej mocy w zależności od ruchu. |
| **Prostota zarządzania**                    | Natychmiastowa konfiguracja i minimalne wymagania dotyczące zarządzania w porównaniu do tradycyjnych rozwiązań NAT. |
| **Wysoka dostępność**                       | NAT Gateway jest zarządzany przez AWS, co zapewnia wysoką dostępność i niezawodność bez konieczności zarządzania infrastrukturą. |
| **Bez dodatkowych zasobów**                 | Nat Gateway nie wymaga użycia dodatkowych instancji EC2 do obsługi NAT, co obniża koszty operacyjne. |

### Wady

| **Wada**                                    | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Koszty**                                  | NAT Gateway jest usługą płatną, a koszty mogą wzrosnąć w przypadku dużego ruchu lub dużej liczby instancji. |
| **Limitowana ilość zasobów**                | NAT Gateway może być stosunkowo kosztowną opcją przy dużej ilości instancji, szczególnie gdy potrzebujemy wielu usług w różnych regionach. |
| **Brak wsparcia dla niektórych protokołów**  | NAT Gateway może nie obsługiwać niektórych protokołów, takich jak ICMP (używanego do diagnostyki), co może być ograniczeniem w niektórych przypadkach. |

Decyzja: Zdecydowano się na implementację NAT Gateway w naszej infrastrukturze chmurowej, aby umożliwić instancjom w prywatnych subnetach dostęp do zasobów z Internetu bez ujawniania tych instancji publicznie. Dzięki automatycznemu skalowaniu i wysokiej dostępności NAT Gateway stanowi solidne, bezpieczne rozwiązanie w architekturze VPC.

#### Amazon Lambda

Zaganienie: W tradycyjnych systemach aplikacyjnych zasoby obliczeniowe (serwery, maszyny wirtualne) są zarządzane przez użytkownika, co wiąże się z koniecznością ich skalowania, monitorowania oraz zarządzania stanem. W związku z tym, tworzenie i zarządzanie skalowalnymi aplikacjami może być czasochłonne i kosztowne. Potrzebna jest technologia, która umożliwi uruchamianie kodu w sposób serverless (bez potrzeby zarządzania serwerami) i która automatycznie dostosowuje zasoby w zależności od zapotrzebowania.

Rozwiązanie: Amazon Lambda to usługa obliczeniowa typu serverless, która pozwala uruchamiać kod bez konieczności zarządzania infrastrukturą. Użytkownicy mogą wgrać kod, który zostanie automatycznie uruchomiony przez AWS w odpowiedzi na określone zdarzenie, takie jak przesłanie pliku do S3, zmiana danych w bazie danych czy wywołanie HTTP API.
Lambda obsługuje szeroki zakres scenariuszy, od prostych funkcji wywoływanych na zdarzeniach, po złożone aplikacje opierające się na mikroserwisach. W tym podejściu, użytkownicy płacą tylko za czas wykonywania kodu (tzw. "pay-as-you-go"), co pozwala na optymalizację kosztów.

Kluczowe cechy:
- Brak zarządzania serwerami: AWS zarządza całą infrastrukturą, co eliminuje konieczność skalowania, monitorowania i konserwacji serwerów.
- Skalowalność: Funkcje Lambda automatycznie skalują się w zależności od liczby wywołań, co umożliwia elastyczność.
- Model płatności "pay-as-you-go": Płacisz tylko za czas, w którym kod jest wykonywany, bez konieczności utrzymywania stałej infrastruktury.
- Integracja z innymi usługami AWS: Lambda może być wywoływana przez różne usługi, takie jak Amazon S3, DynamoDB, API Gateway, SNS i inne.

### Zalety

| **Zaleta**                                  | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Brak konieczności zarządzania serwerami**  | Lambda umożliwia uruchamianie kodu bez zarządzania infrastrukturą, co zmniejsza koszty operacyjne i czas poświęcony na konserwację. |
| **Automatyczna skalowalność**               | Funkcje Lambda automatycznie skalują się w zależności od zapotrzebowania, bez potrzeby ręcznego dostosowywania zasobów. |
| **Płatności za rzeczywiste użycie**         | Model płatności oparty na czasie wykonywania kodu sprawia, że opłaty są precyzyjnie dopasowane do faktycznego zużycia. |
| **Integracja z szerokim zakresem usług AWS**| Lambda łatwo integruje się z innymi usługami AWS, co ułatwia tworzenie rozproszonych aplikacji i mikroserwisów. |
| **Szeroki zakres zastosowań**               | Może być używana do przetwarzania plików, przetwarzania danych w czasie rzeczywistym, obsługi API i wielu innych scenariuszy. |

### Wady

| **Wada**                                    | **Opis**                                                                                          |
|---------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Ograniczenia czasowe**                    | Każda funkcja Lambda ma limit czasu działania, który wynosi 15 minut. Może to stanowić problem w przypadku długotrwałych operacji. |
| **Brak dostępu do stanu**                   | Funkcje Lambda są "stateless", co oznacza, że każda funkcja nie przechowuje żadnego stanu między wywołaniami, co może wymagać dodatkowej logiki do zarządzania stanem. |
| **Koszty przy dużej liczbie wywołań**       | Choć model płatności za czas wykonania jest opłacalny, duża liczba wywołań może prowadzić do wyższych kosztów w porównaniu do tradycyjnych serwerów. |
| **Trudności w debugowaniu**                 | Praca z funkcjami Lambda może być trudna do debugowania, szczególnie przy bardziej złożonych aplikacjach, wymagających zaawansowanego śledzenia błędów. |
| **Ograniczone zasoby wykonawcze**           | Funkcje Lambda mają ograniczenia dotyczące pamięci i mocy obliczeniowej, co może ograniczać ich wykorzystanie w bardziej wymagających zadaniach. |

Decyzja: Zdecydowano się na implementację Amazon Lambda w celu stworzenia skalowalnych aplikacji mikroserwisowych, które nie wymagają zarządzania infrastrukturą. Dzięki modelowi płatności "pay-as-you-go" oraz automatycznej skalowalności, Lambda stanowi elastyczne i opłacalne rozwiązanie w naszej architekturze chmurowej.

#### Internet Gateway

Zagadnienie: Aplikacje chmurowe często muszą komunikować się z zasobami znajdującymi się w Internecie, takimi jak serwisy zewnętrzne, API lub zasoby publiczne. W tradycyjnych środowiskach sieciowych, komunikacja ta odbywa się za pośrednictwem routerów, które łączą lokalne sieci z siecią globalną. W środowisku chmurowym, potrzeba jest komponentu, który umożliwi komunikację między prywatnymi zasobami w chmurze a światem zewnętrznym, zachowując odpowiednią kontrolę nad bezpieczeństwem i dostępem.

Rozwiązanie: Internet Gateway w Amazon Web Services (AWS) jest usługą, która umożliwia instancjom wirtualnym (np. EC2) znajdującym się w prywatnej sieci VPC (Virtual Private Cloud) łączenie się z Internetem. Jest to most, który pozwala na przesyłanie danych między zasobami wewnętrznymi w chmurze a zasobami zewnętrznymi w Internecie.
Internet Gateway zapewnia dostęp do internetu zarówno dla instancji w publicznych subnetach, jak i dla instancji w prywatnych subnetach z odpowiednimi regułami routingowymi. Dodatkowo, zapewnia odpowiednie mechanizmy bezpieczeństwa, takie jak kontrola dostępu i NAT (Network Address Translation), aby umożliwić komunikację wychodzącą, a jednocześnie chronić zasoby wewnętrzne.

Kluczowe cechy
- Bezpośredni dostęp do Internetu: Dzięki Internet Gateway, zasoby w VPC mogą komunikować się z zasobami zewnętrznymi w Internecie.
- Bezpieczeństwo i kontrola: Możliwość ustawienia reguł bezpieczeństwa, takich jak grupy zabezpieczeń i ACL (Access Control List), które kontrolują dostęp do zasobów w sieci.
- Wsparcie dla NAT: Internet Gateway umożliwia przekierowanie ruchu NAT w celu zapewnienia wychodzącej komunikacji z prywatnych subnetów.
- Brak kosztów: Korzystanie z Internet Gateway w AWS jest bezpłatne – opłaty naliczane są za dane przesyłane przez Internet.

### Zalety

| **Zaleta**                                    | **Opis**                                                                                          |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Prosty dostęp do Internetu**                | Internet Gateway umożliwia łatwy dostęp do Internetu, co jest niezbędne dla aplikacji wymagających komunikacji z zasobami zewnętrznymi. |
| **Wsparcie dla różnych usług AWS**            | Możliwość integracji z innymi usługami AWS, np. EC2, Lambda, S3, pozwala na elastyczną i kompleksową architekturę. |
| **Skalowalność**                              | Automatycznie skalowalny komponent, który dostosowuje się do zmieniającego się ruchu w sieci. |
| **Brak kosztów**                              | Internet Gateway nie wiąże się z dodatkowymi opłatami za użycie samej usługi – płacisz tylko za dane przesyłane przez Internet. |
| **Integracja z NAT Gateway**                  | Dzięki integracji z NAT Gateway, zasoby w prywatnych subnetach mogą nawiązywać połączenia wychodzące z Internetem. |

### Wady

| **Wada**                                      | **Opis**                                                                                          |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Ograniczenie do regionu AWS**               | Internet Gateway działa tylko w obrębie jednego regionu AWS, co może wymagać odpowiedniej konfiguracji w przypadku wieloregionowych aplikacji. |
| **Brak wsparcia dla ruchu przychodzącego**    | Internet Gateway umożliwia tylko wychodzący ruch z instancji do Internetu. Do ruchu przychodzącego potrzebne są dodatkowe mechanizmy (np. Load Balancer). |
| **Wymaga odpowiedniej konfiguracji VPC**     | Aby Internet Gateway działał poprawnie, wymagana jest odpowiednia konfiguracja VPC oraz tabel routingu. |
| **Bezpieczeństwo**                            | Choć Internet Gateway zapewnia dostęp do Internetu, wymaga poprawnej konfiguracji grup bezpieczeństwa i ACL, aby uniknąć nieautoryzowanego dostępu. |

Decyzja: Internet Gateway został wybrany do implementacji w naszej architekturze w celu umożliwienia zasobom w naszej VPC komunikacji z Internetem, co jest niezbędne dla aplikacji korzystających z zewnętrznych API i innych zasobów dostępnych publicznie.

#### Autoryzacja z wykorzystaniem JWT

Zagadnienie: W nowoczesnych aplikacjach, szczególnie w mikroserwisach, zachodzi potrzeba zapewnienia bezpiecznego i efektywnego mechanizmu autoryzacji i autentykacji użytkowników. W tradycyjnych podejściach do autentykacji, każda aplikacja musi przechowywać dane użytkowników i ich sesje. To może prowadzić do problemów z wydajnością, skalowalnością i bezpieczeństwem, zwłaszcza w przypadku rozproszonych systemów.

Rozwiązanie: JWT (JSON Web Token) jest popularnym standardem do realizacji autoryzacji i autentykacji w aplikacjach webowych i chmurowych. Token JWT zawiera zakodowane dane użytkownika, takie jak jego identyfikator, role, czas wygaśnięcia tokena oraz inne metadane. Dzięki temu JWT pozwala na delegowanie autoryzacji pomiędzy różnymi mikroserwisami, bez potrzeby przechowywania sesji w każdej z aplikacji.
W JWT dane są bezpiecznie zaszyfrowane i podpisane, co zapewnia, że token nie może zostać zmanipulowany. Dodatkowo JWT jest przechowywany po stronie klienta (np. w lokalnej pamięci przeglądarki lub ciasteczkach), co pozwala na łatwe skalowanie aplikacji i niezależność od stanu serwera.

Kluczowe cechy
- Bezstanowość: Nie ma potrzeby przechowywania sesji po stronie serwera, co znacząco poprawia skalowalność aplikacji.
- Szybkość: JWT jest samodzielnym tokenem zawierającym wszystkie potrzebne dane, co eliminuje konieczność przechowywania sesji i zapytań do bazy danych.
- Łatwa integracja: JWT jest zgodny z wieloma technologiami i łatwy do integracji z aplikacjami opartymi na mikroserwisach.
- Bezpieczeństwo: JWT używa podpisów cyfrowych, co zapewnia integralność danych i ochronę przed ich manipulowaniem.
- Szerokie wsparcie: JWT jest szeroko wspierane w popularnych frameworkach i bibliotekach, co umożliwia łatwą implementację w wielu językach programowania.

### Zalety

| **Zaleta**                                    | **Opis**                                                                                          |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Bezstanowość**                              | JWT eliminuje konieczność przechowywania sesji po stronie serwera, co ułatwia skalowanie aplikacji. |
| **Bezpieczeństwo**                            | Dzięki podpisom cyfrowym, JWT zapewnia, że tokeny są autentyczne i nie zostały zmienione. |
| **Elastyczność**                              | JWT jest stosunkowo prosty w implementacji i wspierany przez większość popularnych frameworków. |
| **Szerokie wsparcie dla różnych środowisk**   | JWT jest wspierane przez szeroką gamę platform i technologii, w tym systemy chmurowe i mikroserwisy. |
| **Skalowalność**                              | Umożliwia rozproszone zarządzanie autoryzacją, co jest kluczowe w aplikacjach mikroserwisowych. |

### Wady

| **Wada**                                      | **Opis**                                                                                          |
|-----------------------------------------------|--------------------------------------------------------------------------------------------------|
| **Brak możliwości łatwego unieważnienia**    | Po wygenerowaniu tokenu JWT, nie ma łatwego sposobu na jego unieważnienie przed upływem czasu życia. |
| **Zbyt długi czas życia tokena**              | Długi czas życia tokena może prowadzić do problemów bezpieczeństwa w przypadku wycieku tokena. |
| **Brak mechanizmów do ścisłej kontroli sesji**| JWT nie zapewnia mechanizmu zarządzania sesją, co może prowadzić do trudności w monitorowaniu i kontrolowaniu użytkowników. |
| **Potrzebna odpowiednia konfiguracja**       | Wymaga odpowiedniej konfiguracji oraz bezpiecznego przechowywania kluczy do podpisywania tokenów. |

Decyzja: JWT zostało wybrane do implementacji w naszym systemie, aby umożliwić bezpieczną i skalowalną autoryzację użytkowników w aplikacji rozproszonej. Dzięki łatwej integracji z mikroserwisami i eliminacji konieczności przechowywania sesji na serwerze, pozwala to na prostsze zarządzanie dostępem oraz lepszą skalowalność systemu. Zastosowanie JWT jest również korzystne z punktu widzenia wydajności, ponieważ pozwala na szybszą autoryzację użytkowników bez potrzeby wielokrotnego zapytania do bazy danych.

#### Relacyjna baza danych Amazon RDS

#### Amazon Cognito


### Aplikacyjne

#### Architektura heksagonalna

#### Architektura warstwowa

#### Event Sourcing

#### Optimistic Locking

#### Wzorzec Agregat

#### Wzorzec Fasady

#### Struktury Dużej Skali


## Widoki architekotniczne

### Widok kontekstowy (C4 Context)
![structurizr-SystemContext](https://github.com/user-attachments/assets/da262738-292d-43cf-ba15-03f70b78c461)

### Scenariusze interakcji (C4 Container)
![structurizr-Container-001](https://github.com/user-attachments/assets/e7d28b4e-aae6-441e-a1d4-c07a8b7ccf8c)



### Interfejsy integracyjne

| Aspekt                            | Opis                |
| --------------------------------- | ------------------- |
| Aplikacja źródłowa                | Deskly FE           |
| Aplikacja docelowa                | Deskly Location     |
| Techinika integracji              | HTTPS               |
| Mechanizm uwierzytelniania        | JWT                 |
| Manipulacja na danych wrazliwych? | nie                 |
| Strona inicujująca                | Deskly FE           |
| Model komunikacji                 | synchroniczny, REST |
| Wydajność                         | 1000 zapytań / s    |
| Wolumetria                        | 250 kB / s          |
| Wymagana dostępność               | 99.9%               |

| Aspekt                            | Opis                |
| --------------------------------- | ------------------- |
| Aplikacja źródłowa                | Deskly FE           |
| Aplikacja docelowa                | Deskly Core         |
| Techinika integracji              | HTTPS               |
| Mechanizm uwierzytelniania        | JWT                 |
| Manipulacja na danych wrazliwych? | tak                 |
| Strona inicujująca                | Deskly FE           |
| Model komunikacji                 | synchroniczny, REST |
| Wydajność                         | 1000 zapytań / s    |
| Wolumetria                        | 250 kB / s          |
| Wymagana dostępność               | 99.9%               |

| Aspekt                            | Opis                          |
| --------------------------------- | ----------------------------- |
| Aplikacja źródłowa                | Deskly Location               |
| Aplikacja docelowa                | Deskly Core                   |
| Techinika integracji              | AWS SDK                       |
| Mechanizm uwierzytelniania        | access key, secret access key |
| Manipulacja na danych wrazliwych? | nie                           |
| Strona inicujująca                | Deskly Location               |
| Model komunikacji                 | asynchroniczny, SQS           |
| Wydajność                         | 500 zapytań / s               |
| Wolumetria                        | 100 kB / s                    |
| Wymagana dostępność               | 99.9%                         |

| Aspekt                            | Opis                          |
| --------------------------------- | ----------------------------- |
| Aplikacja źródłowa                | Deskly Core                   |
| Aplikacja docelowa                | Deskly Location               |
| Techinika integracji              | AWS SDK                       |
| Mechanizm uwierzytelniania        | access key, secret access key |
| Manipulacja na danych wrazliwych? | nie                           |
| Strona inicujująca                | Deskly Core                   |
| Model komunikacji                 | asynchorniczny, SQS           |
| Wydajność                         | 500 zapytań / s               |
| Wolumetria                        | 100 kB / s                    |
| Wymagana dostępność               | 99.9%                         |

| Aspekt                            | Opis                         |
| --------------------------------- | ---------------------------- |
| Aplikacja źródłowa                | Deskly Core, Deskly Location |
| Aplikacja docelowa                | Deskly DB                    |
| Techinika integracji              | JDBC                         |
| Mechanizm uwierzytelniania        | nazwa uytkownika, hasło      |
| Manipulacja na danych wrazliwych? | tak                          |
| Strona inicujująca                | Deskly Core, Deskly Location |
| Model komunikacji                 | synchorniczny                |
| Wydajność                         | 500 zapytań / s              |
| Wolumetria                        | 100 kB / s                   |
| Wymagana dostępność               | 99.9%                        |

## Widok funkcyjny (C4 Component)
![structurizr-Component-001 (1)](https://github.com/user-attachments/assets/36f9e1bf-a9a1-4deb-bf15-8b0a395fba53)
![structurizr-Component-002](https://github.com/user-attachments/assets/50619c36-690b-4ad8-aeee-d7a60bba9579)

## Widok rozmieszczenia (Architekrura Wdrożeniowa)

![image](https://github.com/user-attachments/assets/8854b070-17c7-459a-bbc0-40e0458714e8)

## Widok informacyjny

### Model informacyjny

![Model_Informacyjny1 drawio (2)](https://github.com/user-attachments/assets/c3eb8814-428e-40b2-828d-c305f32d8abc)

### Projekt Bazy Danych

![deskly-db-diagram drawio (3)](https://github.com/user-attachments/assets/237edf3e-e0eb-480c-b409-7d7b942fb9b8)

## Widok wytwarzania 

### Frontend

Aplikacja frontendowa zostanie zaimplementowana we frameworku Angular 18. Do zbudowania aplikacji zostanie wykorzystane zostanie narzędzie nx. Aplikacja została podzielona na moduły reprezentujące domeny grupujące funkcjonalności udostępniane uzytkownikom końcowym. Centralnym punktem aplikacji będzie katalog `src` zawierający pliki `index.html` (definiuje wstępną struktruę DOM) oraz  `main.ts` (od tego pliku rozpoczyna sie ładowanie logiki aplikacji). Kazda z modułów ma zblizoną strukturę obejmującę 1 - 4 katalogów ze zbioru (`feature` - komponenty smart, `ui` - komponenty prezentacyjne, `data` - serwisy biznesowe, zarządzanie stanem, komunikacja z backendem oraz `domain` - modele danych). 

W aplikacji zaimplementowany zostanie mechanizm leniwego ładowania, polegający na tym, że w trakcie budowania aplikacji niektóre jej części (moduły) są umieszczone w odzielnych plikach JS (tzw. chunkach), które nie muszą być wczytywane podczas początkowego wczytywania aplikacji, a dopiero w momencie, gdy zostaną zarządane przez użytkownika (przykładowo nie ma potrzeby wczytywania kodu obsługującego funkcjonalności, które nie są dostępne dla danego użytkownika). Rozwiązanie to umożliwia optymalizację czasu wczytywania aplikacji oraz korzystnie na wpływa na UX. 

Ponizej zamieszczono diagram prezentujący widok wytwarzania aplikacji frontendowej.

![Widok wytwarzania](./images/fe.png)

### Backend

## Realizacja przypadku użycia (Przypisanie zasobu do lokacji)

Przypisanie zasobu jest inicjowane przez Location Managera z poziomu klienta Deskly. Polega na przesłaniu zapytania POST zawierającego identyfikatory przypisywanych zasobów.

Przykład zapytania
```
curl --location 'localhost:8080/api/v1/location/6f0a36c6-6814-4e38-b40b-0a65b2f7c3c6/resource/assign' \
--header 'Content-Type: application/json' \
--request POST \
--data '{
    "resourceIds": ["db37fe1a-ab0e-4f9d-8b43-5bf84dcc3648", "7f446172-971e-48c1-b5bc-0538b96dfc20"]
}'
```

Diagram sekwencji

![Diagram sekwencji](./images/sequence-diagram.png)
