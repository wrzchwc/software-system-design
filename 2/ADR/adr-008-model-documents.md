# Architecture Decision Record: Model Contracting

## Kontekst
System musi umożliwiać przechowywanie dokumnetów takich jak faktury, drafty umów, podpisane umowy.

## Decyzja

Logika składowania dokumentów będzie realizowana przez osobny model i będzie wykorzystywała do tego integrację z AWS S3 Bucket. 

### Uzasadnienie

Typ
- Product

Klasa problemu:
- CRUD

Implementacja modelu jako integracja z AWS S3 (Simple Storage Service) jest tanim rozwiązaniem pod kątem czasowym. Koszty związane z przechowywaniem plików w tym serwisie również nie są drogie, dla planu S3 Standard za pierwsze 50TB to jedynie 0.023$/GB co miesiąc. Model w takim rozwiązaniu jest wysoce konfigurowalny i gotowy na zmianę wymagań funkcjonalnych w tym zakresie. 

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Wykorzystanie sprawdzonego rozwiązania z rynku
- Tanie koszty dewelopmentu i utrzymania
- Elastyczność i skalowalność
- S3 zapewnia trawałość danych na poziomie 99,99999999999% co znacząco minimalizuje ryzyko utraty danych
- Bezpieczeństwo i wysoka wydajność

### Negatywne
- Wiązanie się z jednym dostawcą usługi (vendor lock-in)

## Referencje

- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)
- [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/)
- [Amazon S3 Overview](https://aws.amazon.com/s3/?nc=sn&loc=0)

## Data

``15/12/2024``