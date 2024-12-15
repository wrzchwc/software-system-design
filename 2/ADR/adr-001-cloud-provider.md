# Architecture Decision Record: Wybór dostawcy usług chmurowych

## Kontekst

Projekt wymaga wdrożenia infrastruktury chmurowej w celu zapewnienia skalowalności, dostępności i elastyczności. Kluczowe wymagania obejmują:

- Wysoką dostępność usług (SLA powyżej 99,9%).
- Globalną infrastrukturę z centrami danych w wielu regionach.
- Bezpieczeństwo danych i zgodność z regulacjami (np. GDPR).
- Możliwość skalowania systemu w górę lub w dół w zależności od liczby aktywnych użytkowników oraz zapotrzebowania na zasoby.
- Możliwość automatyzacji procesów przy użyciu API i narzędzi DevOps.

## Decyzja

Wybieramy Amazon Web Services (AWS) jako dostawcę usług chmurowych dla projektu.

### Uzasadnienie
AWS został wybrany na podstawie następujących kryteriów:

- Doświadczenie rynkowe: AWS jest liderem na rynku chmurowym, oferującym stabilną i rozwiniętą infrastrukturę od ponad 15 lat.
- Globalna dostępność: AWS posiada największą liczbę regionów i stref dostępności spośród dostawców, co zapewnia lepsze wsparcie dla globalnych operacji.
- Szeroka gama usług: AWS oferuje najszerszy katalog usług, w tym: 
  -  ``AWS Lambda``
  -  ``S3 (Simple Storage Service)``
  -  ``EC2 (Elastic Compute Cloud)``
  -  ``RDS (Relational Database Service)``
  -  ``SQS (Simple Queue Service)``
  - ``EKS (Elastic Kubernetes Service)``
- Bezpieczeństwo i zgodność: AWS posiada certyfikaty zgodności z międzynarodowymi standardami, takimi jak ISO 27001, GDPR, SOC 2.
- Wsparcie społeczności i narzędzi: Duża społeczność użytkowników oraz dostęp do dokumentacji, kursów i wsparcia technicznego.
- Elastyczny model cenowy: AWS umożliwia płatność za rzeczywiste zużycie zasobów, co pozwala zoptymalizować koszty

Alternatywy:
- Microsoft Azure: Rozważano, jednak usługi są mniej dojrzałe w porównaniu z AWS, a integracja z rozwiązaniami spoza ekosystemu Microsoftu bywa bardziej wymagająca.
- Google Cloud Platform (GCP): Posiada lepsze wsparcie dla platformy Kubernetes, natomiast mniejszy zakres usług oraz ograniczona globalna infrastruktura zadecydowały o odrzuceniu.

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Zapewnienie wysokiej dostępności i skalowalności dzięki sprawdzonej globalnej infrastrukturze AWS.
- Łatwiejsza implementacja zaawansowanych funkcji dzięki szerokiemu zestawowi usług.
- Silne wsparcie w obszarze automatyzacji i DevOps.

### Negatywne
- Potencjalne ryzyko uzależnienia od jednego dostawcy (vendor lock-in).
- Relatywnie wyższe koszty w niektórych usługach w porównaniu do konkurencji.

## Referencje

- [Dokumentacja AWS](https://aws.amazon.com/)
- [Analiza porównawcza dostawców chmurowych 2024](https://dev.to/dkechag/cloud-provider-comparison-2024-vm-performance-price-3h4l)

## Data

`` 15/12/2024``