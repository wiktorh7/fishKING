# Savage Gear SG2 Travel: przeniesienie do milio (fishKING)

Produkt: wędka spinningowa Savage Gear SG2 Travel, dwa warianty (MEDIUM GAME i MICRO GAME).

Źródła danych:
- ceny, warianty i parametry: arkusz `10_PRODUKTÓW_WIKTOR.xlsx`,
- opis i zdjęcie: karta produktu w sklepie fatfish.pl (Savage Gear SG2 Medium Game Travel 215 cm 10-40 g 4 sekcje).

Storefront: `https://milio-fishking.test/shop/products/savage-gear-sg2-travel`
Zrzut ekranu: `savage-gear-sg2-travel.png`

## Co się udało odwzorować

- Nazwa, marka (Savage Gear), opis po polsku (własnymi słowami, nie kopia ze sklepu), tagi, zdjęcia.
- Dwa warianty jako opcja produktu `Model`:

| Wariant | SKU | Cena | Stan | Długość | Części | Ciężar wyrzutu |
|---|---|---|---|---|---|---|
| MEDIUM GAME | SG2-TRAVEL-M | 325,00 zł | 5 | 215 cm | 4 | 10-40 g |
| MICRO GAME | SG2-TRAVEL-S | 199,99 zł | 10 | 198 cm | 2 | 1-5 g |

- Cena i stan magazynowy są przypisane do wariantu.
- Zdjęcia są przypisane do wariantów (widać je osobno w koszyku).

## Czego nie ma w modelu danych milio

- **Specyfikacja techniczna** (długość, liczba sekcji, ciężar wyrzutu, długość transportowa, akcja Moderate Fast): oryginalna karta ma dla niej własną tabelę „Dane techniczne". W panelu milio nie było miejsca na atrybuty techniczne: żadnych pól na specyfikację. Jedyną opcją jest wolny tekst w opisie.
- **Kod producenta (72160):** nie został przeniesiony. Sekcji Product Identifiers nie sprawdzałem pod tym kątem.
- **Funkcje sklepu, nie modelu produktu:** raty 0%, „Zapytaj o produkt", ulubione, opinie klientów, punkty lojalnościowe.
- **Informacje o bezpieczeństwie produktu (GPSR)**, czyli dane producenta wprowadzającego: nie przeniesione, nie szukałem dla nich pola.

## Uproszczenia

- **Oryginalny sklep nie ma wariantów.** Na fatfish.pl MEDIUM GAME to osobna karta produktu, a rozmiar jest zaszyty w nazwie. W milio scaliłem dwie takie karty w jeden produkt z opcją `Model`.
- **Rozbieżność cen:** w arkuszu MEDIUM GAME kosztuje 325 zł, a w sklepie fatfish.pl 368 zł. W milio użyłem ceny z arkusza.
- **Dane transportowe** (długość 58 cm, waga 145 g) znałem tylko dla MEDIUM GAME. Dla MICRO GAME nie miałem takich danych, więc dane wysyłkowe wpisałem tylko do jednego wariantu.
- Parametry MICRO GAME (198 cm, 2 części, 1-5 g) pochodzą z arkusza, a nie z karty sklepu.

## Obejścia

- **Konwersje zdjęć nie generowały się same.** Storefront prosił o pliki `*-large` i `*-small`, których nie było w `storage/app/public/<id>/conversions/`. Komenda `media-library:regenerate --force` kończyła się komunikatem „All done!", ale nie tworzyła plików, a w kolejce nie było upadłych zadań. Skopiowałem oryginały ręcznie pod nazwy konwersji.
- **Kategoria (Collection)** nie istniała, więc utworzyłem ją ręcznie, zanim mogłem przypisać produkt.
- **Parametry techniczne:** brak pól, więc jedyne obejście to tekst w opisie.
- **Galeria na karcie produktu nie przełącza zdjęcia po wyborze modelu**, mimo że zdjęcia są przypisane do wariantów. Nie naprawiałem tego, bo to zachowanie szablonu storefrontu, a nie danych.

## Czego wymaga milio, a oryginalny sklep nie pokazuje

- **SKU i cena bazowa** już przy tworzeniu produktu, zanim powstaną warianty.
- **Typ produktu (Product Type)** jako pole obowiązkowe.
- **Marka** jako osobny rekord, który trzeba utworzyć przed użyciem.
- **Status draft:** nowy produkt jest ukryty we wszystkich kanałach i grupach klientów, dopóki go się nie opublikuje.
- **COGS (koszt zakupu):** pole, którego klient nigdy nie widzi. Przykład waluty w opisie pola to KRW, czyli odsłania koreańską konfigurację domyślną.
- **Opcje własne produktu i opcje współdzielone** to dwie osobne rzeczy (przyciski „Add Option" i „Add shared option").
- **Osobne sekcje panelu:** Availability, Pricing, Inventory, Shipping, Product Identifiers, URLs, Collections, Product Associations.
- **Błąd panelu przy zapisie opcji:** w logu pojawił się wyjątek `Undefined array key "product_option"` w widgecie opcji produktu Lunar, mimo że opcja i warianty zapisały się poprawnie.
- **Kategoria musi istnieć wcześniej:** Collections nie miały kategorii wędek spinningowych, a oryginalny sklep ma gotowe drzewo kategorii.
- **Availability:** poza publikacją (zmiana statusu z draft) nie musiałem ustawiać nic dodatkowego. W Inventory, URLs i Product Associations nie zauważyłem niczego, co wymagałoby obejścia.

## Wysyłka gabarytów

Wymiary i wagę wpisałem tylko dla jednego wariantu (dla drugiego brakowało danych). Nie sprawdzałem, czy metody wysyłki (GLS, InPost) biorą gabaryt pod uwagę, więc tego nie potwierdzam.

Dla tej wędki gabaryt nie jest problemem: według karty sklepu długość transportowa wersji MEDIUM GAME to 58 cm, bo to wędka podróżna składana na 4 części (215 cm po złożeniu do pracy).
