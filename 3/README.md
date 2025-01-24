# Wyniki etapu III - Implementacja systemu

- Kamil Bońkowski (252727)
- Szymon Walasik (283393)
- Jakub Wierzchowiec (252738)

Niniejszy dokument stanowi podsumowanie prac nad systemem do rezerwacji przestrzeni biurowych Deskly.

## Wdrożenie systemu
System został wdrożony na AWS i jest dostępny do użytku publicznego.

- [frontend](http://deskly-lb-1156685114.us-east-1.elb.amazonaws.com/)
- [API gateway](https://o3pm5tkex5.execute-api.us-east-1.amazonaws.com/staging)

## Status implementacji elementów systemu

### Legenda:

<table>
  <tr>
    <th style="width: 50px;">Symbol</th>
    <th style="width: 200px;">Opis</th>
  </tr>
  <tr>
    <td>✅</td>
    <td>Zaimplementowane</td>
  </tr>
  <tr>
    <td>🔴</td>
    <td>Nie zaimplementowane</td>
  </tr>
   <tr>
    <td>🔵</td>
    <td>Częściowo zaimplementowane</td>
  </tr>
    <tr>
    <td>🟡</td>
    <td>W trakcie testów</td>
  </tr>
      <tr>
    <td>🔄</td>
    <td>W trakcie implementacji</td>
  </tr>

</table>  

### Infrastruktura wdrożeniowa


<table>
  <tr>
    <th style="width: 300px;">Usługa/Mechanizm</th>
    <th style="width: 700px;">Opis</th>
    <th style="width: 200px;">Status</th>
  </tr>
  <tr>
    <td><code>AWS Cognito</code></td>
    <td>Uwierzytelnianie użytkowników odbywa się poprzez integrację z AWS Cognito</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>AWS Cognito</code> <code>AWS Lambda</code> </td>
    <td>Integracja AWS Cognito z AWS Lambda w celu nadawania ról systemowych</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>AWS EKS</code></td>
    <td>Elastic Kubernetes Service (AWS EKS) jest wykorzystywany do zarządzania mikroserwisami</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>AWS Application Load Balancer</code></td>
    <td>Load Balancing przychodzących zapytań z wykorzystaniem AWS Application Load Balancer </td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>AWS Application Load Balancer</code></td>
    <td>Integracja Kubernetes Ingress z AWS Application Load Balancer</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>AWS Cognito</code> <code>API Gateway</code></td>
    <td>Autoryzacja zapytań z wykorzystaniem AWS Cognito i API Gateway</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>AWS RDS</code></td>
    <td>Mikroserwisy wykorzystują relacyjne bazy danych AWS RDS do przechowywania danych</td>
    <td>✅</td>
  <tr>
    <td><code>AWS RDS</code></td>
    <td>Realacyjne bazy danych RDS są dostępne w dwóch strefach dostępności (Availability Zones) </td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>AWS S3 Bucket</code></td>
    <td>Mikroserwisy wykorzystują AWS S3 Bucket do przechowywania plików</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>AWS SQS</code></td>
    <td>Mikroserwisy do komunikacji asynchronicznej wykorzystują kolejkę AWS SQS</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>Horizontal Pod Scaling</code></td>
    <td>Horyzontalne skalowanie podów w zależności od stanu zużycia CPU lub pamięci</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>Horizontal Node Scaling</code></td>
    <td>Horyzontalne skalowanie nodeów w zależności od stanu zużycia CPU lub pamięci</td>
    <td>🔴</td>
</tr>
<tr>
    <td><code>AWS CloudWatch Logs</code></td>
    <td>Logi mikroserwisów oraz innych elementów klastra Kubernetes są dostępne w AWS CloudWatch</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>Nat Gateway</code></td>
    <td>Ruch sieciowy wychodzący z prywatnych podsieci do Internetu odbywa się poprzez Nat Gateway</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>Internet Gateway</code></td>
    <td>Ruch sieciowy wychodzący z publicznych podsieci do Internetu odbywa się poprzez Internet Gateway</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>Cluster Availability Zones</code></td>
    <td>Klaster EKS dostępny jest w dwóch strefach dostępności (Availability Zones)</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>VPC Network</code></td>
    <td>Infrastruktura działa w hermetycznej sieci VPC</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>VPC Subnets</code></td>
    <td>Sieć VPC podzielona jest na podsieci publiczne i prywatne</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>VPC Endpoints</code></td>
    <td>Ruch wychodzący z klastra do AWS CloudWatch, AWS SQS, AWS S3 odbywa się poprzez VPC Endpoints</td>
    <td>🔴</td>
</tr>

</table>

### DevOps

<table>
  <tr>
    <th style="width: 150px;">Narzędzie</th>
    <th style="width: 700px;">Opis</th>
    <th style="width: 200px;">Status</th>
  </tr>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Projekt wykorzystuje narzędzie Jenkins do automatyzacji procesu developmentu</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Integracja Jenkins z Github Webhooks</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Integracja z zewnętrznym węzłem (Jenkins Agent)</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Wykorzystanie pluginu Blue Ocean do wizualizacji etapów pipeline</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Automatyczny build projektu</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Automatyczne uruchamianie testów jednostkowych</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Automatyczne tworzenie obrazów Dockerowych i publikowanie ich w repozytorium DockerHub</td>
    <td>✅</td>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Deployment nowego obrazu do klastra Kubernetes</td>
    <td>🔄</td>
  </tr>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Integracja z SonarQube</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>Jenkins</code></td>
    <td>Integracja narzędzi do analizy zależności między pakietami oraz modułami</td>
    <td>🔴</td>
  </tr>
    </tr>
    <tr>
    <td><code>Jenkins</code></td>
    <td>Parametryzacja haseł, kluczy prywatnych, tokenów itd. wykorzystując Jenkins Credentials </td>
    <td>✅</td>
  </tr>
    <tr>
    <td><code>Ansible</code></td>
    <td>Zarządzanie serwerami przy użyciu skryptów automatyzujących</td>
    <td>✅</td>
  </tr>
  </tr>
    <tr>
    <td><code>Terraform</code></td>
    <td>Tworzenie infrastruktury w chmurze AWS jako Infrastructure As Code</td>
    <td>✅</td>
  </tr>
  </tr>
    <tr>
    <td><code>Docker</code></td>
    <td>Konteneryzacja mikroserwisów</td>
    <td>✅</td>
  </tr>
    </tr>
    <tr>
    <td><code>Postman</code></td>
    <td>Dokumentowanie API</td>
    <td>✅</td>
  </tr>

</table>

### Realizacja wymagań funkcjonalnych

<table>
  <tr>
    <th style="width: 150px;"></th>
    <th style="width: 700px;">Wymaganie</th>
    <th style="width: 200px;">Status</th>
  </tr>
  <tr>
    <td><code>FR/KD/01</code></td>
    <td>Jako klient Deskly chciałbym mieć możliwość zalogować się do/wylogować się ze swojego konta użytkownika.</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>FR/KD/02</code></td>
    <td>Jako klient Deskly chciałbym mieć podgląd kodu QR do otwarcia drzwi z poziomu konta użytkownika.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/03</code></td>
    <td>Jako klient Deskly po rezerwacji zasobu chciałbym otrzymać kod QR na maila umożliwiający otwarcie drzwi wejściowych do danej lokacji 24 godziny przed rozpoczęciem rezerwacji.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/04</code></td>
    <td>Jako klient Deskly chciałbym mieć podgląd wszystkich wynajętych zasobów oraz szczegółów każdej z aktywnych rezerwacji.</td>
    <td>🔄</td>
  </tr>
  <tr>
    <td><code>FR/KD/05</code></td>
    <td>Jako klient Deskly chciałbym mieć możliwość rezerwacji zasobu w dowolnie wybranej lokacji.</td>
    <td>🔄</td>
  </tr>
  <tr>
    <td><code>FR/KD/06</code></td>
    <td>Jako klient Deskly chciałbym podczas rezerwacji biurka lub sali konferencyjnej być w stanie wybrać interesujący mnie zasób korzystając ze schematu topologii lokacji.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/07</code></td>
    <td>Jako klient Deskly chciałbym zapisać się na listę oczekujących na zasób w danym terminie (jeśli jest już zarezerwowany przez kogoś innego), gdy czas do rozpoczęcia rezerwacji jest dłuższy niż 24 godziny.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/08</code></td>
    <td>Jako klient Deskly chciałbym móc wypisać się z kolejki oczekujących na dany zasób w dowolnym momencie.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/09</code></td>
    <td>Jako klient Deskly oczekujący w kolejce na zasób chciałbym zostać poinformowany o rozwiązaniu kolejki i otrzymać propozycję rezerwacji/zakolejkowania się na tożsamy zasób.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/10</code></td>
    <td>Jako klient stały chciałbym zostać poinformowany mailowo o zbliżającym się końcu umowy.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/11</code></td>
    <td>Jako klient stały chciałbym otrzymać propozycję automatycznego przedłużenia umowy wraz ze szczegółami o aktualnym cenniku.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/12</code></td>
    <td>Jako klient biznesowy Deskly chciałbym mieć podgląd wszystkich wynajętych zasobów oraz szczegółów każdej z aktywnych rezerwacji.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/13</code></td>
    <td>Jako klient biznesowy Deskly chciałbym, żeby po akceptacji umowy przez Contract Managera wynegocjowane zasoby zostały zarezerwowane w imieniu firmy z datą rozpoczęcia umowy dla wskazanych pracowników firmy i żeby dla tych pracowników zostały automatycznie wygenerowane konta użytkownika z dostępem do zasobów.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/14</code></td>
    <td>Jako klient biznesowy Deskly chciałbym posiadać konto użytkownika, które będzie pozwalać mi jako pracodawcy zarządzać dostępem do zarezerwowanych zasobów dla pracowników.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/KD/15</code></td>
    <td>Jako klient biznesowy Deskly chciałbym móc stworzyć konto nowemu pracownikowi i nadać mu uprawnienia do korzystania z zarezerwowanych zasobów.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/LM/01</code></td>
    <td>Jako Location Manager chciałbym móc dodać lokację, zdefiniować cennik zasobów oraz zdefiniować zasoby w danej lokacji (rodzaj zasobu, zdjęcia, dane seryjne (w przypadku biurek oraz sprzętu audio-wideo), liczba miejsc (w przypadku sali konferencyjnej), opis).</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>FR/LM/01</code></td>
    <td>Jako Location Manager chciałbym móc dodać lokację, zdefiniować cennik zasobów oraz zdefiniować zasoby w danej lokacji (rodzaj zasobu, zdjęcia, dane seryjne (w przypadku biurek oraz sprzętu audio-wideo), liczba miejsc (w przypadku sali konferencyjnej), opis).</td>
    <td>✅</td>
  </tr>
  <tr>
    <td><code>FR/LM/02</code></td>
    <td>Jako Location Manager mogę zlecić konserwację zasobu.</td>
    <td>🔄</td>
  </tr>
  <tr>
    <td><code>FR/LM/03</code></td>
    <td>Jako Location Manager mogę wyłączyć dany zasób z użytkowania (nawet jeśli jest aktualnie zarezerwowany).</td>
    <td>🔄</td>
  </tr>
  <tr>
    <td><code>FR/LM/04</code></td>
    <td>Jako Location Manager chciałbym zdefiniować godziny otwarcia danej lokacji.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/LM/05</code></td>
    <td>Jako Location Manager chciałbym móc zdefiniować topologię zasobów w danej lokacji (dodać/usunąć/modyfikować).</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/LM/06</code></td>
    <td>Jako Location Manager chciałbym mieć możliwość aktualizacji danych lokalizacji oraz dostępnych zasobów.</td>
    <td>🔵<</td>
  </tr>
    <tr>
    <td><code>FR/LM/07</code></td>
    <td>Jako Location Manager chciałbym mieć możliwość przypisywania zasobów do danej lokacji.</td>
    <td>🔵</td>
  </tr>
  </tr>
    <tr>
    <td><code>FR/LM/08</code></td>
    <td>Jako Location Manager chciałbym mieć możliwość wypisywania zasobów z danej lokacji.</td>
    <td>🔵<</td>
  </tr>
  <tr>
    <td><code>FR/CM/01</code></td>
    <td>Jako Contract Manager chciałbym mieć możliwość wysłania do edycji wersji roboczej umowy do wcześniej zweryfikowanego klienta.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/CM/02</code></td>
    <td>Jako Contract Manager chciałbym mieć możliwość akceptacji oraz proponowania zmian w umowie udostępnionej klientowi.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/CM/03</code></td>
    <td>Jako Contract Manager chciałbym mieć możliwość akceptacji oraz odrzucenia umowy z potencjalnym klientem.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/FM/01</code></td>
    <td>Jako Finance Manager chciałbym mieć podgląd do klientów, którzy nie uregulowali faktury na czas.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/FM/02</code></td>
    <td>Jako Finance Manager chciałbym wysłać fakturę do klienta zgodną z rzeczywistym wykorzystaniem przez niego zasobów w danym okresie rozliczeniowym.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/FM/03</code></td>
    <td>Jako Finance Manager chciałbym mieć podgląd do wszystkich wystawionych faktur.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/FM/04</code></td>
    <td>Jako Finance Manager chciałbym mieć podgląd do cenników, według których naliczane są opłaty w danej lokacji dla danych klientów.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/FM/05</code></td>
    <td>Jako Finance Manager chciałbym mieć wgląd do wszystkich zawartych umów.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/BM/01</code></td>
    <td>Jako Booking Manager chciałbym przesuwać dowolnych klientów w kolejce na oczekiwany zasób.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/BM/02</code></td>
    <td>Jako Booking Manager chciałbym mieć podgląd do obłożenia rezerwacjami w danej lokacji (ile aktualnie jest zarezerwowanych zasobów przez kogo i na jak długo).</td>
    <td>🔄</td>
  </tr>
  <tr>
    <td><code>FR/BM/03</code></td>
    <td>Jako Booking Manager chciałbym mieć możliwość przeniesienia rezerwacji klienta na tożsamy zasób.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/BM/04</code></td>
    <td>Jako Booking Manager chciałbym mieć możliwość dodania/usunięcia z puli zasobów klienta biznesowego.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/BM/05</code></td>
    <td>Jako Booking Manager mogę rozwiązać kolejkę oczekującą na zasób.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/PK/01</code></td>
    <td>Jako potencjalny klient Deskly chciałbym mieć możliwość stworzenia konta użytkownika.</td>
    <td>🔴</td>
  </tr>
  <tr>
    <td><code>FR/PK/02</code></td>
    <td>Jako potencjalny klient Deskly chciałbym mieć możliwość akceptacji umowy/proponowania zmian w umowie/odrzucenia umowy.</td>
    <td>🔴</td>
  </tr>
</table>

### Realizacja wymagań niefunkcjonalnych

<table>
  <tr>
    <th style="width: 150px;"></th>
    <th style="width: 700px;">Wymaganie</th>
    <th style="width: 200px;">Status</th>
  </tr>
  <tr>
    <td><code>NFR/SYS/01</code></td>
    <td>System działa na urządzeniach z systemem operacyjnym macOS (w najnowszej wersji), Windows (w najnowszej wersji) oraz przeglądarkach internetowych Google Chrome, Safari, Microsoft Edge (w najnowszych wersjach).</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/SYS/02</code></td>
    <td>System działa na urządzeniach mobilnych z systemem operacyjnym Android (w najnowszej wersji) oraz iOS (w najnowszej wersji).</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/SYS/03</code></td>
    <td>System powinien obsługiwać bazę danych o wysokiej wydajności, wspierającą relację pomiędzy obiektami (PostgreSQL 17.2).</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/SYS/04</code></td>
    <td>Wszystkie usługi powinny działać w chmurze AWS i wspierać mechanizmy auto-skalowania.</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/SYS/05</code></td>
    <td>System powinien integrować się z zewnętrznymi dostawcami poczty elektronicznej oraz systemami kontroli dostępu (generowanie kodów QR).</td>
    <td>🔄</td>
</tr>
<tr>
    <td><code>NFR/SYS/06</code></td>
    <td>System powinien wymagać weryfikacji użytkownika poprzez e-mail przy zakładaniu konta</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/PER/01</code></td>
    <td>System powinien być w stanie obsłużyć jednoczesne logowanie i rezerwacje dokonywane przez co najmniej 10.000 użytkowników (1000 zapytań na sekundę przy założeniu że użytkownik wykonuje zapytanie średnio co 10 sekund).</td>
    <td>🟡</td>
</tr>
<tr>
    <td><code>NFR/PER/02</code></td>
    <td>Czas odpowiedzi na operacje związane z rezerwacjami i dostępem do zasobów nie powinien przekraczać 2 sekund.</td>
    <td>🟡</td>
</tr>
<tr>
    <td><code>NFR/PER/03</code></td>
    <td>Czas wyszukiwania zasobów oraz generowania raportów finansowych powinien trwać poniżej 3 sekund.</td>
    <td>🟡</td>
</tr>
<tr>
    <td><code>NFR/LEG/01</code></td>
    <td>System powinien spełniać regulację GDPR (General Data Protection Regulation) w zakresie przetwarzania, przechowywania i usuwania danych osobowych użytkowników.</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/LEG/02</code></td>
    <td>Musi istnieć możliwość prowadzenia logów audytowych dla wszystkich danych związanych z negocjacją umowy oraz danych związanych z rezerwacjami.</td>
    <td>🔄</td>
</tr>
<tr>
    <td><code>NFR/SEC/01</code></td>
    <td>Dane osobowe i dane związane z rezerwacjami powinny być szyfrowane w bazie danych oraz podczas przesyłania (TLS).</td>
    <td>🔴</td>
</tr>
<tr>
    <td><code>NFR/AVA/01</code></td>
    <td>System powinien mieć dostępność na poziomie minimum 99,9%.</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/AVA/02</code></td>
    <td>W przypadku awarii, system powinien być w stanie przywrócić dostępność w ciągu maksymalnie 1h.</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/AVA/03</code></td>
    <td>Dopuszczalna jest spójność ostateczna na replikach baz danych w przypadkach takich jak: informacje o dostępnych zasobach, podgląd szczegółów rezerwacji, zarządzanie kolejkami oczekujących na zasoby, informacje o cennikach, powiadomienia o zbliżających się końcach umów.</td>
    <td>🟡</td>
</tr>
<tr>
    <td><code>NFR/SCL/01</code></td>
    <td>System powinien automatycznie skalować się w górę lub w dół w zależności od liczby aktywnych użytkowników oraz zapotrzebowania na zasoby.</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/SCL/02</code></td>
    <td>Skalowanie horyzontalne powinno umożliwiać dodawanie nowych instancji w przypadku dużego obciążenia i równomiernie dystrybuować do nich ruch.</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/SCL/03</code></td>
    <td>Architektura wdrożeniowa systemu powinna być podzielona na mikroserwisy umożliwiając niezależne skalowanie krytycznych usług (np. obsługa rezerwacji, wysyłanie kodów QR, rozliczenia).</td>
    <td>✅</td>
</tr>
<tr>
    <td><code>NFR/SUP/01</code></td>
    <td>System powinien mieć wdrożony proces wsparcia technicznego dla klientów z możliwością zgłoszeń przez aplikację.</td>
    <td>🔴</td>
</tr>
<tr>
    <td><code>NFR/SUP/02</code></td>
    <td>Zautomatyzowane monitorowanie wydajności i dostępności aplikacji oraz natychmiastowe powiadomienia dla zespołu wsparcia w przypadku wykrycia anomalii.</td>
    <td>🔵</td>
</tr>

</table>