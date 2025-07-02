# 4. Dokumentacja projektu

## 4.1 Opis problemu i jego znaczenia  
Celem projektu jest zbudowanie klasyfikatora, który na podstawie zestawu fizykochemicznych cech wina przewidzi, czy dany egzemplarz będzie oceniony jako „dobre” (quality ≥ 6) czy „słabe” (quality < 6). Automatyczna ocena jakości wina może wspierać producentów i kupujących, przyspieszając kontrolę jakości i pomagając w optymalizacji procesów produkcyjnych.

## 4.2 Szczegółowe wyjaśnienie wykorzystanych metod

- **Regresja logistyczna**  
  - Model liniowy, który estymuje prawdopodobieństwo przynależności do jednej z dwóch klas.  
  - W projekcie zastosowano skalowanie cech (`StandardScaler`), aby ułatwić konwergencję algorytmu optymalizacji oraz porównać wagi poszczególnych zmiennych.

- **Drzewo decyzyjne**  
  - Hierarchiczna struktura dzieląca przestrzeń cech według progów, dobieranych tak, aby maksymalnie rozdzielić klasy.  
  - Nie wymaga skalowania cech bo operuje na porządkowaniu wartości, a nie na ich względnych różnicach.

- **Random Forest**  
  - Zestaw wielu drzew decyzyjnych trenowanych na losowych podzbiorach cech i próbek, których wyniki są agregowane (głosowanie większościowe).  
  - Dzięki losowości i uśrednianiu redukuje overfitting pojedynczego drzewa i poprawia stabilność wyników.

## 4.3 Opis procesu implementacji i przetwarzania danych

1. **Wczytanie i wstępna eksploracja**  
   - Załadowanie zbioru „Wine Quality Dataset” z Kaggle.  
   - Wyświetlenie pierwszych wierszy, podstawowe statystyki (`df.describe()`), analiza braków i duplikatów.  

2. **Przygotowanie danych**  
   - Utworzenie binarnej zmiennej docelowej `goodquality = 1` (quality ≥ 6) lub `0` (quality < 6).  
   - Podział na zbiory treningowy i testowy (80/20), ze stratifikacją po klasach.  
   - Skalowanie cech tylko dla regresji logistycznej przy użyciu `StandardScaler`.

3. **Trenowanie i ocena modeli**  
   - Regresja logistyczna (na danych skalowanych).  
   - Drzewo decyzyjne i Random Forest (na danych w oryginalnej skali).  
   - Dla każdego modelu obliczono: dokładność (`accuracy_score`), macierz pomyłek (`confusion_matrix`) oraz raport klasyfikacji (`precision`, `recall`, `F1-score`).
