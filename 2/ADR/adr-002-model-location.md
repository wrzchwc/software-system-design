# Architecture Decision Record: Model Location

## Kontekst
System potrzebuje modelu który będzie służył jako źródło prawdy na temat szczegółów odnośnie lokacji i zasobów którymi dysponuje klient. Ponadto model powinien efektywnie realizować wymgania funkcjonalne dotyczące: 
- Tworzenia/Modyfikacji/Archiwizacji lokacji
- Tworzenia/Modyfikacji/Archiwizacji zasobu
- Przypisywani zasobu do lokacji
- Wypisywania zasobu z lokacji

## Decyzja
- Metadane dotyczące zasobów oraz lokacji powinny być razem odczytywane, modyfikowane i zapisywane.
- Inforamcje dotyczące relacji pomiędzy zasobami i lokacjami powinny być razem odczytywane, modyfikowane i zapisywane.
- Informacje dotyczące godzin otwarcia powinny być razem odczytywane modyfikowane i zapisywane.

### Uzasadnienie
Typ modelu:
  - Product

Klasa problemu:
  - CRUD

- Akcje wpływające na inne komponenety systemu
  - Przypisanie zasobu do lokacji
  - Wypisanie zasobu z lokacji
  - Modyfikacja godzin otwarcia lokacji
  - Archiwizacja lokacji (wiąże sie z wypisaniem zasobu z lokacji)
  - Archiwiazcja zasobu (wiąże sie z wypisaniem zasobu z lokacji)

- Akcje nie wpływające na inne komponenety systemu
  - Stworzenie nowego zasobu
  - Stworzenie nowej lokacji
  - Modyfikacja metadanych zasobu: nazwa, zdjęcia, typ, atrybuty
  - Modyfikacja metadanych lokacji: nazwa, opis, zdjęcia, email, adres, numer telefonu

Operacje tworzenia lokacji i zasobów oraz ich modyfikacji nie wpływają na inne elementy systemu (są stabilne) wiąc powinny zmieniać się i być odczytywane razem. Przypisanie/wypisanie zasobu do/z lokacji powoduje przeliczenie dostęności zasobu, stąd te dane muszą zmieniać się oddzielnie od metadanych. Podobnie jest z modyfikajcą/zdefiniowaniem godzin otwarcia lokacji. Dane te również muszą zmieniać się oddzielnie ponieważ również wpływaja na przeliczenie dostępności zasobu.

## Status

Zaakceptowane

## Konsekwencje

### Pozytywne
- Odseparowanie operacji stabilnych od niestabilnych.
- Operacje tworzenia i modyfikowania metadanych dla zasobów i lokacji nie wpływają na resztę systemu.
- Informawanie innych komponentów systemu jedynie o fakcie przypisania/wypisania zasobu do/z lokacji oraz zmianach godzin otwarcia.
- Szybsze odczyty i zapisy przy operacjach na metadanch.

### Negatywne
- Większa złożoność systemu

## Referencje

- [Mapa kontekstów](https://github.com/wrzchwc/software-system-design/blob/main/1/README.md#mapa-kontekst%C3%B3w)


## Data

``15/12/2024``