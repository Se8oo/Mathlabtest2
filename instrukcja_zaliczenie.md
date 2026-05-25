# Instrukcja wykonania zadania na zaliczenie - kaskada dwóch zbiorników

Instrukcja jest przygotowana na podstawie:

- `transkrypcja_i_opis.md` - transkrypcja i opis nagrania,
- `kaskada2_instrukcja.pdf` - treść zadania i specyfikacja obiektu,
- `Materiały pomocnicze.pdf` - metoda tabelaryczna i wzory na nastawy,
- `Kaskada2.mdl` - model obiektu w Simulinku,
- `matlab.odt` - przykładowy kod MATLAB do identyfikacji,
- `Automatyka - szablon - zaliczenie.docx` - szablon sprawozdania.

Celem jest zaprojektowanie układu regulacji stałowartościowej dla kaskady dwóch zbiorników, zidentyfikowanie modelu transmitancyjnego obiektu na podstawie odpowiedzi skokowej oraz dobranie nastaw regulatora metodą tabelaryczną.

## 1. Co dokładnie jest w zadaniu

Z `kaskada2_instrukcja.pdf` wynika, że trzeba:

1. Zaprojektować układ regulacji stałowartościowej poziomu cieczy w zbiorniku.
2. Zastosować regulator typu PID albo odpowiednią odmianę PID wynikającą z metody tabelarycznej.
3. Dobrać parametry regulatora na podstawie modelu obiektu.
4. Wyznaczyć parametry modelu transmitancyjnego z 2 punktów pomiarowych.
5. Wszystkie obliczenia wykonać w MATLAB-ie.
6. Przygotować czytelny dokument końcowy według szablonu i oddać go jako PDF.

Dane ze specyfikacji:

```text
q1 = 0.5 m^3/s
s2 = 0.05 m^2
h2 = 5.1 m
cykl pracy układu pomiarowo-sterującego = 1 s
```

Znaczenie sygnałów:

- `q1` - dopływ cieczy do pierwszego zbiornika; jest to sygnał sterujący regulatora.
- `s2` - otwarcie zaworu wyjściowego; regulator nie ma wpływu na ten sygnał, więc można go traktować jako zakłócenie/wejście nieregulowane.
- `h2` - poziom cieczy w dolnym zbiorniku, czyli wielkość regulowana.
- `y` - pomiar wysokości cieczy w zbiorniku dolnym.
- `indeks` - dodatkowe wejście modelu, do którego trzeba wpisać swój numer indeksu.

Zakresy z instrukcji:

- sygnał sterujący regulatora `0..1` odpowiada przepływowi `q1` w zakresie `0..1 m^3/s`,
- sygnał pomiarowy `y` w zakresie `0..10 V` odpowiada poziomowi cieczy,
- sygnał `s2` w zakresie `0..1` odpowiada otwarciu zaworu wyjściowego.

## 2. Przygotowanie katalogu w MATLAB-ie

1. Sklonuj repozytorium albo pobierz wszystkie pliki.
2. Uruchom MATLAB.
3. Ustaw katalog repozytorium jako bieżący folder roboczy MATLAB-a.
4. W jednym folderze powinny znajdować się przynajmniej:

```text
Kaskada2.mdl
kaskada2_instrukcja.pdf
Materiały pomocnicze.pdf
matlab.odt
Automatyka - szablon - zaliczenie.docx
```

Nie przenoś samego modelu bez reszty materiałów. W nagraniu prowadzący podkreślał, że praca w jednym folderze ogranicza problemy ze ścieżkami.

## 3. Uruchomienie modelu Simulinka

1. W MATLAB-ie otwórz Simulink.
2. Wybierz `Open File` i otwórz:

```text
Kaskada2.mdl
```

3. Model nazywa się wewnętrznie `Kaskada2_2013b`.
4. Główny blok obiektu to:

```text
Kaskada zbiorników
```

5. Blok ma wejścia:

```text
q1
s2
indeks
```

oraz wyjście:

```text
y
```

