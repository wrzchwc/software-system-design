# Architecture Decision Record: Model Pricing

## Kontekst

System potrzebuje modelu który będzie źródłem prawdy na temat aktualnych cen, cenników w lokacjach, ceny wynajmu zasobu dla konkretnego klienta.

## Decyzja

Logika dotycząca cen będzie realizowana przez osobny model.


### Uzasadnienie

W przyszłości logika modelu może znacząco się rozszerzyć stąd powinna być enkapsulowana w jednym miejscu. Model ten poimo aktualnych wymagań związanych jedynie z dodawaniem  i modyfikowaniem cennników, będzie przygotowany na wymgania które mogą pojawić się w przyszłości np. obsługa rabatów. 

Typ modelu:
- Product

Klasa problemu
- CRUD

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Separacja odpowiedzialności
- Elastyczność i łatwość zmian
- Reużywalność
- Ograniczone zażądzanie złożonością

### Negatywne
- Logika modelu może być złożona i wymagać wiedzy z zakresu finansów

## Referencje

- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)

## Data

``15/12/2024``