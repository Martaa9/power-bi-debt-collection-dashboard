# Dane demo raportu windykacyjnego v10

Pakiet obejmuje sześć miesięcy 11.2025–04.2026, po dwa pliki miesięcznie: stan przed blokadami i stan po działaniach windykacyjnych. Pliki w `00_Raw_data` są źródłem raportu; `01_Support_files` zawiera klientów strategicznych i miesięczne akcje; `docs/quality_check_metrics.xlsx` przedstawia kontrole.

## Chronologia faktur

- `Data wyk.` oznacza miesiąc wykonania usługi. Typowa faktura za marzec jest wystawiona na początku kwietnia i ma 14 dni na zapłatę. W poszczególnych plikach jest kilka przypadków z terminem 7 albo 30 dni.
- Dla stanu z 24.04.2026 faktury za marzec wystawiono na początku kwietnia. Ich termin płatności minął przed 24.04; dlatego mogą podlegać działaniom windykacyjnym.
- W pliku z 06.05.2026 nowe faktury za kwiecień wystawiono na początku maja. Wszystkie 105 nowych faktur są jeszcze przed terminem płatności.
- Poza dwiema drobnymi fakturami z krótkim terminem, usługi z miesiąca raportu nie tworzą salda przeterminowanego w tym samym cyklu. Dotyczy to również 2025 roku i 04.2026, dzięki czemu kategoria `niski` pozostaje obecna.
- W każdej parze plików daty wspólnych faktur są takie same, a zamknięte faktury mają daty wpłat zgodne z datą wystawienia i datą pliku.
- `Nr faktury`, `Rejestr`, `Mc_Rok`, numery wysyłek, zamówień oraz demonstracyjne numery KSeF są zgodne z miesiącem i rokiem wystawienia. `Miesiąc faktury` w raporcie należy nadal liczyć z `Data wyk.`.

## Kontrole w każdym miesiącu

- 4 faktury przeterminowane powyżej 10 tys. zł dotyczą usług wykonanych w poprzednim miesiącu.
- Są przypisane do 3 dłużników powyżej 10 tys. zł, w tym 2 klientów strategicznych TOP50.
- Liczby otwartych i przeterminowanych faktur oraz salda sprzed korekty chronologii pozostają bez zmian.
- Daty plików przypadają na dni robocze, bez 24.12 i polskich świąt ustawowych.
- Struktura 12 plików pozostała taka sama: każdy ma 1500 wierszy i 66 kolumn. Nie dodano `ExportDate`; w danych nie występuje `smsapi`.

Przykład dla 04.2026: w pliku bazowym jest 352 przeterminowanych faktur na 476 000,19 zł. W pliku końcowym z 06.05.2026 jest 288 faktur na 347 480,13 zł, co odpowiada spadkowi salda o 27%. Usługi wykonane w kwietniu odpowiadają tam tylko za 414,90 zł zaległości z dwóch drobnych wyjątków.

## Odświeżenie Power BI

Po rozpakowaniu ustaw `pProjectRoot` na folder `windykacja_demo_v10`. Aktualne źródła to:

- `Folder.Files(pProjectRoot & "\\00_Raw_data")`
- `File.Contents(pProjectRoot & "\\01_Support_files\\klienci_strategiczni.xlsx")`
- `File.Contents(pProjectRoot & "\\01_Support_files\\akcje_windykacyjne.xlsx")`

Wspierające zapytania `Przekształć plik` i `Przykładowy plik` w Power Query muszą pobierać dane z aktualnego folderu demo. `Nr faktury` pozostaje tekstem. Kolumny dat Excela są datami, a wcześniejszy krok czyszczenia tekstu może zmienić ich numery seryjne na tekst i wymagać oddzielnej konwersji.

Błąd `Funkcji SUM nie można użyć z wartościami typu String` w miarach `Blokady - miesiąc raportu` i `Akcje - aktualny miesiąc` dotyczy typu kolumny w modelu Power BI. W źródłowym arkuszu akcji miesięczne wartości są liczbami. Po przekształceniu ich w Power Query trzeba nadać kolumnie argumentu `SUM` typ liczbowy: liczba całkowita dla liczników, liczba dziesiętna dla kwot. Zmiana typów w źródle po odświeżeniu nie poprawi miary automatycznie, jeśli zapytanie później znów wymusza tekst.

Mapowanie `NIP_mapowanie` pozostaje przydatne: w historycznych miesiącach tej samej firmie mogą odpowiadać różne warianty nazwy, a NIP jest stałym kluczem.
