# Architecture Decision Record: Model Contract Negotiations

## Kontekst
System musi realizować wymagania biznesowe związane z negocjowaniem kontraktu z klientami biznesowymi.

## Decyzja

Logika związana z negocjacjami kontraktu będzie realizowana przez osobny model.

### Uzasadnienie

Typ modelu:
- Product

Klasa problemu:
- Konkurencja o zasoby

W wyniku event stormingu zauważono że negocjacja kontraktu potrzbuje osobnego modelu niż ten do zarządzania dokumentami. Pomimo tego że jest to dokument którego pola podlegają negocjacji to operacje które przez to można na nim wykonywać są zupełnie inne niż w przypadku tworzenia draftów umowy. Ponadto wymagana jest przy tym spójność na poziomie transakcyjnym ponieważ negocjowana umowa może być modyfikowana przez wiele osób jednocześnie i wiąże się z blokowaniem zasobów na czas negocjacji.

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Brak splątania klas problemów
- Separacja odpowiedzialności
- Elastyczność i łatwość zmian

### Negatywne
- Wymaga dobrego zrozumienia wielowątkowości i problemów związanych z konkurencją o zasoby


## Referencje

- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)

## Data

``15/12/2024``