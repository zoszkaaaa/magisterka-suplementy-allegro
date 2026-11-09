# Analiza rynku suplementów w formie żelków – aplikacja badawcza

Aplikacja do pracy magisterskiej (SGH, kierunek Analiza Danych – Big Data).
Status: **pilotaż / faza testów**. Aplikacja działa wyłącznie na potrzeby własnego konta.

## 1. Opis i cel aplikacji

Aplikacja to skrypt w Pythonie uruchamiany lokalnie, służący do zebrania danych
do pracy magisterskiej o rynku suplementów diety w formie żelków w Polsce.
Z Allegro korzysta wyłącznie w trybie **odczytu**: pobiera dane z katalogu produktów
(nazwa, kategoria, parametry, w tym kod EAN/GTIN, marka, producent, liczba sztuk),
aby ocenić jakość i kompletność danych katalogowych w wybranych segmentach
(np. sen, uroda, odporność, dzieci).

Aplikacja **nie** wystawia ofert, nie zmienia danych na koncie, nie obsługuje zamówień,
płatności ani wiadomości.

## 2. Zakres funkcjonalny

| Funkcja | Opis |
|---|---|
| Wyszukiwanie produktów w katalogu | Wyszukiwanie produktów po frazie (np. „melatonina żelki”) |
| Odczyt parametrów produktu | Pobranie parametrów produktu (EAN/GTIN, marka, producent, liczba sztuk, skład) |
| Raport jakości danych | Lokalne obliczenie, jaki odsetek produktów ma wypełnione poszczególne pola |

Częstotliwość: uruchamiane ręcznie, kilkadziesiąt–kilkaset zapytań na jedno uruchomienie,
z przerwami między zapytaniami.

## 3. Sposób połączenia z Allegro

- OAuth 2.0 – **Device Flow** (aplikacja bez dostępu do przeglądarki).
- Skrypt wyświetla link weryfikacyjny; autorka loguje się na swoje konto Allegro
  w przeglądarce i zatwierdza dostęp. Skrypt pobiera token i odświeża go za pomocą refresh tokena.

## 4. Wykorzystanie Allegro API i uprawnienia

| Scope | Funkcja aplikacji | Wykorzystanie |
|---|---|---|
| `allegro:api:sale:offers:read` | Wyszukiwanie i odczyt produktów z katalogu | Pobieranie danych produktów i ich parametrów (tylko odczyt) |

Wykorzystywane zasoby: `GET /sale/products`, `GET /sale/products/{id}`, `GET /sale/categories`, `GET /me`.

## 5. Dostęp i bezpieczeństwo danych

- Aplikacja działa lokalnie na prywatnym komputerze autorki; nie ma interfejsu webowego ani innych użytkowników.
- Client ID, Client Secret i tokeny OAuth są przechowywane lokalnie w plikach wyłączonych z repozytorium
  (`.env`, `.allegro_token.json`) i nie są nikomu udostępniane.
- Pobierane są wyłącznie dane katalogowe produktów; aplikacja nie pobiera danych osobowych innych użytkowników.
- Dane są wykorzystywane wyłącznie w celach naukowych, w formie zagregowanej.

## 6. Dane kontaktowe

Zofia Soszka – e-mail: **thestargummy@gmail.com**
