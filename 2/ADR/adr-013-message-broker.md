# Architecture Decision Record: Wybór Message Brokera

## Kontekst
System  wymaga skalowalnej i niezawodnej komunikacji asynchronicznej pomiędzy różnymi komponentami. Potrzebujemy rozwiązania do kolejkowania wiadomości, które pozwoli na odseparowanie producentów i konsumentów wiadomości, a także zapewni mechanizmy niezawodności i tolerancji błędów.

## Decyzja

Wybieramy Amazon Simple Queue Service (SQS) jako głównego mechanizm kolejkowania wiadomości w projekcie

### Uzasadnienie
- SQS oferuje mechanizmy wysokiej dostępności i trwałości danych dzięki replikacji w wielu strefach dostępności AWS
- Automatycznie skalująca się infrastruktura SQS pozwala obsłużyć od kilku do milionów wiadomości na sekundę, dostosowując się do potrzeb projektu
- Umożliwia implementację zarówno kolejek FIFO (First-In-First-Out) do zapewnienia kolejności przetwarzania, jak i Standard Queues dla większej przepustowości
- Łatwa integracja z innymi usługami AWS, takimi jak AWS Lambda, Amazon SNS czy Amazon S3, co ułatwia tworzenie bardziej złożonych systemów
- Obsługuje szyfrowanie wiadomości w spoczynku i w transporcie oraz kontrolę dostępu za pomocą IAM
- Jest to rozwiązanie ekonomiczne dzięki modelowi płatności za użycie (pay-as-you-go)
- Posiada mechanizm nadawania atrybutów dla wiadomości dzięki czemu przy implementacji architektury multi-tenant będzie można selektywnie czytać z kolejki eventy kontkretnego tenanta i konsumować je równolegle

Rozpatrywano również alternatywne rozwiązania tekie jak: Kafka, ActiveMQ. Są to wysoko konfigurowalne rozwiązania i też z tego powodu wprowadzają dodatkową złożoność która nie jest potrzebna na tym etapie projektu. Na ten moment SQS spełnia wszystkie wymagania dotycznące komunikacji pomiędzy mikrousługami i jest prostszy w konfiguracji. 

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Odseparowanie komponentów
- Zwiększona niezawodność
- Łatwe skalowanie
- Redukcja złożoności
- Szybka reakcja na zwiększone obciążenie

### Negatywne
- Opóźnienia
- Koszty przy dużej skali
- Konieczność samodzielnego zarządzania logiką przetwarzania wiadomości
- Uzależnienie się od usługi jednego dostawcy (vendor lock-in)

## Referencje
- [Amazon Simple Queue Service](https://aws.amazon.com/sqs/)
- [ActiveMQ vs Kafka](https://quix.io/blog/activemq-vs-kafka-comparison)
- [Kafka Documentation](https://kafka.apache.org/20/documentation.html)
- [ActiveMQ Documentation](https://activemq.apache.org/components/classic/documentation/)


## Data

``15/12/2024``