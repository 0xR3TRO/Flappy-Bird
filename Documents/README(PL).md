## Opis projektu

### Cel:

Projekt "Flappy Bird Online" ma na celu dostarczenie użytkownikom narzędzia do gry w klasyczną, prostą i wciągającą grę Flappy Bird, dostępną bezpośrednio w przeglądarce internetowej. Aplikacja umożliwia graczom kontrolowanie ptaka poprzez klikanie spacji w celu przejścia przez jak największą ilość przeszkód.

### Opis funkcji:

- **Rozgrywka:** Użytkownicy mogą grać w klasyczną grę Flappy Bird, klikając spację, aby ptak unosił się i omijał przeszkody.
- **Licznik punktów:** System śledzi i wyświetla wynik gracza na bieżąco.
- **Tablica wyników:** Przechowywanie najlepszych wyników graczy oraz możliwość przeglądania rankingów.
- **Restart gry:** Opcja szybkiego restartu gry po zakończeniu rundy.

## Analiza wymagań:

### Wymagania funkcjonalne:

- **Rozgrywka:** Użytkownik może kontrolować ptaka za pomocą klawisza spacji, który unosi ptaka, aby omijał przeszkody.
- **Licznik punktów:** Aplikacja wyświetla aktualny wynik gracza na ekranie podczas gry.
- **Tablica wyników:** Przechowywanie i wyświetlanie najlepszych wyników graczy.
- **Restart gry:** Możliwość rozpoczęcia nowej gry po zakończeniu rundy.

### Wymagania niefunkcjonalne:

- **Płynność rozgrywki:** Gra powinna działać płynnie, bez opóźnień i zacięć.
- **Interfejs użytkownika:** Prostota i intuicyjność interfejsu, umożliwiająca łatwą obsługę gry.
- **Wydajność:** Szybkie ładowanie gry oraz minimalne zużycie zasobów systemowych.

## Projekt interfejsu:

### Szkice/wizualizacje interfejsu:

- _Strona główna:_ Ekran startowy z przyciskiem do rozpoczęcia gry oraz dostępem do tablicy wyników.
- _Okno gry:_ Widok rozgrywki z ptakiem, przeszkodami, licznikiem punktów oraz przyciskiem restartu.
- _Tablica wyników:_ Lista najlepszych wyników z opcją powrotu do ekranu startowego.

### Mapa strony:

- _Strona główna_
  - Przycisk rozpoczęcia gry
  - Opcja przeglądania tablicy wyników
- _Okno gry_
  - Rozgrywka
  - Licznik punktów
  - Przyciski restartu
- _Tablica wyników_
  - Lista najlepszych wyników
  - Powrót do ekranu startowego

## Architektura systemu:

### Opis struktury danych:

Aplikacja przechowuje dane dotyczące wyników graczy, w tym:

- **Wyniki gry:** Zawiera informacje o wynikach uzyskanych przez graczy.
- **Parametry gry:** Dane dotyczące aktualnej rozgrywki, takie jak pozycja ptaka i przeszkód.

### Diagramy architektury:

Architektura oparta jest na strukturze MVC, gdzie:

- **Model:** Odpowiada za logikę gry, zarządzanie punktami i przechowywanie wyników.
- **Widok (View):** Prezentuje interfejs użytkownika.
- **Kontroler (Controller):** Zarządza komunikacją między modelem a widokiem.

## Implementacja:

### Opis technologii:

- **Frontend:** HTML, CSS, JavaScript (React.js).
- **Backend:** Node.js (do obsługi tablicy wyników).
- **Baza danych:** SQLite (przechowywanie wyników graczy).

### Struktura kodu:

- _Katalogi/pliki_: Oddzielne pliki dla logiki gry, interfejsu użytkownika i zarządzania danymi.
- _Style pisania kodu_: Zastosowanie modularności, czytelności i komentarzy w kodzie.

## Testowanie:

### Plan testów:

- **Testy jednostkowe:** Sprawdzenie poprawności działania funkcji kontrolujących ptaka i przeszkody.
- **Testy integracyjne:** Upewnienie się, że wszystkie komponenty współpracują ze sobą poprawnie.
- **Testy interfejsu użytkownika:** Sprawdzenie interakcji z użytkownikiem na różnych urządzeniach.
- **Testy wydajnościowe:** Ocena płynności działania gry w różnych warunkach.

### Procedury testowania:

- Opracowanie zestawu przypadków testowych dla każdej funkcji gry.
- Ustalenie procedur raportowania i naprawiania znalezionych błędów.

## Wdrożenie i konserwacja:

### Plan wdrożenia:

- **Etapy wdrażania:** Testowanie, poprawki, publikacja na platformach dostępnych dla użytkowników.
- **Terminy:** Określenie dat planowanych etapów.

### Procedury konserwacji:

- **Wsparcie techniczne:** Ustanowienie kanałów komunikacji z użytkownikami w celu zgłaszania problemów.
- **Aktualizacje:** Planowanie regularnych aktualizacji w zależności od potrzeb i feedbacku użytkowników.

## Harmonogram:

### Plan projektu:

- **Etapy realizacji:** Podział prac na konkretne zadania (np. implementacja logiki gry, interfejsu, testowanie).
- **Terminy:** Określenie czasu potrzebnego na każdy etap.

## Kosztorys:

### Szacunkowe koszty:

- **Rozwój aplikacji:** Wg godzin pracy lub zespołu programistów.
- **Koszty utrzymania:** Serwery, ewentualne opłaty za usługi zewnętrzne, wsparcie techniczne.

---

[English](/README.md)