6. Blok `Kaskada zbiorników` ma ustawione `Permissions: NoReadOrWrite`, więc nie należy próbować go rozbijać ani edytować w środku. Traktuj go jako czarną skrzynkę.
7. Do wejścia `indeks` wpisz swój numer indeksu.
8. Dla punktu pracy ustaw:

```text
q1 = 0.5
s2 = 0.05
```

9. Uruchom symulację i sprawdź, czy odpowiedź na wyjściu `y` stabilizuje się w okolicy punktu pracy.

W pliku `.mdl` widać, że model zapisuje wyniki do zmiennej `out`, a czas jest zapisany jako `tout`. Dane ze scope'a są używane w przykładzie jako `out.ScopeData`.

## 4. Eksperyment do identyfikacji obiektu

Szablon zaliczenia wymaga identyfikacji dla:

```text
10% ujemnego wymuszenia skokowego sygnału sterującego zadanego w punkcie pracy układu
```

Praktycznie oznacza to:

1. Najpierw doprowadzasz układ do punktu pracy:

```text
q1 = 0.5
s2 = 0.05
```

2. Po ustaleniu poziomu wykonujesz skok sterowania `q1` o `-10%` względem punktu pracy:

```text
q1_po_skoku = 0.5 * 0.9 = 0.45
```

3. W przykładowym kodzie z `matlab.odt` prowadzący przyjmuje moment skoku/wycięcia danych około:

```matlab
1500
```

czyli analizowany fragment zaczyna się od okolic `t = 1500 s`.

4. Rejestrujesz dwa sygnały:

- wejście/wymuszenie `u`, czyli sygnał sterujący,
- wyjście `y`, czyli odpowiedź poziomu cieczy.

## 5. Kod bazowy z pliku `matlab.odt`

W repozytorium jest plik `matlab.odt` z kodem użytym podczas zajęć. Najważniejsza część wygląda tak:

```matlab
te=out.ScopeData.time;
ue=out.ScopeData.signals(1).values;
ye=out.ScopeData.signals(2).values;

n=max(find(te<=1500));
t=te(n:end)-te(n);
u=ue(n:end)-ue(n-1);
y=ye(n:end)-ye(n);

uu=u(end);
yu=y(end);

n10=max(find(y<=yu*0.1));
t10=t(n10);
y10=y(n10);

n90=max(find(y<=yu*0.9));
t90=t(n90);
y90=y(n90);

k=yu/uu;
T=(t90-t10)/2.2;
tau=t10-0.1*T;

[Lp Mp] = pade(tau,12);

L=k;
M=[T 1];

L=conv(L,Lp);
M=conv(M,Mp);

ymodel=lsim(L,M,u,t);
plot(t,y,t,ymodel);
plot(t,y-ymodel);

kp=(0.34*T)/(k*tau);
Ti=T;
ki=kp/Ti;
```

Ten kod jest dobrym szkieletem, ale podczas zaliczenia nie przepisuj go bezmyślnie. Sprawdź kolejność sygnałów i upewnij się, że dane rzeczywiście są w `out.ScopeData.signals(1)` oraz `out.ScopeData.signals(2)`.

## 6. Import danych z Simulinka

Po symulacji sprawdź w Workspace, czy istnieje zmienna:

```matlab
out
```

Następnie pobierz dane:

```matlab
te = out.ScopeData.time;
ue = out.ScopeData.signals(1).values;
ye = out.ScopeData.signals(2).values;
```

Zgodnie z szablonem:

- sygnał nr 1 powinien być sygnałem wejściowym/wymuszeniem,
- sygnał nr 2 powinien być sygnałem wyjściowym.

Zawsze zrób kontrolny wykres:

```matlab
figure;
subplot(2,1,1);
plot(te, ue);
grid on;
title('Wejście / wymuszenie');
xlabel('t [s]');
ylabel('u');

subplot(2,1,2);
plot(te, ye);
grid on;
title('Wyjście obiektu');
xlabel('t [s]');
ylabel('y');
```

Jeśli wykresy są zamienione, popraw indeksy `signals(1)` i `signals(2)`.

