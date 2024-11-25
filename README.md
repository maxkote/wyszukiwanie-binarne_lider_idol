## Spis Treści:
- [1. Wyszukiwanie binarne](#1-wyszukiwanie-binarne)
- [2. Lider w zbiorze](#2-lider-w-zbiorze)
- [3. Idol w zbiorze](#3-idol-w-zbiorze)



# 1. Wyszukiwanie binarne

**Wyszukiwanie binarne** to wydajny algorytm używany do znajdowania wartości w posortowanych zbiorach danych. Jego kluczowa idea polega na dzieleniu zakresu wyszukiwania na pół w każdej iteracji, co znacznie przyspiesza proces.

## Jak działa:

1. Znajdź **środkowy element** w aktualnym zakresie (indeks: `(low + high) // 2`).
2. Porównaj szukaną wartość z elementem środkowym:
   - Jeśli jest równa: wartość została znaleziona.
   - Jeśli jest mniejsza: przeszukuj lewą połowę.
   - Jeśli jest większa: przeszukuj prawą połowę.
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
  ```python
   while low <= high:

        mid = (high + low) // 2

        # If x is greater, ignore left half
        if arr[mid] < x:
            low = mid + 1

        # If x is smaller, ignore right half
        elif arr[mid] > x:
            high = mid - 1

        # means x is present at mid
        else:
            return mid

    # If we reach here, then the element was not present
    return -1
  ```
- **Rekurencyjna**: Funkcja wywołuje samą siebie, zmniejszając zakres w każdym kroku.
 ```python


# 2. Lider w zbiorze

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

## Implementacja w Pythonie:

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
```


# 3. Idol w zbiorze

## Opis problemu
W pewnej grupie osób każda osoba może znać inne osoby, ale nie jest to relacja wzajemna (osoba A może znać osobę B, ale osoba B niekoniecznie zna osobę A). **Idol** to osoba, która:
1. Jest znana przez wszystkich w grupie.
2. Nie zna nikogo z grupy.

Idola można znaleźć, analizując macierz sąsiedztwa. Wiersze w macierzy reprezentują wiedzę danej osoby o innych, a kolumny — wiedzę o tej osobie. Przyjmujemy, że:
- Wartość `1` oznacza "zna".
- Wartość `0` oznacza "nie zna".
- Osoba nie zna samej siebie, więc na przekątnej macierzy są same zera.

## Przykładowa macierz
Przykład macierzy dla grupy 5 osób:
```python
macierz = [
    [0, 1, 0, 1, 1],  # Osoba 0
    [0, 0, 1, 0, 1],  # Osoba 1
    [0, 1, 0, 1, 1],  # Osoba 2
    [1, 1, 1, 0, 1],  # Osoba 3
    [0, 0, 0, 0, 0]   # Osoba 4 (idol)
]
```

## Algorytm Wykrywania Idola

### Kroki Algorytmu

#### 1. Znalezienie Potencjalnego Idola
- Przechodzimy przez każdy wiersz macierzy.
- Jeśli wiersz składa się wyłącznie z zer, osoba odpowiadająca temu wierszowi jest potencjalnym idolem.

#### 2. Weryfikacja Potencjalnego Idola
- Sprawdzamy kolumnę odpowiadającą potencjalnemu idolowi.
- Wszystkie elementy w tej kolumnie (z wyjątkiem przekątnej) muszą być równe `1`.
- Jeśli znajdziemy `0` w kolumnie, zbiór nie ma idola.

#### 3. Wynik
- Jeśli oba warunki są spełnione, idol został znaleziony.
- Jeśli żaden wiersz nie spełnia pierwszego warunku lub weryfikacja kolumny się nie powiedzie, idol nie istnieje.

---

## Implementacja

```python
macierz = [
    [0, 1, 0, 1, 1],
    [0, 0, 1, 0, 1],
    [0, 1, 0, 1, 1],
    [1, 1, 1, 0, 1],
    [0, 0, 0, 0, 0]
]

for i in range(len(macierz)):
    if macierz[i] == [0] * len(macierz):  # Wiersz składający się z zer
        for x in macierz[:i] + macierz[i+1:]:
            if x[i] == 0:  # Sprawdzenie kolumny
                print("Zbiór nie ma idola")
                break
        else:
            print(f"Idol to osoba {i}")
        break
else:
    print("Zbiór nie ma idola")
```
