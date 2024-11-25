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


# Lider w zbiorze - Notatka

**Lider** w zbiorze to liczba, która występuje więcej niż **n/2** razy, gdzie **n** to liczba elementów w zbiorze. 

### Przykłady:
- Zbiór: `{1, 4, 6, 1, 1}` – Liderem jest liczba **1**, ponieważ występuje 3 razy, a `5 / 2 = 2.5` i 3 > 2.
- Zbiór: `{8, 6, 4, 5, 3, 2}` – Brak lidera, ponieważ żadna liczba nie występuje więcej niż 3 razy.

## Właściwości zbiorów z liderem:
- Jeśli zbiór ma lidera, usunięcie dwóch różnych liczb (nawet lidera i innej liczby) nie zmienia lidera.
- W wyniku usuwania par elementów ze zbioru:
  1. Jeśli zbiór stanie się pusty, nie ma lidera.
  2. Jeśli zostanie jeden element, to sprawdza się, czy jest liderem.
  3. Jeśli pozostały elementy są identyczne, ten element jest liderem.

## Algorytm wyszukiwania lidera:
1. **Algorytm** opiera się na eliminowaniu par elementów:
   - Inicjujemy lidera jako pierwszy element i licznik wystąpień (n = 1).
   - Iterujemy po zbiorze i porównujemy bieżący element z liderem:
     - Jeśli się zgadzają, zwiększamy licznik.
     - Jeśli się różnią, zmniejszamy licznik.
     - Gdy licznik spada do 0, nowym liderem staje się bieżący element.
2. Następnie liczymy wystąpienia lidera w zbiorze:
   - Jeśli występuje więcej niż **n/2** razy, to jest liderem.
   - W przeciwnym razie, zbiór nie ma lidera.
  
## Złożoność obliczeniowa:
- Algorytm wyszukiwania lidera jest efektywny, ponieważ pozwala na znalezienie lidera w O(n) czasie, eliminując konieczność wielokrotnego sprawdzania każdej liczby.

### Implementacja w Pythonie:

```python
zbior = [1, 3, 3, 2, 5, 5, 3, 3, 3, 3, 1]
lider = zbior[0]
n = 1
for i in range(1, len(zbior)):
    if n > 0:
        if lider == zbior[i]:
            n = n + 1
        else:
            n = n - 1
    else:
        lider = zbior[i]
        n = 1

if n == 0:
    print("Zbiór nie ma lidera")
    exit()

liczba_wystapien_lidera = 0
for i in range(0, len(zbior)):
    if zbior[i] == lider:
        liczba_wystapien_lidera += 1

if liczba_wystapien_lidera > len(zbior) / 2:
    print("Liderem zbioru jest ", lider)
else:
    print("Zbiór nie ma lidera")

