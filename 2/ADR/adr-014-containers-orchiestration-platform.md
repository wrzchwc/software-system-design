# Architecture Decision Record: Wybór platformy do orchiestracji kontenerów

## Kontekst
System wymaga zarządzania kontenerami w sposób skalowalny, elastyczny i niezawodny. Aplikacją, która musi działać w środowisku rozproszonym z możliwością dynamicznego skalowania zasobów w odpowiedzi na zmieniające się obciążenie. Zależy nam na automatyzacji procesów wdrażania, monitorowania i utrzymywania aplikacji.

## Decyzja

Wybieramy Amazon Elastic Kubernetes Service (EKS) jako platformę do zarządzania kontenerami


### Uzasadnienie

- Eliminuje konieczność samodzielnego zarządzania klastrem Kubernetes, co zmniejsza obciążenie operacyjne
- Integruje się z innymi usługami AWS, takimi jak IAM (zarządzanie tożsamościami), CloudWatch (monitorowanie), ALB/ELB (load balancing) czy EBS (dyski)
- AWS oferuje zaawansowane mechanizmy bezpieczeństwa, w tym izolację sieci (VPC), kontrolę dostępu na poziomie ról (Role Based Access Control) i integrację z AWS IAM
- Automatycznie obsługuje skalowanie w górę i w dół w zależności od obciążenia aplikacji
- AWS zapewnia infrastrukturę dostępną w wielu regionach, co pozwala na łatwe wdrożenie aplikacji w różnych lokalizacjach geograficznych

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- EKS automatyzuje wiele zadań związanych z zarządzaniem Kubernetes, co pozwala zespołowi skupić się na rozwoju aplikacji
- Wysoka dostępność
- Lepsza wydajność
- Bezproblemowa integracja z narzędziami DevOps
- Skalowalność
- Wsparcie i społeczność

### Negatywne
- EKS generuje koszty za zarządzanie klastrem oraz za inne usługi AWS (np. EC2, S3, CloudWatch), co może być droższe w porównaniu z samodzielnie zarządzanym Kubernetes
- Zależność od dostawcy usługi (vendor lock-in)
- Pomimo automatyzacji, EKS dalej jest złożoną platformą do konfigurowania
- Wymagana wiedza o AWS

## Referencje
- [Amazone Elastic Kubernetes Service](https://aws.amazon.com/eks/)
- [Kubernetes Documentation](https://kubernetes.io/)
- [Docker Documentation](https://docs.docker.com/)
- [What is a container ?](https://www.docker.com/resources/what-container/)

## Data

``15/12/2024``