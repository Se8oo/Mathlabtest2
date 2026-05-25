# Instrukcja wykonania zadania na zaliczenie

Instrukcja powstała na podstawie pliku `transkrypcja_i_opis.md`. Opisuje praktyczny przebieg pracy w MATLAB-ie i Simulinku: od uruchomienia modelu, przez identyfikację obiektu, aż po przygotowanie wyników do szablonu zaliczenia.

> Uwaga: w miejscach, gdzie w materiałach prowadzącego są konkretne wzory lub nazwy plików, użyj dokładnie tych danych z repozytorium. Poniżej jest procedura robocza, a nie zamiennik oficjalnych materiałów.

## 1. Przygotowanie folderu

1. Pobierz całe repozytorium albo wypakuj paczkę z materiałami.
2. Wszystkie pliki trzymaj w jednym katalogu:
   - model Simulinka (`.slx` albo `.mdl`),
   - skrypt MATLAB-a (`.m`),
   - materiały pomocnicze,
   - przykładowe zadanie,
   - szablon zaliczenia/sprawozdania.
3. W MATLAB-ie ustaw ten katalog jako bieżący folder roboczy.
4. Nie przenoś pojedynczych plików między folderami, bo model może zgubić ścieżki.

## 2. Otworzenie i uruchomienie modelu

1. Uruchom MATLAB.
2. Otwórz Simulink.
3. W Simulinku wybierz `Open File` i otwórz program/model z repozytorium.
4. Jeśli model zawiera zablokowane bloki, nie rozbijaj ich i nie edytuj środka, jeśli nie jest to wymagane w poleceniu.
5. Wpisz dane wymagane w zadaniu:
   - numer indeksu,
   - wartości wynikające z indeksu,
   - parametry podane w przykładzie,
   - wartości z materiałów pomocniczych.
6. Uruchom symulację.
7. Sprawdź, czy pojawiają się wykresy wejścia i wyjścia oraz czy odpowiedź układu wygląda logicznie.

## 3. Eksport danych z Simulinka do MATLAB-a

Po uruchomieniu symulacji dane powinny trafić do zmiennej typu `out`. W transkrypcji pojawia się ścieżka w stylu:

```matlab
out.scopeData.signals(...).values
```

Najczęściej potrzebujesz:

```matlab
t = out.tout;                         % czas, jeśli jest dostępny
u = out.scopeData.signals(1).values;   % sygnał wejściowy / wymuszenie
y = out.scopeData.signals(2).values;   % sygnał wyjściowy / odpowiedź obiektu
```

Jeśli kolejność sygnałów jest inna, sprawdź w strukturze `out.scopeData.signals`, który sygnał jest wejściem, a który wyjściem.

Dla wygody możesz od razu zrobić wykres:

```matlab
figure;
subplot(2,1,1);
plot(t, u);
grid on;
title('Sygnał wejściowy');
xlabel('t');
ylabel('u');

subplot(2,1,2);
plot(t, y);
grid on;
title('Sygnał wyjściowy');
xlabel('t');
ylabel('y');
```

## 4. Wybór fragmentu do identyfikacji

Identyfikację wykonuje się na odpowiedzi po skoku wymuszenia.

1. Znajdź moment, w którym wejście `u` zmienia wartość.
2. Odczytaj wartość wejścia przed skokiem i po ustaleniu:

```matlab
u0 = ...;   % wartość wejścia przed skokiem
u1 = ...;   % wartość wejścia po skoku
```

3. Odczytaj wartość wyjścia przed skokiem i po ustaleniu:

```matlab
y0 = ...;   % wartość wyjścia przed skokiem
y1 = ...;   % wartość wyjścia po ustaleniu
```

4. Nie wybieraj punktów przypadkowo. Początek ma być przed skokiem, a koniec wtedy, gdy odpowiedź jest już ustalona.
5. Jeśli po obliczeniach wychodzi `Inf`, bardzo często oznacza to dzielenie przez zero, np. źle wybrane `u0` i `u1` albo pomylony sygnał.

## 5. Obliczenie wzmocnienia obiektu

Wzmocnienie obiektu liczysz jako stosunek zmiany wyjścia do zmiany wejścia:

```matlab
du = u1 - u0;
dy = y1 - y0;

K = dy / du;
```

Sprawdź:

- `du` nie może być zerem,
- `K` powinno mieć sensowną wartość,
- znak `K` powinien pasować do wykresu: jeśli wyjście rośnie po wzroście wejścia, `K` powinno być dodatnie.

## 6. Punkty 10% i 90%

Dla obiektu inercyjnego z opóźnieniem potrzebne są punkty odpowiadające około 10% i 90% całej zmiany odpowiedzi.

