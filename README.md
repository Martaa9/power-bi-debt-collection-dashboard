# Raport windykacyjny Power BI

Interaktywny raport Power BI wspierający analizę należności i proces windykacji. Projekt obejmuje cały proces od przygotowania i transformacji danych, przez budowę modelu i miar DAX, po finalny dashboard.

Projekt został przygotowany jako wersja demonstracyjna na potrzeby portfolio i wykorzystuje wyłącznie dane syntetyczne.

## Cel projektu

Celem raportu jest ułatwienie monitorowania portfela należności, identyfikacji obszarów wymagających uwagi oraz priorytetyzacji dalszych działań windykacyjnych.

Raport umożliwia m.in.:

* monitorowanie wartości otwartych i przeterminowanych należności,
* identyfikację największych dłużników,
* analizę faktur według poziomu istotności,
* monitorowanie klientów strategicznych,
* analizę przeterminowanych faktur klientów należących do TOP 50,
* śledzenie działań windykacyjnych i blokad,
* analizę zmian pomiędzy kolejnymi okresami raportowymi.

## Dane i logika

Źródłem raportu są cykliczne pliki Excel reprezentujące kolejne okresy raportowe oraz pomocnicze zbiory danych.

W Power Query przygotowany został proces importu, łączenia i transformacji danych. Następnie dane wykorzystano do budowy modelu Power BI oraz miar DAX odpowiadających m.in. za:

* dynamiczne określanie aktualnego okresu raportowego,
* porównywanie wartości pomiędzy okresami,
* obliczanie salda przeterminowanego,
* klasyfikację należności według przyjętych progów,
* filtrowanie klientów i faktur zgodnie z regułami biznesowymi.

Raport został przygotowany tak, aby kolejne okresy były automatycznie uwzględniane po zapisaniu nowych plików źródłowych w odpowiednim folderze. W przygotowaniu danych uwzględniono również reguły porządkujące zmiany nazw klientów oraz mapowanie danych po NIP, tak aby zachować spójność informacji pomiędzy kolejnymi okresami raportowymi.

## Podgląd raportu

### Podsumowanie należności
![Podsumowanie należności]()

### Analiza dłużników
![Analiza dłużników]()

### Działania windykacyjne
![Działania windykacyjne]()

## Technologie

* Power BI
* Power Query
* DAX
* Excel
* modelowanie danych

## Dane demonstracyjne

Wszystkie dane wykorzystane w projekcie są danymi syntetycznymi przygotowanymi wyłącznie na potrzeby portfolio. Projekt nie zawiera rzeczywistych danych klientów ani informacji poufnych.

