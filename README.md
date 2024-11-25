# Wyszukiwanie binarne – Notatka

**Wyszukiwanie binarne** to wydajny algorytm używany do znajdowania wartości w posortowanych zbiorach danych. Jego kluczowa idea polega na dzieleniu zakresu wyszukiwania na pół w każdej iteracji, co znacznie przyspiesza proces.

## Jak działa:

1. Znajdź **środkowy element** w aktualnym zakresie (indeks: `(low + high) // 2`).
2. Porównaj szukaną wartość z elementem środkowym:
   - Jeśli równa: wartość została znaleziona.
   - Jeśli mniejsza: przeszukuj lewą połowę.
   - Jeśli większa: przeszukuj prawą połowę.
3. Powtarzaj, aż znajdziesz wartość lub zakres stanie się pusty.

## Kluczowe cechy:
- **Efektywność**: Czas działania wynosi O(log n), ponieważ liczba porównań zmniejsza się o połowę z każdym krokiem.
- **Wymagania**: Zbiór danych musi być **posortowany**.
- **Elastyczność**: Może być zaimplementowany iteracyjnie lub rekurencyjnie.

## Przykłady zastosowań:
- **Bazy danych**: Szybkie wyszukiwanie rekordów.
- **Nauka o danych**: Znajdowanie wartości w dużych, posortowanych zbiorach.
- **Grafika komputerowa**: Algorytmy takie jak śledzenie promieni.

## Porównanie z innymi algorytmami:
- **Wyszukiwanie liniowe**: Przeszukuje dane jeden po drugim (czas O(n)), ale nie wymaga sortowania.

## Implementacje w Pythonie:
- **Iteracyjna**: Używa pętli, aby zmniejszać zakres.
- **Rekurencyjna**: Funkcja wywołuje samą siebie, zmniejszając zakres w każdym kroku.