1. Znormalizuj odpowiedź:

```matlab
yn = (y - y0) / (y1 - y0);
```

2. Znajdź próbki, w których odpowiedź przekracza 10% i 90%:

```matlab
i10 = find(yn >= 0.10, 1, 'first');
i90 = find(yn >= 0.90, 1, 'first');

t10 = t(i10);
t90 = t(i90);
```

3. Jeżeli odpowiedź maleje zamiast rosnąć, warunek trzeba odwrócić albo normalizację wykonać tak, aby `yn` rosło od 0 do 1.
4. Na wykresie zaznacz te punkty, bo będą potrzebne do uzasadnienia w sprawozdaniu:

```matlab
figure;
plot(t, yn);
hold on;
plot(t10, yn(i10), 'r*');
plot(t90, yn(i90), 'g*');
grid on;
legend('odpowiedź znormalizowana', '10%', '90%');
```

## 7. Obliczenie stałej czasowej i opóźnienia

Dla modelu inercyjnego z opóźnieniem przyjmuje się postać:

```text
        K
G(s) = ----- * exp(-theta*s)
       T*s+1
```

gdzie:

- `K` - wzmocnienie,
- `T` - stała czasowa,
- `theta` albo `tau` - opóźnienie.

Z transkrypcji wynika, że stała czasowa była liczona z punktów 10%-90%:

```matlab
T = (t90 - t10) / 2.2;
```

Jeśli liczysz opóźnienie metodą 10%-90%, możesz użyć zależności:

```matlab
theta = t10 - 0.105 * T - tStep;
```

gdzie `tStep` to czas wystąpienia skoku wejścia. Jeżeli wcześniej przesuniesz czas tak, że skok jest w chwili `0`, wtedy:

```matlab
theta = t10 - 0.105 * T;
```

Jeśli `theta` wychodzi ujemne albo nielogiczne, sprawdź:

- czy dobrze znaleziono `tStep`,
- czy `t10` i `t90` są po skoku,
- czy `u` i `y` nie zostały zamienione miejscami,
- czy wybrany model na pewno pasuje do obiektu.

## 8. Zbudowanie transmitancji w MATLAB-ie

Najprostszy zapis obiektu bez jawnego opóźnienia:

```matlab
s = tf('s');
G0 = K / (T*s + 1);
```

Jeśli trzeba uwzględnić opóźnienie, można użyć przybliżenia Padego. W transkrypcji pojawia się przybliżenie rzędu 12:

```matlab
rzad = 12;
[numDelay, denDelay] = pade(theta, rzad);
Gdelay = tf(numDelay, denDelay);

G = G0 * Gdelay;
```

Do sprawozdania wpisz transmitancję z konkretnymi wartościami liczbowymi:

```text
G(s) = ...
```

Nie wklejaj samego wzoru ogólnego. Prowadzący zwraca uwagę, że ma być podana transmitancja wyznaczona dla Twojego obiektu.

## 9. Porównanie modelu z obiektem

Po zbudowaniu transmitancji trzeba sprawdzić, czy model pasuje do odpowiedzi z Simulinka.

Przykładowo:

```matlab
tRel = t - t(1);
uRel = u - u0;

yModelRel = lsim(G, uRel, tRel);
yModel = yModelRel + y0;

figure;
plot(t, y, 'b');
hold on;
plot(t, yModel, 'r--');
grid on;
legend('obiekt z Simulinka', 'model zidentyfikowany');
xlabel('t');
ylabel('y');
title('Porównanie odpowiedzi obiektu i modelu');
```

Jeżeli wykresy mocno się rozjeżdżają:

- sprawdź, czy wybrano właściwy typ obiektu,
- sprawdź kolejność sygnałów,
- sprawdź `K`, `T`, `theta`,
- upewnij się, że punkty 10% i 90% są odczytane z właściwego fragmentu,
- uruchamiaj skrypt etapami, a nie dopiero po napisaniu całości.

## 10. Uzupełnienie modelu i regulatora

Po identyfikacji trzeba przejść do części z regulatorem.

1. W materiałach pomocniczych znajdź wzory na nastawy regulatora.
2. Podstaw swoje wartości `K`, `T` i `theta`/`tau`.
3. Oblicz nastawy, np. parametry typu:

```matlab
Kp = ...;
Ti = ...;
Ki = ...;
```

4. Pilnuj nawiasów w MATLAB-ie. Z transkrypcji wynika, że błędy w nawiasach często psują wyniki bez oczywistego komunikatu.
5. Wpisz wyliczone nastawy do odpowiedniego bloku regulatora w Simulinku.
6. Uruchom model ponownie.
7. Sprawdź, czy regulowana wielkość zachowuje się sensownie.

