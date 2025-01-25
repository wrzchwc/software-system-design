# Wyniki etapu IIb - Ocena architektury systemu

- Kamil Bońkowski, 252727
- Szymon Walasik, 283393
- Jakub Wierzchowiec, 252738

Niniejszy dokument stanowi ocenę architektury systemu [System biletowy dla komunikacji miejskiej](https://github.com/PWR-ACS-SE-24/SoftwareSystemDesign/tree/main/documentation/course/e2) (stan na 19.01.2025r., commit `9106972`).

## Lista kontrolna kompletności opisu arechitektury

Lista została opracowa w oparciu o [Architecture Review Checklist - System Engineering / Overall Architecture](http://www.opengroup.org/public/arch/p4/comp/clists/syseng.htm).

Legenda:

- A - opisano w pełni
- B - opisano cześciowo
- C - nie opisano
- ND - nie dotyczy

<table>
  <tr>
    <th>Element opisu</th>
    <th>Status</th>
  </tr>
  <tr>
    <th colspan="2">Ogólne</th>
  </tr>
  <tr>
    <td>ND</td>
    <td>1. Jakie inne aplikacje i/lub systemy wymagają integracji z ocenienym systemem?</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>2. Opisz poziom integracji i strategię z każdym z nich.</td>
  </tr>
  <tr>
    <td>B</td>
    <td>3. Jak geograficznie rozproszona jest baza użytkowników?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>4. Jakie strategiczne znaczenie ma ten system dla innych społeczności użytkowników wewnątrz lub poza przedsiębiorstwem?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>5. Jakie zasoby komputerowe są potrzebne do świadczenia usług systemu użytkownikom wewnątrz przedsiębiorstwa? Poza przedsiębiorstwem, korzystając z zasobów przedsiębiorstwa? Poza przedsiębiorstwem, korzystając z własnych zasobów?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>6. Jak użytkownicy spoza macierzystego środowiska dostarczania mogą uzyskać dostęp do aplikacji i danych?</td>
  </tr>
  <tr>
    <td>C</td>
    <td>7. Jaki jest oczekiwany okres eksploatacji tej aplikacji?</td>
  </tr>
  <tr>
    <td>B</td>
    <td>8. Opisz projekt, który uwzględnia zmiany w bazie użytkowników, przechowywanych danych i technologii systemu dostarczania.</td>
  </tr>
  <tr>
    <td>A</td>
    <td>9. Jaka jest wielkość bazy użytkowników i ich oczekiwany poziom wydajności?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>10. Jakie techniki testów wydajności i obciążeniowych są używane?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>11. Jaka jest ogólna organizacja komponentów oprogramowania i danych?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>12. Jaka jest ogólna konfiguracja usług i systemu?</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>13. Jak są mapowane konfiguracje oprogramowania i danych na konfigurację usług i systemów?</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>14. Jakie technologie własnościowe (sprzętowe i programowe) są potrzebne dla tego systemu?</td>
  </tr>
  <tr>
    <td>C</td>
    <td>15. Opisz, w jaki sposób każda wersja oprogramowania może być odtworzona i ponownie wdrożona w czasie.</td>
  </tr>
  <tr>
    <td>B</td>
    <td>16. Opisz obecną bazę użytkowników i jak ta baza może się zmieniać w ciągu najbliższych 3 do 5 lat.</td>
  </tr>
  <tr>
    <td>B</td>
    <td>17. Opisz obecną geograficzną dystrybucję bazy użytkowników i jak ta baza może się zmieniać w ciągu najbliższych 3 do 5 lat.</td>
  </tr>
  <tr>
    <td>A</td>
    <td>18. Opisz, ilu obecnych lub przyszłych użytkowników potrzebuje korzystać z aplikacji mobilnie lub offline.</td>
  </tr>
  <tr>
    <td>A</td>
    <td>19. Opisz, co aplikacja ogólnie robi, główne komponenty aplikacji oraz główne przepływy danych.</td>
  </tr>
  <tr>
    <td>B</td>
    <td>20. Opisz instrumentację zawartą w aplikacji, która pozwala monitorować zdrowie i wydajność aplikacji.</td>
  </tr>
  <tr>
    <td>A</td>
    <td>21. Opisz uzasadnienie biznesowe dla systemu.</td>
  </tr>
  <tr>
    <td>B</td>
    <td>22. Opisz racjonalność wyboru języka rozwoju systemu względem innych opcji, biorąc pod uwagę początkowe koszty rozwoju i długoterminowe koszty utrzymania.</td>
  </tr>
  <tr>
    <td>C</td>
    <td>23. Opisz proces analizy systemu, który został wykorzystany do opracowania architektury systemu i wyboru produktu w fazie projektowania architektury systemu.</td>
  </tr>
  <tr>
    <td>C</td>
    <td>24. Kto poza pierwotnym klientem może korzystać z tego systemu lub czerpać z niego korzyści?</td>
  </tr>
  <tr>
    <td>C</td>
    <td>25. Jaki procent użytkowników korzysta z systemu w trybie przeglądania, a jaki w trybie aktualizacji?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>26. Jaka jest typowa długość żądań transakcyjnych?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>27. Czy potrzebujesz gwarantowanego dostarczania lub aktualizacji danych, czy system toleruje awarie?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>28. Jakie są wymagania dotyczące dostępności systemu?</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>29. Opisz, gdzie architektura systemu przestrzega lub nie przestrzega standardów.</td>
  </tr>
  <tr>
    <td>C</td>
    <td>30. Opisz podejście do planowania projektu i analizy użyte w projekcie.</td>
  </tr>
  <tr>
    <th colspan="2">Procesory/Serwery/Klienci</th>
  </tr>
  <tr>
    <td>A</td>
    <td>1. Opisz architekturę aplikacji Klient/Serwer.</td>
  </tr>
  <tr>
    <td>A</td>
    <td>2. Dodaj ilustrację do obrazu, aby pokazać, gdzie wykonywane są funkcje aplikacji.</td>
  </tr>
  <tr>
    <th colspan="2">Klient</th>
  </tr>
  <tr>
    <td>ND</td>
    <td>1. Czy funkcje inne niż prezentacja są wykonywane na urządzeniu użytkownika?</td>
  </tr>
  <tr>
    <td>B</td>
    <td>2. Opisz dane i procesy związane z pomocą udostępnianą użytkownikom.</td>
  </tr>
  <tr>
    <td>A</td>
    <td>3. Opisz technikę nawigacji ekran po ekranie.</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>4. Opisz, jak użytkownik nawigował między tą a innymi aplikacjami.</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>5. Jak uruchamiane są ta i inne aplikacje z urządzenia użytkownika?</td>
  </tr>
  <tr>
    <td>A</td>
    <td>6. Czy istnieją możliwości współdzielenia danych i procesów między aplikacjami? Jeśli tak, opisz, co jest współdzielone i za pomocą jakiej techniki/technologii.</td>
  </tr>
  <tr>
    <td>C</td>
    <td>7. Opisz wolumeny danych przesyłanych do klienta.</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>8. Jakie są dodatkowe wymagania dotyczące lokalnego przechowywania danych wspierających aplikację?</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>9. Jakie są dodatkowe wymagania dotyczące lokalnego przechowywania oprogramowania/pamięci wspierających aplikację?</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>10. Czy znane są konflikty sprzętowe/programowe lub ograniczenia pojemności spowodowane wymaganiami innych aplikacji, które mogłyby wpłynąć na użytkowników aplikacji?</td>
  </tr>
  <tr>
    <td>C</td>
    <td>11. Opisz, jak wygląd i działanie warstwy prezentacji systemu porównują się z wyglądem i działaniem innych istniejących aplikacji.</td>
  </tr>
  <tr>
    <td>B</td>
    <td>12. Opisz w jakim stopniu klient musi wspierać komunikację asynchroniczną i/lub synchroniczną.</td>
  </tr>
  <tr>
    <td>B</td>
    <td>13. Opisz, jak warstwa prezentacji systemu jest oddzielona od innych warstw obliczeniowych lub transferu danych systemu.</td>
  </tr>
  <tr>
    <th colspan="2">Serwer aplikacji</th>
  </tr>
  <tr>
    <td>ND</td>
    <td>1. Czy warstwa prezentacji i warstwa aplikacji mogą działają na oddzielnych procesorach?</td>
  </tr>
  <tr>
    <td>ND</td>
    <td>2. Czy warstwa aplikacji i warstwa dostępu do danych mogą działać na oddzielnych procesorach?</td>
  </tr>
  <tr>
    <td>C</td>
    <td>3. Czy aplikacja może być umieszczona na serwerze aplikacji niezależnie od wszystkich innych aplikacji? Jeśli nie, wyjaśnij zależności.</td>
  </tr>
  <tr>
    <td>A</td>
    <td>4. Czy można łatwo dodać dodatkowe równoległe serwery aplikacji? Jeśli tak, jaki jest mechanizm równoważenia obciążenia?</td>
  </tr>
  <tr>
    <td>B</td>
    <td>5. Czy zmierzono zapotrzebowanie aplikacji na zasoby i jaka jest wartość? Jeśli tak, czy potwierdzono pojemność planowanego serwera na poziomie aplikacji i poziomie agregacji?</td>
  </tr>
  <tr>
    <th colspan="2">Serwer danych</th>
  </tr>
  <tr>
    <td>ND</td>
    <td>1. Czy istnieją inne aplikacje, które muszą współdzielić serwer danych? Jeśli tak, proszę je zidentyfikować i opisać wymagania dotyczące danych i dostępu do danych.</td>
  </tr>
  <tr>
    <td>B</td>
    <td>2. Czy zmierzono zapotrzebowanie aplikacji na zasoby i jaka jest wartość? Jeśli tak, czy potwierdzono pojemność planowanego serwera na poziomie aplikacji i poziomie agregacji?</td>
  </tr>
</table>

## Przegląd podejść architektonicznych

Przegląd sporządzono zgodnie z [ATAM: Method for Architecture Evaluation](https://insights.sei.cmu.edu/documents/629/2000_005_001_13706.pdf).

- architektura mikroserwisów
- AWS
- AWS SQS
- AWS RDS
- AWS CloudWatch
- AWS EKS
- AWS SES
- AWS Lambda
- wzorzec API Gateway
- wzorzec sidecar
- wzorce projektowe (adapter, łańcuch odpowiedzialności, komenda, strategia)
- asynchroniczna komunikacja między serwisami
- automatyczne skalowanie
- JWT
- load balancing usług
- Kubernetes
- PostgreSQL
- Spring Boot
- Angular
- NestJS
- Hono
- Deno
- Grafana
- Health Check API
- Cypress
- renderowanie po stronie klienta
- kody QR

## Drzewo użyteczności

Charakterystyki jakościowe dobrano zgodnie z normą ISO/IEC 25010. Priorytety określono zgodnie ze wzorem `(BG, D)`, gdzie `BG` oznacza korzyść biznesową (`H` (wysoka), `M` (średnia) lub `L` (niska)), a `D` oznacza trudność implmentacyjną (`H` (wysoka), `M` (średnia) lub `L` (niska)).

<table>
  <tr>
    <th>Charakterystyka jakościowa</th>
    <th>Perspektywa oceny</th>
    <th>Scenariusz</th>
  </tr>
  <tr>
    <th rowspan="2">wydajność</th>
    <th>wydajność czasowa</th>
    <td>Użytkownik wysyła zapytanie związane z zakupem biletów lub logistyką w ramach normalnej pracy systemu, czas odpowiedzi nie przekracza 1 sekundy. (H, H)</td>
  </tr>
  <tr>
    <th>przepustowość</th>
    <td>Użytkownicy w liczbie 5000 otwierają system w ramach normalnej pracy systemu, transakcje są obsługiwane bez błędów i spadku wydajności. (H, M)</td>
  </tr>
  <tr>
    <th rowspan="2">niezawodność</th>
    <th>dostępność</th>
    <td>Użytkownik próbuje skorzystać z systemu, niezależnie od stanu środowiska, system jest dostępny przez 99.9% czasu. (H, L)</td>
  </tr>
  <tr>
    <th>odzyskiwalność</th>
    <td>Gdy w systemie wydarzy się awaria, system można przywrócić do działania w ciągu maksymalnie 1h. (H, M)</td>
  </tr>
  <tr>
    <th rowspan="2">utrzymywalność</th>
    <th>testowalność</th>
    <td>System umożliwia weryfikację poprawności jego działania za pośrednictwem szerokiej gammy testów automatycznych - jednostkowe, integracyjne, E2E, wydajnościowe.</td>
  </tr>
  <tr>
    <th>modyfikowalność</th>
    <td>Wdrożenie nowej funkcjonalności nie powinno zajmować więcej niż 10 tygodni roboczych. (M, L)</td>
  </tr>
</table>

W analizowanym projekcie nie wskazano wymagań, na podstawie których możnaby ułożyć scenariusze dotyczące charakterystyk funkcjonalność, kompatybilność, użyteczność, bezpieczeństwo, przenośność.

## Analiza wybranych scenariuszy

<table>
  <tr>
    <th>Scenariusz<code>S1</code></th>
    <td colspan="4">Użytkownik wysyła zapytanie związane z zakupem biletów lub logistyką w ramach normalnej pracy systemu, czas odpowiedzi nie przekracza 1 sekundy.</td>
  </tr>
  <tr>
    <th>Atrybut</th>
    <td colspan="4">wydajność czasowa</td>
  </tr>
  <tr>
    <th>Środowisko</th>
    <td colspan="4">Normalna praca systemu</td>
  </tr>
  <tr>
    <th>Przyczyna</th>
    <td colspan="4">Użytkownik wysyła zapytanie związane z zakupem biletów lub logistyką.</td>
  </tr>
  <tr>
    <th>Odpowiedź</th>
    <td colspan="4">Zapytanie jest obsługiwane w czasie nie większym niż 1 sekunda.</td>
  </tr>
  <tr>
    <th>Decyzje architektoniczne</th>
    <th>Wrażliwość</th>
    <th>Kompromis</th>
    <th>Ryzyko</th>
    <th>Nie-ryzyko</th>
  </tr>
  <tr>
    <td><b>archietktura mikroserwisów</b></td>
    <td><code>S1.S1</code></td>
    <td></td>
    <td><code>S1.R1</code></td>
    <td></td>
  </tr>
  <tr>
    <td><b>asynchroniczna komunikacja między serwisami</b></td>
    <td></td>
    <td><code>S1.T2</code></td>
    <td><code>S1.R2</code></td>
    <td></td>
  </tr>
  <tr>
    <td><b>PostgreSQL</b></td>
    <td><code>S1.S3</code></td>
    <td><code>S1.T3</code></td>
    <td></td>
    <td><code>S1.N3</code></td>
  </tr>
  <tr>
    <td><b>automatyczne skalowanie</b></td>
    <td><code>S1.S4</code></td>
    <td></td>
    <td></td>
    <td><code>S1.N4</code></td>
  </tr>
  <tr>
    <th>Analiza</th>
    <td colspan="4">Podjęte decyzje architektoniczne determinują wydajność czasową systemu. Architektura mikroserwisowa może utrudniać osiągnięcie zakładnych czasów przetwarzania, jednak jej zastosowanie jest zrozumiałe z perspektywy innych atrybutów jakościowych. Wybór PostgreSQL jako RDBMS jest zrozumiały, jednak moze nie być optymalny w każdym przypadku. Należy również dobrze przemyśleć dobór indeksów bazodanowych, jak również konfigurację load balancingu.</td>
    </td>
  </tr>
  <tr>
    <th>Diagram architektoniczny</th>
    <td colspan="4"><img src="./images/deployment-diagram.svg"/></td>
  </tr>
</table>

- `S1.S1`: Projekt i implementacja architektury mikroserwisowej jest trudniejszy, niż architektury monolitycznej.
- `S1.R1`: Architektura mikroserwisowa wprowadza dodatkowe opóźnienie ze względu na przesył danych przez sieć.

---

- `S1.T2`: Asynchroniczna komunikacja między serwisami zwiększa niezawodność, jednak może wprowadzać opóźnienia związane z transferem danych przez sieć.
- `S1.R2`: Osiągnięcie czasu realizacji zakupu biletu w czasie nie przekraczającym 1 sekundy może stanowić wyzwanie, ze względu na wykorzystanie co najmniej 3 kolejek.

---

- `S1.S3`: Dobór indeksów bazodanowych może istotnie wpływać na efektywność przetwarzania transakcji, zarówno korzystnie, jak i negatywnie.
- `S1.T3`: Powszechne zastosowanie PostgreSQL dla wszystkich mikroserwisów ułatwi zarządzanie modelami danych, jednak nie będzie to optymalny wybór pod kątem wydajności dla wszytkich mikroserwisów pod kątem wydajności.
- `S1.N3`: PostgreSQL to jeden z wiodących systemów do zarządzania relacyjnymi bazami danych, dobrze sprawdzający się w OLTP.

---

- `S1.S4`: Automatyczne skalowanie może zostać źle skonfigurowane (np. dobór parametrów), co może negatywnie wpływać na zużycie zasobów oraz efektywność obsługi transakcji.
- `S1.N4`: Mechanizm umożliwia optymalizację zużycia zasobów przy zmiennej liczbie użytkowników jednocześnie korzystających z systemu (np. w czasie porannych lub popołudniowych godzin szczytu).

<table>
  <tr>
    <th>Scenariusz<code>S2</code></th>
    <td colspan="4">Użytkownicy w liczbie 5000 otwierają system w ramach normalnej pracy systemu, transakcje są obsługiwane bez błędów i spadku wydajności.</td>
  </tr>
  <tr>
    <th>Atrybut</th>
    <td colspan="4">przepustowość</td>
  </tr>
  <tr>
    <th>Środowisko</th>
    <td colspan="4">Normalna praca systemu</td>
  </tr>
  <tr>
    <th>Przyczyna</th>
    <td colspan="4">5000 użytkowników korzysta jednocześnie z systemu</td>
  </tr>
  <tr>
    <th>Odpowiedź</th>
    <td colspan="4">Transakcje są obsługiwane prawidłowo i nie obserwuje się spadków w ogólnej wydajności systemu.</td>
  </tr>
  <tr>
    <th>Decyzje architektoniczne</th>
    <th>Wrażliwość</th>
    <th>Kompromis</th>
    <th>Ryzyko</th>
    <th>Nie-ryzyko</th>
  </tr>
  <tr>
    <td><b>load balancing usług</b></td>
    <td><code>S2.S1</code></td>
    <td></td>
    <td></td>
    <td><code>S2.N1</code></td>
  </tr>
  <tr>
    <td><b>automatyczne skalowanie</b></td>
    <td><code>S2.S2</code></td>
    <td></td>
    <td></td>
    <td><code>S2.N2</code></td>
  </tr>
  <tr>
    <td><b>Kubernetes</b></td>
    <td><code>S2.S3</code></td>
    <td></td>
    <td></td>
    <td><code>S2.N3</code></td>
  </tr>
  <tr>
    <td><b>AWS SQS</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td><code>S2.N4</code></td>
  </tr>
  <tr>
    <td><b>wzorzec API gateway</b></td>
    <td></td>
    <td><code>S2.T5</code></td>
    <td><code>S2.R5</code></td>
    <td><code>S2.N5</code></td>
  </tr>
  <tr>
    <th>Analiza</th>
    <td colspan="4">Ogół podjętych decyzji architektonicznych należy uznać za rozsądny i uzasadniony. Należy jednak dużą wagą nadać poprawnej konfiguracji, gdyż może ona silnie determinować przepustowość sytemu. Samodzielna implementacja API gateway może stanowić wyzwanie impmentacyjne, które można by zredukować korzystając z oferowanego przez AWS API Gateway. Nie wyspecyfikowano wymagań, których usługa nie byłaby w stanie spełnić.</td>
  </tr>
  <tr>
    <th>Diagram architektoniczny</th>
    <td colspan="4">
      <img src="./images/deployment-diagram.svg"/>
      <img src="./images/component-diagram-main.svg"/>
    </td>
  </tr>
</table>

- `S2.S1`: Load balancing może zostać źle skonfiguraowany (np. dobór parametrów, algorytm balansowania), co może negatywnie wpływać na zużycie zasobów oraz efektywność obsługi transakcji.
- `S2.N1`: Mechanizm umożliwia optymalizację zużycia zasobów poprzez równomierne rozdzielenie workloadu, co jest szczególnie przy wysokim obciążeniu systemu.

---

- `S2.S2`: Automatyczne skalowanie może zostać źle skonfiguraowane (np. dobór parametrów), co może negatywnie wpływać na zużycie zasobów oraz efektywność obsługi transakcji.
- `S2.N2`: Mechanizm umożliwia optymalizację zużycia zasobów przy zmiennej liczbie użytkowników jednocześnie korzystających z systemu (np. w czasie porannych lub popołudniowych godzin szczytu).

---

- `S2.S3`: Kuberenetes to rozbudowane narzędzie, w którym dużą rolę odgrywa prawidłowa konfiguracja, co może stanowić wyzwanie, szczególnie w początkowej fazie rozwoju systemu.
- `S2.N3`: Kubernets to zaawansowane rozwiązanie do zarządzania dużą liczbą konterów, posiadające wbudowane mechanizmy niezawodnościowe oraz adaptacyjne.

---

- `S2.N4`: Mechanizm kolejki (realizowany za pośrednictwem SQS) umożliwia rozluźnienie powiązań pomiędzy mikroserwiasmi oraz zapobiega tworzeniu się wąskich gardeł podczas złożonych transakcji.

---

- `S2.T5`: Wzorzec API gateway upraszcza integrację z aplikacjami klienckimi, jednakże wydajność oraz optymalizacja tego komponentu może stanowić wąskie gardło podczas przetwarzania transakcji.
- `S2.R5`: Samodzielna implementacja API gateway rodzi ryzyko nieoptymalności implementacji oraz może niepotrzebnie komplikować rozwój systemu.
- `S2.N5`: Wzorzec API gateway sam w sobie to "eleganckie" rozwiązanie pozwalające na uproszczenie integracji z klientami oraz centralizację niektórych funckjonalności systemu (np. uwierzytelnianie).

<table>
  <tr>
    <th>Scenariusz<code>S3</code></th>
    <td colspan="4">Użytkownik próbuje skorzystać z systemu, niezależnie od stanu środowiska, system jest dostępny przez 99.9% czasu. </td>
  </tr>
  <tr>
    <th>Atrybut</th>
    <td colspan="4">dostępność</td>
  </tr>
  <tr>
    <th>Środowisko</th>
    <td colspan="4">Niezależnie od stanu środowiska</td>
  </tr>
  <tr>
    <th>Przyczyna</th>
    <td colspan="4">Chęć skorzystania przez użytkownika z systemu</td>
  </tr>
  <tr>
    <th>Odpowiedź</th>
    <td colspan="4">Dostępność systemu przez 99.9% czasu</td>
  </tr>
  <tr>
    <th>Decyzje architektoniczne</th>
    <th>Wrażliwość</th>
    <th>Kompromis</th>
    <th>Ryzyko</th>
    <th>Nie-ryzyko</th>
  </tr>
  <tr>
    <td><b>Kubernetes</b></td>
    <td><code>S3.S1</code></td>
    <td></td>
    <td></td>
    <td><code>S3.N1</code></td>
  </tr>
  <tr>
    <td><b>AWS</b></td>
    <td></td>
    <td><code>S3.T2</code></td>
    <td></td>
    <td><code>S3.N2</code></td>
  </tr>
  <tr>
    <td><b>architektura mikroserwisów</b></td>
    <td></td>
    <td></td>
    <td><code>S3.R3</code></td>
    <td><code>S3.N3</code></td>
  </tr>
   <tr>
    <td><b>wzorzec API gateway</b></td>
    <td></td>
    <td><code>S3.T4</code></td>
    <td><code>S3.R4</code></td>
    <td></td>
  </tr>
  <tr>
    <th>Analiza</th>
    <td colspan="4">Decyzja o korzystaniu z usług zewnętrznego dostawcy usług chmurowych to kompromis, jednakże znajdujący racjonalne uzasadnienie w przypadku analizowanego systemu. Architekutra mikroserwisowa korzystnie wpłynie na dostępność systemu, dzięki system nie posiada Single Point Of Failure. Zastosowanie Kubernetesa należy uznać za uzasdnione biorąc pod uwagę skalę systemu oraz wymagania dotyczace jego niezawaodności. K8s posiada wiele rozwiązań takich jak np. ReplicaSet, które zwiększają poziom niezawodności systemu gwarantując szybkie zastępowanie niesprawnych podów. Samodzielna implementacja API Gateway zwiększa dodatkowo złożoność systemu i naraża stabilność systemu.</td>
    </td>
  </tr>
  <tr>
    <th>Diagram architektoniczny</th>
    <td colspan="4"><img src="./images/deployment-diagram.svg"/></td>
  </tr>
</table>

- `S3.S1`: Kuberenetes to rozbudowane narzędzie, w którym dużą rolę odgrywa prawidłowa konfiguracja, co może stanowić wyzwanie, szczególnie w początkowej fazie rozwoju systemu.
- `S3.N1`: Kubernets to zaawansowane rozwiązanie do zarządzania dużą liczbą konterów, posiadające wbudowane mechanizmy niezawodnościowe (np. ReplicaSet).

---

- `S3.T2`: Korzystanie z usług zewnętrznego dostawcy chmurowych częściowo ogranicza swobodę implementacyjną oraz w zależności od skali przedsięwzięcia może być mniej opłacalne ekonomicznie, jednakże pozwala na ograniczenie wydatków związanych z infrastruktrą, i co ważniejsze, redukuje wyzwania dla zespołu inżynierskiego związane z zapewnieniem wysokiej dostępności.
- `S3.N2`: AWS to lider usług chmurowych, oferujących szeroką gammę rozwiązań zwiększającą dostępność systemów informatycznych oraz globalną siatkę centrów danych oraz serwerowni.

---

- `S3.R3`: Awaria jednego mikroserwisu może wpływać na fukcjonowanie innego, który jest od niego zależny.
- `S3.N3`: Architektura mikroserwisowa korzystnie wpływa na zapewnienie wysokiej dostępności, tworząc układ o wielu POFs (ang. points of failure).

---

- `S3.T4`: API gateway upraszcza integrację części backendowej z klientami, jednakże awaria tego kompentu odcina klientów od części backendowej systemu.
- `S3.R4`: Samodzielna implementacja API gateway rodzi ryzyko błędów w implementacji. Ten komponent jest szczególnie istotny w kontekście dostępności, dlatego, że stanowi Single Point Of Failure.

<table>
  <tr>
    <th>Scenariusz<code>S4</code></th>
    <td colspan="4">Gdy w systemie wydarzy się awaria, system można przywrócić do działania w ciągu maksymalnie 1h.</td>
  </tr>
  <tr>
    <th>Atrybut</th>
    <td colspan="4">odzyskiwalność</td>
  </tr>
  <tr>
    <th>Środowisko</th>
    <td colspan="4">Normalna praca systemu</td>
  </tr>
  <tr>
    <th>Przyczyna</th>
    <td colspan="4">Awaria systemu lub jego części znaczenie wpływająca na pracę reszty systemu</td>
  </tr>
  <tr>
    <th>Odpowiedź</th>
    <td colspan="4">Czas wymagany do przywrócenia pełnej sprawności systemu nie przekracza 1 godziny.</td>
  </tr>
  <tr>
    <th>Decyzje architektoniczne</th>
    <th>Wrażliwość</th>
    <th>Kompromis</th>
    <th>Ryzyko</th>
    <th>Nie-ryzyko</th>
  </tr>
  <tr>
    <td><b>Health Check API</b></td>
    <td></td>
    <td><code>S4.T1</code></td>
    <td><code>S4.R1</code></td>
    <td></td>
  </tr>
  <tr>
    <td><b>AWS CloudWatch</b></td>
    <td><code>S4.S2</code></td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><b>Kubernetes</b></td>
    <td><code>S4.S3</code></td>
    <td></td>
    <td></td>
    <td><code>S4.N4</code></td>
  </tr>
  <tr>
    <td><b>AWS</b></td>
    <td></td>
    <td></td>
    <td></td>
    <td><code>S4.N5</code></td>
  </tr>
  <tr>
    <th>Analiza</th>
    <td colspan="4">Decyzja o skorzystaniu z usług AWS nie stanowi ryzyka w kontekście odzyskiwalności. Zastosowanie Health Check API to kompromis pomiędzy monitorowaniem systemu (które jest jak najbardziej potrzebne), a fałszywie pozytywnymi odczytami stanu systemu. Należy dobrać interwał sprawdzeń w taki sposób, aby nie obciążać systemu przy zachowaniu wiarygoności odczytów. Zastosowanie Kubernetesa również można rozpatrywać jako dobrą praktykę, pomimo złożoności tego narzędzia.</td>
    </td>
  </tr>
  <tr>
    <th>Diagram architektoniczny</th>
    <td colspan="4">
      <img src="./images/deployment-diagram.svg"/>
    </td>
  </tr>
</table>

- `S4.T1`: Health Check API wspomaga monitrowanie stanu system generująć niewielki narzut na monitorwany system/podsystem, może jednak generować fałszywie pozytywne alaramy.
- `S4.R1`: System może raportować prawidłowe działanie, pomimo, że jego działanie może być zaburzone pomiędzy sprawdzeniami.

---

- `S4.S2`: CloudWatch to rozbudowane narzędzie do monitoriwania logów, należy je jednak skonfigurować prawidłowo, aby uniknąć fałszywych alarmów (o ile funkcja ta jest używana).

---

- `S4.S3`: Kuberenetes to rozbudowane narzędzie, w którym dużą rolę odgrywa prawidłowa konfiguracja, co może stanowić wyzwanie, szczególnie w początkowej fazie rozwoju systemu.
- `S4.N4`: Kubernets to zaawansowane rozwiązanie do zarządzania dużą liczbą konterów, posiadające wbudowane mechanizmy niezawodnościowe (np. ReplicaSet).

---

- `S4.N5`: AWS zoobowiązuje się do zapewnienia wysokiej dostępności swoim usług (pod rygorem odszkodowań), ponadto oferuje kompleksowe wsparcie techniczne dla kluczowych usług.

<table>
  <tr>
    <th>Scenariusz<code>S5</code></th>
    <td colspan="4">System umożliwia weryfikację poprawności jego działania za pośrednictwem szerokiej gammy testów automatycznych - jednostkowe, integracyjne, E2E, wydajnościowe.</td>
  </tr>
  <tr>
    <th>Atrybut</th>
    <td colspan="4">testowalność</td>
  </tr>
  <tr>
    <th>Środowisko</th>
    <td colspan="4">Testowe</td>
  </tr>
  <tr>
    <th>Przyczyna</th>
    <td colspan="4">System powinien działać poprawnie na środowisku produkcyjnym</td>
  </tr>
  <tr>
    <th>Odpowiedź</th>
    <td colspan="4">Zapewnienie mechanizmów testujących w procesie wytwórczym przekłada się stabilność i poprawność działania systemu</td>
  </tr>
  <tr>
    <th>Decyzje architektoniczne</th>
    <th>Wrażliwość</th>
    <th>Kompromis</th>
    <th>Ryzyko</th>
    <th>Nie-ryzyko</th>
  </tr>
    <tr>
    <td><b>Podejście Clean Architecture</b></td>
    <td></td>
    <td><code>S6.T1</code></td>
    <td></td>
    <td><code>S6.N1</code></td>
  </tr>
  <tr>
    <td><b>Testy jednostkowe</b></td>
    <td></td>
    <td></td>
    <td><code>S6.R1</code></td>
    <td></td>
  </tr>
    <tr>
    <td><b>Testy integracyjne</b></td>
    <td></td>
    <td><code>S6.T2</code></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td><b>Testy obciążeniowe</b></td>
    <td></td>
    <td><code>S6.T3</code></td>
    <td><code>S6.R2</code></td>
    <td></td>
  </tr>
  <tr>
    <td><b>Testy E2E</b></td>
    <td><code>S6.S1</code></td>
    <td><code>S6.T4</code></td>
    <td></td>
    <td><code>S6.R4</code></td>
  </tr>
    <tr>
    <td><b>Testy Security</b></td>
    <td><code>S6.S2</code></td>
    <td><code>S6.T4</code></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <th>Analiza</th>
    <td colspan="4"> Separacja logiki domenowej i logiki integracyjnej w podejściu Clean Architecture pozwala na łatwiejsze testowanie logiki biznesowej. Łatwiej dzięki temu wykorzystać techniki takie jak TDD (Test Driven Development) lub BDD (Behaviour Driven Development) i "odciąć" się od warstwy IO. W tym podejściu testy jednostkowe mogą zostać również re-użyte i posłużyć jako testy integracyjne, ponieważ wystarczy zmienić jedynie dostarczaną konfigurację testową. W dokumentacji nie zostały opisane narzędzia do testowania integracyjnego serwisów backendowych, do tego świetnie nadaje się biblioteka TestContainers. Włączenie testów E2E w proces CI to dobre rozwiązanie, warto pamiętać o tym, że testy te wykonują się długo i powinny być uruchamiane w określonych odstępach czasowych na odpowiednich środowiskach (np. testing, staging, UAT). Testy obciążeniowe są ważnym elementem, który definiuje jakość systemu, warto uruchamiać je cyklicznie, aby monitorować czy wprowadzane zmiany nie wprowadzają regresji w tym obszarze. Testy security takie jak testy penetracyjne pomogą w namierzeniu luk w zabezpieczeniach systemu na poziomie: architektury wdrożeniowej, konfiguracji sieciowej, zależności z innymi dostawcami. Na początkowym etapie projektu delegacja tego typu testów firmie zewnętrznej to rozsądna decyzja, w przyszłości można zastanowić się nad pozyskaniem specjalisty w tym zakresie. Dobrym pomysłem jest również wprowadzenie OWASP ZAP do procesu CI w celu minimalizacji ryzyka wprowadzenia zmian podatnych na ataki.</td>
  </tr>
</table>

- `S5.T1` - Architektura portów i adapterów zwiększa elastyczność systemu i jego testowanie, ale komplikuje jego projektowanie.
- `S5.N1` - Dzięki wyraźnemu rozdzieleniu odpowiedzialności można łatwo testować logikę domenową i logikę integracyjną.
---
- `S5.R1` - Jeżeli testy jednostkowe nie obejmują kluczowych przypadków, mogą prowadzić do przeoczenia błędów w logice aplikacji.
---
- `S5.T2` - Testy integracyjne mogą wymagać więcej czasu niż testy jednostkowe, ale oferują lepsze pokrycie współdziałania komponentów.
- `S5.N2` - Testy integracyjne pomagają zagwarantować, że system działa jako spójna całość, nawet w przypadku zmian w poszczególnych modułach.
---
- `S5.T3` - Testy obciążeniowe mogą wymagać znacznych zasobów obliczeniowych i regularnego dostosowywania.
- `S5.R2` - Jeśli testy obciążeniowe nie są odpowiednio zaprojektowane i nie są wykonywane na odpowiednim środowisku, mogą prowadzić do błędnych wniosków na temat wydajności systemu.
---
- `S5.S1` - Testy E2E są czasochłonne, co może wpływać na czas działania pipeline CI/CD i wyniki testów.
- `S5.T4` - Testy E2E będą uruchamiane wyłącznie na środowiskach stagingowych.
- `S5.R4` - Włączenie dużej ilości testów E2E w proces CI/CD na środowisku deweloperskim może spowolnić proces dostarczania
---
- `S5.S2` - Automatyczne skanowanie może generować fałszywe wyniki, które wymagają ręcznej weryfikacji.
- `S5.T5` - Testy bezpieczeństwa mogą spowolnić proces CI/CD, ale zwiększają pewność co do bezpieczeństwa systemu.

## Wyniki

Poniżej zaagregowano punkty wrażliwości, kompromisy, ryzyka oraz nie-ryzyka dla analizowanch scenariuszy.

### Punkty wrażliwości

Każdy z punktów wrażliwości stanowi potencjalne ryzyko lub nie-ryzyko. W związku z tym, każdy z punktów wrażliwości został sklasyfikowany jako ryzyko (`R`) lub nie-ryzyko (`N`).

- `S1.S1`: Projekt i implementacja architektury mikroserwisowej jest trudniejszy, niż architektury monolitycznej. (`R`)
- `S1.S3`: Dobór indeksów bazodanowych może istotnie wpływać na efektywność przetwarzania transakcji, zarówno korzystnie, jak i negatywnie. (`R`)
- `S1.S4`: Automatyczne skalowanie może zostać źle skonfiguraowane (np. dobór parametrów, algorytm balansowania), co może negatywnie wpływać na zużycie zasobów oraz efektywność obsługi transakcji. (`N`)
- `S2.S1`: Load balancing może zostać źle skonfiguraowany (np. dobór parametrów, algorytm balansowania), co może negatywnie wpływać na zużycie zasobów oraz efektywność obsługi transakcji. (`N`)
- `S2.S2`: Automatyczne skalowanie może zostać źle skonfiguraowane (np. dobór parametrów), co może negatywnie wpływać na zużycie zasobów oraz efektywność obsługi transakcji. (`N`)
- `S2.S3`: Kuberenetes to rozbudowane narzędzie, w którym dużą rolę odgrywa prawidłowa konfiguracja, co może stanowić wyzwanie, szczególnie w początkowej fazie rozwoju systemu. (`N`)
- `S3.S1`: Kuberenetes to rozbudowane narzędzie, w którym dużą rolę odgrywa prawidłowa konfiguracja, co może stanowić wyzwanie, szczególnie w początkowej fazie rozwoju systemu. (`N`)
- `S4.S2`: CloudWatch to rozbudowane narzędzie do monitoriwania logów, należy je jednak skonfigurować prawidłowo, aby uniknąć fałszywych alarmów (o ile funkcja ta jest używana). (`R`)
- `S4.S3`: Kuberenetes to rozbudowane narzędzie, w którym dużą rolę odgrywa prawidłowa konfiguracja, co może stanowić wyzwanie, szczególnie w początkowej fazie rozwoju systemu. (`N`)
- `S5.S1` - Testy E2E są czasochłonne, co może wpływać na czas działania pipeline CI/CD i wyniki testów. (`R`)
- `S5.S2` - Automatyczne skanowanie może generować fałszywe wyniki, które wymagają ręcznej weryfikacji. (`N`)

### Kompromisy

- `S1.T2`: Asynchroniczna komunikacja między serwisami zwiększa niezawodność, jednak może wprowadzać opóźnienia związane z transferem danych przez sieć.
- `S1.T3`: Powszechne zastosowanie PostgreSQL dla wszystkich mikroserwisów ułatwi zarządzanie modelami danych, jednak nie będzie to optymalny wybór pod kątem wydajności dla wszytkich mikroserwisów pod kątem wydajności.
- `S2.T5`: Wzorzec API gateway upraszcza integrację z aplikacjami klienckimi, jednakże wydajność oraz optymalizacja tego komponentu może stanowić wąskie gardło podczas przetwarzania transakcji.
- `S3.T2`: Korzystanie z usług zewnętrznego dostawcy chmurowych częściowo ogranicza swobodę implementacyjną oraz w zależności od skali przedsięwzięcia może być mniej opłacalne ekonomicznie, jednakże pozwala na ograniczenie wydatków związanych z infrastruktrą, i co ważniejsze, redukuje wyzwania dla zespołu inżynierskiego związane z zapewnieniem wysokiej dostępności.
- `S3.T4`: API gateway upraszcza integrację części backendowej z klientami, jednakże awaria tego kompentu odcina klientów od części backendowej systemu.
- `S4.T1`: HC API generuje niewielki narzut na monitorwany system/podsystem, może jednak generować fałszywie pozytywne alaramy.
- `S5.T1` - Architektura portów i adapterów zwiększa elastyczność systemu i jego testowanie, ale komplikuje jego projektowanie.
- `S5.T2` - Testy integracyjne mogą wymagać więcej czasu niż testy jednostkowe, ale oferują lepsze pokrycie współdziałania komponentów.
- `S5.T3` - Testy obciążeniowe mogą wymagać znacznych zasobów obliczeniowych i regularnego dostosowywania.
- `S5.T4` - Testy E2E będą uruchamiane wyłącznie na środowiskach stagingowych.
- `S5.T5` - Testy bezpieczeństwa mogą spowolnić proces CI/CD, ale zwiększają pewność co do bezpieczeństwa systemu.

### Ryzyka

- `S1.R1`: Architektura mikroserwisowa wprowadza dodatkowe opóźnienie ze względu na przesył danych przez sieć.
- `S1.R2`: Osiągnięcie czasu realizacji zakupu biletu w czasie nie przekraczającym 1 sekundy może stanowić wyzwanie, ze względu na wykorzystanie co najmniej trzech kolejek.
- `S2.R5`: Samodzielna implementacja API gateway rodzi ryzyko nie optymalności implementacji oraz może niepotrzebnie komplikować rozwój systemu.
- `S3.R3`: Awaria jednego mikroserwisu może wpływać na funkcjonowanie innego, który jest od niego zależny.
- `S3.R4`: Samodzielna implementacja API gateway rodzi ryzyko błędów w implementacji. Ten komponent jest szczególnie istotny w kontekście dostępności, dlatego, że stanowi pojedynczy POF.
- `S4.R1`: System może raportować prawidłowe działanie, pomimo, że jego działanie może być zaburzone pomiędzy sprawdzeniami.
- `S5.R1` - Jeżeli testy jednostkowe nie obejmują kluczowych przypadków, mogą prowadzić do przeoczenia błędów w logice aplikacji.
- `S5.R2` - Jeśli testy obciążeniowe nie są odpowiednio zaprojektowane i nie są wykonywane na odpowiednim środowisku, mogą prowadzić do błędnych wniosków na temat wydajności systemu.

### Nie-ryzyka

- `S1.N3`: PostgreSQL to jeden z wiodących systemów do zarządzania relacyjnymi bazami danych, dobrze sprawdzający się w OLTP.
- `S1.N4`: Mechanizm umożliwia optymalizację zużycia zasobów przy zmiennej liczbie użytkowników jednocześnie korzystających z systemu (np. w czasie porannych lub popołudniowych godzin szczytu).
- `S2.N1`: Mechanizm umożliwia optymalizację zużycia zasobów poprzez równomierne rozdzielenie workloadu, co jest szczególnie przy wysokim obciążeniu systemu.
- `S2.N2`: Mechanizm umożliwia optymalizację zużycia zasobów przy zmiennej liczbie użytkowników jednocześnie korzystających z systemu (np. w czasie porannych lub popołudniowych godzin szczytu).
- `S2.N3`: Kubernetes to zaawansowane rozwiązanie do zarządzania dużą liczbą konterów, posiadające wbudowane mechanizmy niezawodnościowe oraz adaptacyjne.
- `S2.N4`: Mechanizm kolejki (realizowany za pośrednictwem SQS) umożliwia rozluźnienie powiązań pomiędzy mikroserwiasmi oraz zapobiega tworzeniu się wąskich gardeł podczas złożonych transakcji.
- `S2.N5`: Wzorzec API gateway sam w sobie to "eleganckie" rozwiązanie pozwalające na uproszczenie integracji z klientami oraz centralizację niektórych funckjonalności systemu (np. uwierzytelnianie).
- `S3.N1`: Kubernetes to zaawansowane rozwiązanie do zarządzania dużą liczbą konterów, posiadające wbudowane mechanizmy niezawodnościowe (np. ReplicaSet).
- `S3.N2`: AWS to lider usług chmurowych, oferujących szeroką gammę rozwiązań zwiększającą dostępność systemów informatycznych oraz globalną siatkę centrów danych oraz serwerowni.
- `S3.N3`: Architektura mikroserwisowa korzystnie wpływa na zapewnienie wysokiej dostępności, tworząc układ o wielu POFs (ang. points of failure).
- `S4.N4`: Kubernetes to zaawansowane rozwiązanie do zarządzania dużą liczbą konterów, posiadające wbudowane mechanizmy niezawodnościowe (np. ReplicaSet).
- `S4.N5`: AWS zobowiązuje się do zapewnienia wysokiej dostępności swoim usług (pod rygorem odszkodowań), ponadto oferuje kompleksowe wsparcie techniczne dla kluczowych usług.
- `S5.N1` - Dzięki wyraźnemu rozdzieleniu odpowiedzialności można łatwo testować logikę domenową i logikę integracyjną.
- `S5.N2` - Testy integracyjne pomagają zagwarantować, że system działa jako spójna całość, nawet w przypadku zmian w poszczególnych modułach.

## Inne problemy oraz wątpliwości

- Rezygnację z SSR dla aplikacji klienckiej należy uznać za rozwiązanie mocno kompromisowe ze względu na gorsze wsparcie dla SEO (aplikacja użytku publicznego) oraz dłuższy czas renderowania aplikacji (pogorszenie web vitals).
- Stosunkowo wysokie wykorzystanie na urządzeniach mobilnych oraz wykorzystanie zasobów sprzętowych (kamera wideo) sugerowałoby implementację w formie PWA lub natywnej aplikacji mobilnej. Wybór Angulara jako technologii frontendowej w tym przypadku może nie być optymalnym wyborem, ze względu na to, że technologia ta tergetowana jest bardziej na urządzenia desktopowe (nie jest tak lightweight jak React, Flutter lub Next.js).
- Różnorodność w doborze technologii backendowych wykorzystuje agnostycyzm technologiczny REST oraz protokołu HTTP, jednak może utrudniać procesy wymiany wiedzy oraz code review pomiędzy członkami zespołu.
- Deno to niszowe środowisko uruchomieniowe JavaScript, o znacznie niższej popularności rynkowej niż Node.js, co może rodzić problemy ze wsparciem oraz kompatybilnością w fazie utrzymania systemu po jego wdrożeniu produkcyjnym.
- Samodzielna implmentacja autoryzacji rodzi ryzyko wystąpienia podatności oraz może zwiększać poziom trudności utrzymania systemu po jego wdrożeniu produkcyjnym.
- Dokumentacja nie wskazuje wprost na zastosowanie EKS, czytelnik musi domyślić się tej informacji.
- Abstrakcyjne nazwy dla podsystemów są elastyczne i mogą zmniejszać koszt utrzymania dokumentacji, jednakże nie informują o domenie, za którą odpowiada dany podsystem, co wymusza opanowanie "słownika nazw" i zwiększa poziom wejścia w architekturę projektu. (personalna opinia).
- Wymaganie niefunkcjonalne `NF/PRF/01` wymaga doprecyzowania. Zdefiniowano maksymalne czasy odpowiedzi dla 90% przypadków, nie zdefiniowano jakie są maksymalne czasy dla 10% pozostałych przypadków (nieskończone czasy są nieakceptowalne; dobrze byłoby podać estymacje lub określić czasy dla szerszych zakresów, najlepiej 99.9% lub więcej).
- Load Balancer oraz Ingress Resource nie zostały uwzględnione na diagramie wdrożenia.
- Brak informacji na temat integracji Ingress Resource z Elastic Load Balancer. Wykorzystując AWS EKS do orchiestracji mikroserwisami można zintegrować Ingress Resource z Network Load Balancerem lub Application Load Balancerem różnica jest w warstie na której operuje dany load balancer.

## Wnioski

<!-- Przepisać na tekst ciągły, na razie wolny strumień myśli -->

- Obszerne uzasadnienia dla doboru technologii oraz podejść architekotnicznych, biorące pod uwagę mocne oraz słabe strony rozważanych rozwiązań.
- Szczegółowa dokumentacja przypadków użycia w formie diagramów sekwencji.
- Optymalizacja wykorzystania umiejętności członków zespołu poprzez swobodę w wyborze technologii backendowych, co powinno przyspieszyć rozwój systemu w jego początkowej fazie.
- Dobór stosowanych instancji EC2 oraz RDS w oparciu o precyzjne estymacje oraz dane statystyczne.
- Całościowy opis strategii testowania systemu.
- Przejrzyste widoki funkcjonalne.
- Szczegółowy plan implementacji indeksów oraz endpointów.