## 7. Wycięcie fragmentu po skoku

Przykład z materiałów przyjmuje analizę od `t = 1500 s`:

```matlab
n = max(find(te <= 1500));
t = te(n:end) - te(n);
u = ue(n:end) - ue(n-1);
y = ye(n:end) - ye(n);
```

Znaczenie:

- `t` - czas przesunięty tak, aby początek analizowanego fragmentu był w `0`,
- `u` - zmiana wejścia względem wartości sprzed skoku,
- `y` - zmiana wyjścia względem wartości w chwili rozpoczęcia analizy.

Dla skoku ujemnego wartości `u` i `y` mogą być ujemne. To jest normalne. Ważne, żeby konsekwentnie liczyć zmiany względem punktu pracy.

## 8. Odczyt wartości końcowych

Po wycięciu fragmentu odczytaj końcowe wartości zmian:

```matlab
uu = u(end);
yu = y(end);
```

`uu` to całkowita zmiana wejścia, a `yu` to całkowita zmiana wyjścia.

Wzmocnienie obiektu:

```matlab
k = yu / uu;
```

Sprawdź:

- `uu` nie może być równe `0`,
- jeśli dostajesz `Inf`, to najpewniej dzielisz przez zero,
- jeśli dostajesz `NaN`, sprawdź czy sygnały nie są puste albo czy indeks `n` został znaleziony.

## 9. Punkty 10% i 90%

Dla metody z dwóch punktów pomiarowych wyznaczasz momenty, w których odpowiedź osiąga 10% i 90% końcowej zmiany.

W kodzie z materiałów:

```matlab
n10=max(find(y<=yu*0.1));
t10=t(n10);
y10=y(n10);

n90=max(find(y<=yu*0.9));
t90=t(n90);
y90=y(n90);
```

Ten zapis pasuje do odpowiedzi ujemnej, gdy `yu` jest ujemne. Jeżeli odpowiedź jest dodatnia, warunek zwykle trzeba zmienić na `>=`:

```matlab
n10 = max(find(y >= yu*0.1));
n90 = max(find(y >= yu*0.9));
```

Najbezpieczniej sprawdź punkty na wykresie:

```matlab
figure;
plot(t, y);
hold on;
plot(t10, y10, 'r*');
plot(t90, y90, 'g*');
grid on;
legend('odpowiedź', '10%', '90%');
title('Punkty 10% i 90% odpowiedzi');
xlabel('t [s]');
ylabel('y');
```

Do szablonu wklej wykres z zaznaczonymi punktami albo wykres, na podstawie którego jasno widać odczyt.

## 10. Identyfikacja modelu transmitancyjnego

Dla kaskady dwóch zbiorników odpowiedź w ćwiczeniu jest traktowana jako inercja z opóźnieniem. Przyjmowana postać modelu:

```text
           k
G(s) = ---------- * e^(-tau*s)
       T*s + 1
```

Parametry:

```matlab
k   = yu / uu;
T   = (t90 - t10) / 2.2;
tau = t10 - 0.1*T;
```

W transkrypcji pojawia się wariant `t10 - 0.105*T`, ale w pliku `matlab.odt` użyto `t10 - 0.1*T`. Na zaliczeniu trzymaj się wzoru z materiału/kodu prowadzącego, chyba że prowadzący poda inną wersję.

## 11. Opóźnienie przez przybliżenie Padego

Żeby użyć opóźnienia w transmitancji MATLAB-a, w przykładzie zastosowano przybliżenie Padego rzędu 12:

```matlab
[Lp, Mp] = pade(tau, 12);
```

Najpierw tworzysz inercję:

```matlab
L = k;
M = [T 1];
```

Potem dokładasz opóźnienie:

```matlab
L = conv(L, Lp);
M = conv(M, Mp);
```

Otrzymany model to:

```matlab
G = tf(L, M);
```

Do sprawozdania wpisz swoją liczbową transmitancję, np. po wykonaniu:

```matlab
G
```

Nie wpisuj samego wzoru ogólnego bez wartości liczbowych.

## 12. Porównanie modelu z obiektem