Ważne: sam zrzut ekranu regulatora nie wystarczy. Model musi być uzupełniony wartościami i powinien działać.

## 11. Wariant z zakłóceniem / na wyższą ocenę

W końcowej części nagrania prowadzący pokazuje wariant z zakłóceniem.

Ogólna procedura:

1. Skopiuj albo rozbuduj dotychczasowy model.
2. Dodaj sumator w odpowiednim miejscu układu.
3. Dodaj blok wymuszenia/zakłócenia, np. `Step`.
4. Ustaw czas zadziałania zakłócenia tak, aby nie występowało dokładnie w tym samym momencie co główny skok.
5. Ustaw amplitudę zgodnie z dokumentacją albo przykładem z materiałów.
6. Uruchom symulację.
7. Pokaż na wykresie, jak układ reaguje na zakłócenie.
8. We wnioskach napisz, czy regulator tłumi zakłócenie i czy układ wraca do wartości zadanej.

Pamiętaj: regulujesz wielkość obserwowaną, np. wysokość wody, a nie przypadkowy sygnał pomocniczy.

## 12. Co wkleić do szablonu zaliczenia

W szablonie uzupełnij kolejno:

1. Dane zadania:
   - numer indeksu,
   - wariant,
   - użyty model,
   - najważniejsze parametry wejściowe.
2. Krótki opis uruchomionego modelu Simulinka.
3. Wykres wejścia i wyjścia z pierwszej symulacji.
4. Informację, jaki fragment odpowiedzi wybrano do identyfikacji.
5. Odczytane wartości:
   - `u0`, `u1`,
   - `y0`, `y1`,
   - `tStep`,
   - `t10`,
   - `t90`.
6. Obliczenia:
   - `K`,
   - `T`,
   - `theta`/`tau`.
7. Wyznaczoną transmitancję liczbową.
8. Wykres porównujący obiekt z modelem.
9. Nastawy regulatora.
10. Wykres działania układu z regulatorem.
11. Jeśli robisz wariant rozszerzony: wykres i opis reakcji na zakłócenie.
12. Krótkie wnioski.

## 13. Minimalna kolejność pracy

Jeżeli chcesz pracować możliwie bez chaosu, trzymaj się tej kolejności:

1. Otwórz model.
2. Wpisz dane z zadania.
3. Uruchom symulację.
4. Sprawdź wykresy.
5. Wyciągnij `t`, `u`, `y` do MATLAB-a.
6. Znajdź skok wejścia.
7. Odczytaj wartości początkowe i końcowe.
8. Oblicz `K`.
9. Znajdź punkty 10% i 90%.
10. Oblicz `T` i opóźnienie.
11. Zbuduj transmitancję.
12. Porównaj model z obiektem.
13. Oblicz nastawy regulatora.
14. Wpisz nastawy do Simulinka.
15. Uruchom model z regulatorem.
16. Uzupełnij szablon zaliczenia.

## 14. Najczęstsze błędy

- Praca w złym folderze albo przeniesienie tylko części plików.
- Otwieranie modelu bez ustawienia katalogu roboczego w MATLAB-ie.
- Zamiana sygnału wejściowego z wyjściowym.
- Liczenie `K` z punktów, w których wejście się nie zmieniło, co daje dzielenie przez zero.
- Użycie punktów 10% i 90% sprzed skoku albo z nieustalonego fragmentu.
- Brak sprawdzania wykresów po każdym większym kroku.
- Pisanie całego skryptu naraz i dopiero potem szukanie błędów.
- Brak nawiasów w obliczeniach nastaw regulatora.
- Wklejenie do sprawozdania ogólnego wzoru zamiast swojej transmitancji liczbowej.
- Zrzut ekranu nieuzupełnionego modelu.
- Brak podpisów osi, legend i krótkiego komentarza do wykresów.

## 15. Szybka kontrola przed oddaniem

Przed wysłaniem/oddaniem sprawdź:

- [ ] Czy wszystkie pliki były uruchamiane z jednego folderu?
- [ ] Czy model Simulinka działa bez błędów?
- [ ] Czy wykres wejścia pokazuje skok?
- [ ] Czy wykres wyjścia pokazuje odpowiedź na skok?
- [ ] Czy `K`, `T` i `theta` mają sensowne wartości?
- [ ] Czy transmitancja jest wpisana liczbowo?
- [ ] Czy porównanie modelu z obiektem jest pokazane na wykresie?
- [ ] Czy regulator ma wpisane wyliczone nastawy?
- [ ] Czy w szablonie są wykresy, obliczenia i wnioski?
- [ ] Czy nie ma wyników typu `Inf`, `NaN` albo pustych wykresów?

