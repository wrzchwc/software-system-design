# Architecture Decision Record: Authentication and Authorization

## Kontekst
System wymaga uwierzytelniania i autoryzacji użytkowników. Potrzeby obejmują zarządzanie użytkownikami, obsługę logowania (np. za pomocą Google, Facebooka), skalowalność i zgodność z nowoczesnymi standardami bezpieczeństwa (OAuth2, OpenID Connect).

## Decyzja
- Uwierzytelnianie oraz zarzązanie kontami użytwkoników w systemie zostanie rozwiązane poprzez integrację z AWS Cognito
- Uwierzytelnione zapytania będą zawierały token JWT
- Spring Security zostanie wykorzystane do autoryzacji przychodzących zapytań

### Uzasadnienie

- AWS Cognito oferuje gotowe mechanizmy zarządzania użytkownikami, takie jak rejestracja, odzyskiwanie haseł, weryfikacja e-maili, MFA (Multi-Factor Authentication) i integracja z popularnymi dostawcami tożsamości (Google, Facebook, Apple) bez potrzeby samodzielnej implementacji
- AWS Cognito automatycznie skalowalnie obsługuje miliony użytkowników, eliminując konieczność konfiguracji infrastruktury w naszym systemie
- AWS Cognito zapewnia zgodność z najwyższymi standardami bezpieczeństwa, takimi jak OAuth2, OpenID Connect i SAML. Umożliwia łatwą integrację z AWS IAM i innymi usługami AWS
- Korzystając z AWS Cognito, można skoncentrować się na funkcjonalnościach aplikacji, zamiast implementować szczegóły związane z uwierzytelnianiem w Spring Security


## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Szybsze wdrożenie
- Łatwa skalowalność
- Bezpieczeństwo
- Elastyczność
- Redukcja kosztów operacyjnych

### Negatywne
- Uzależnienie od dostawcy (vendor lock-in)
- Koszta mogą rozsnąć w zależności od liczby klientów
- Mniejsza kontrola

## Referencje
- [Amazon Cognito](https://aws.amazon.com/cognito/)
- [Spring Security Documentation](https://spring.io/projects/spring-security)

## Data

``15/12/2024``