Sprawdź, czy odpowiedź modelu zgadza się z odpowiedzią obiektu:

```matlab
ymodel = lsim(L, M, u, t);

figure;
plot(t, y, 'b', t, ymodel, 'r--');
grid on;
legend('obiekt z Simulinka', 'model zidentyfikowany');
title('Porównanie odpowiedzi obiektu i modelu');
xlabel('t [s]');
ylabel('y');
```

Dodatkowo warto sprawdzić błąd:

```matlab
figure;
plot(t, y - ymodel);
grid on;
title('Błąd modelu');
xlabel('t [s]');
ylabel('y - ymodel');
```

Jeżeli model mocno nie pasuje:

- sprawdź, czy wycięto właściwy fragment od `1500 s`,
- sprawdź, czy wejście i wyjście nie są zamienione,
- sprawdź znaki `u` i `y`,
- sprawdź punkty 10% i 90%,
- sprawdź, czy `tau` nie wyszło ujemne,
- uruchamiaj skrypt etapami, a nie cały naraz.

## 13. Dobór regulatora z materiałów pomocniczych

W `Materiały pomocnicze.pdf` dla obiektu typu inercja z opóźnieniem podany jest regulator tabelaryczny. Kod z `matlab.odt` używa nastaw:

```matlab
kp = (0.34*T)/(k*tau);
Ti = T;
ki = kp/Ti;
```

Czyli:

- `kp` - wzmocnienie regulatora,
- `Ti` - czas całkowania,
- `ki` - wzmocnienie członu całkującego.

Jest to praktycznie regulator PI jako odmiana regulatora PID, gdzie człon różniczkujący można zostawić nieaktywny, jeśli tabela dla danego modelu go nie wymaga.

Jeżeli w Simulinku używasz bloku PID, wpisz parametry zgodnie z wybraną postacią bloku:

- jeśli blok przyjmuje `P`, `I`, `D`, wpisz:

```text
P = kp
I = ki
D = 0
```

- jeśli blok przyjmuje `Kp`, `Ti`, `Td`, wpisz:

```text
Kp = kp
Ti = T
Td = 0
```

Zawsze zrób zrzut ekranu okna parametrów regulatora, bo szablon tego wymaga.

## 14. Eksperyment z regulatorem

Szablon wymaga modelu z regulatorem PID i dostarczonym obiektem. Trzeba pokazać:

1. Doprowadzenie układu do punktu pracy.
2. Skokowe zmniejszenie wartości zadanej o 10% względem punktu pracy.
3. Wprowadzenie skokowej zmiany zakłócenia na wejściu drugim, czyli na `s2`.

Praktyczny układ:

1. Porównaj wartość zadaną poziomu z pomiarem `y`.
2. Błąd podaj na regulator.
3. Wyjście regulatora podaj na wejście `q1` obiektu.
4. Wejście `s2` ustaw na wartość nominalną `0.05`, a potem dodaj skok zakłócenia.
5. Do wejścia `indeks` wpisz swój numer indeksu.
6. Obserwuj wyjście `y` oraz sygnał sterujący.

Zakłócenie na `s2` powinno zadziałać w innym momencie niż skok wartości zadanej, żeby na wykresie było widać osobno wpływ zadania i wpływ zakłócenia.

## 15. Co dokładnie wkleić do szablonu `.docx`

Szablon `Automatyka - szablon - zaliczenie.docx` zawiera następujące pola/sekcje. Uzupełnij je po kolei.

### 15.1 Dane osobowe

- imię i nazwisko,
- numer indeksu,
- data/godzina, jeśli wymagana.

### 15.2 Identyfikacja obiektu

Wklej:

1. Zrzut ekranu modelu w Simulinku - część identyfikacyjna.
2. Wykres odpowiedzi układu na wymuszenie:
   - układ `1x2`,
   - wejście nr 1: sygnał wejściowy/wymuszenie,
   - wejście nr 2: sygnał wyjściowy.
