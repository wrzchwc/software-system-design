# Architecture Decision Record: Model Reservation

## Kontekst
System wymaga modelu który będzie zajmował się obsługą logiki związanej z rezerwacjami np. tworzenie/anulowanie/przekładanie rezerwacji, rozpoczęcie/zakończenie wynajmu. Zmiany stanu rezerwacji mają być audytowalne.

## Decyzja

- Model będzie wykorzystywał Event Sourcing w celu zapewnienia audytu zmian stanu rezerwacji.
- W celu oddzielenia operacji modyfikujących stan od operacji odczytu zostanie wykorzystane podejście CQRS (Command-Query Responsibility Segregation)

### Uzasadnienie

Typ modelu
- Core Domain

Klasa problemu
- Rywalizacja o zasoby

Model rezerwacji to jeden z kluczowych modeli w systemie, który realizuje logikę związaną z tworzeniem rezerwacji. W tym modelu zawarta jest również logika związana z naliczaniem opłat rezerwacji, stąd dzięki audytowalnym zmianom stanu rezerwacji będziemy w stanie odpowiedzieć również na pytania:  
- Z jakiego powodu rezerwacja się rozpoczęła/zakończyła ? 
- Co wpłynęło na cenę rezerwacji ?
- Jakie pośrednie zdarzenia doprowadziły do aktualnego stanu rezerwacji ?

 W przyszłości jeśli wystąpią problemy wydajnościowe związane z odtawrzaniem stanu rezerwacji z eventów, można rozważyć wprowadzenie snapshotu, natomiast na obecną chwilę nie jest to potrzebne.

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Pełna historia zmian stanu
- Elastyczność w odtwarzaniu stanu
- Odwracalność zmian
- Prostsza analiza danaych


### Negatywne
- Większa złożoność
- Przy dużej skali odtawrzanie stanu rezerwacji z eventów może wiązać się z problemami wydajnościowymi
- Wymaga dobrego zrozumienia wielowątkowości i problemów związanych z rywalizacją o zasoby
- Model ten wymaga szczególnie wysokiej jakości kodu ponieważ jest wyróżnikiem biznesowym dzięki któremu produkt zarabia


## Referencje

- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)
- [Event Sourcing i CQRS](https://bulldogjob.pl/readme/cqrs-i-event-sourcing-czyli-latwa-droga-do-skalowalnosci-naszych-systemow)

## Data

``15/12/2024``