3. Krótki opis odpowiedzi obiektu:
   - jaki typ obiektu przyjmujesz,
   - dlaczego, np. odpowiedź wygląda jak inercja z opóźnieniem.
4. Kod MATLAB użyty do identyfikacji.
5. Równanie/transmitancję obiektu `G(s)` z wartościami liczbowymi.
6. Wykres porównania odpowiedzi zarejestrowanej i modelu.

### 15.3 Regulator

Wklej:

1. Wzór przyjętego regulatora z metody tabelarycznej.
2. Wyliczone nastawy:

```text
kp = ...
Ti = ...
ki = ...
```

albo parametry w takiej postaci, jakiej wymaga blok regulatora.

3. Zrzut ekranu modelu w Simulinku z regulatorem.
4. Zrzut ekranu okna parametrów regulatora.
5. Wykres eksperymentu z regulatorem.
6. Krótkie wnioski.

### 15.4 Eksperyment końcowy

Na końcowym wykresie powinno być widać:

- dojście do punktu pracy,
- skok wartości zadanej o `-10%`,
- reakcję na zakłócenie na `s2`,
- powrót/stabilizację poziomu `h2` lub sygnału `y`.

## 16. Minimalna kolejność pracy

1. Otwórz `Kaskada2.mdl`.
2. Wpisz swój indeks.
3. Ustaw punkt pracy: `q1=0.5`, `s2=0.05`.
4. Zrób eksperyment identyfikacyjny: skok `q1` o `-10%` po ustaleniu obiektu.
5. Uruchom symulację.
6. Pobierz `te`, `ue`, `ye` z `out.ScopeData`.
7. Wytnij fragment od `t=1500 s` albo od faktycznego momentu skoku.
8. Oblicz `uu`, `yu`, `k`.
9. Znajdź punkty 10% i 90%.
10. Oblicz `T` i `tau`.
11. Zbuduj model z opóźnieniem przez Padego.
12. Porównaj model z odpowiedzią obiektu.
13. Oblicz `kp`, `Ti`, `ki`.
14. Zbuduj układ z regulatorem.
15. Dodaj skok wartości zadanej i zakłócenie na `s2`.
16. Zrób wykresy i zrzuty ekranu.
17. Uzupełnij szablon `.docx`.
18. Wyeksportuj gotowy dokument do PDF.

## 17. Najczęstsze błędy

- Praca w innym folderze niż folder z modelem i materiałami.
- Brak wpisanego indeksu do modelu.
- Mylenie `q1` z `s2`: `q1` jest sterowaniem, `s2` jest wejściem nieregulowanym/zakłóceniem.
- Zamiana sygnału wejściowego i wyjściowego w `out.ScopeData.signals`.
- Liczenie z całego przebiegu zamiast z fragmentu po skoku.
- Złe warunki dla punktów 10% i 90% przy odpowiedzi ujemnej.
- Dzielenie przez zero przy obliczaniu `k`.
- Ujemne albo nielogiczne `tau`.
- Wklejenie do sprawozdania wzoru ogólnego zamiast liczbowej transmitancji.
- Brak porównania odpowiedzi obiektu i modelu.
- Brak zrzutu parametrów regulatora.
- Brak wniosków do wykresu końcowego.

## 18. Checklista przed oddaniem

- [ ] W szablonie jest imię, nazwisko i indeks.
- [ ] Jest zrzut modelu do identyfikacji.
- [ ] Jest wykres wejścia i wyjścia dla skoku `-10%`.
- [ ] Jest opis typu obiektu.
- [ ] Jest kod MATLAB identyfikacji.
- [ ] Są wartości `k`, `T`, `tau`.
- [ ] Jest transmitancja `G(s)` z wartościami liczbowymi.
- [ ] Jest wykres porównania modelu z obiektem.
- [ ] Są wyliczone nastawy regulatora.
- [ ] Jest zrzut modelu z regulatorem.
- [ ] Jest zrzut parametrów regulatora.
- [ ] Jest wykres eksperymentu z regulatorem i zakłóceniem.
- [ ] Są krótkie wnioski.
- [ ] Dokument został wyeksportowany do PDF.
