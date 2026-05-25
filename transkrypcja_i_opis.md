# Transkrypcja i opis nagrania

Źródło: `G.7z.001`-`G.7z.004` po rozpakowaniu zawiera plik audio `G.m4a`.

Uwaga: transkrypcja została wykonana automatycznie, dlatego w miejscach z gorszą jakością dźwięku, rozmowami w tle albo nazwami zmiennych mogą występować błędy rozpoznawania.

## O co chodzi w nagraniu

Nagranie jest instruktażem do zaliczenia/laboratorium z MATLAB-a i Simulinka. Prowadzący pokazuje krok po kroku, jak pracować z paczką materiałów, uruchomić model, zebrać dane z symulacji, zidentyfikować parametry obiektu oraz przygotować elementy potrzebne do zaliczenia i sprawozdania.

Najważniejszy temat to identyfikacja obiektu inercyjnego, prawdopodobnie układu z kaskadą zbiorników i regulacją poziomu wody. Omawiane są sygnały wejścia i wyjścia, skok wymuszenia, czas stabilizacji, eksport danych z Simulinka do MATLAB-a, wyznaczanie parametrów transmitancji oraz późniejsze wykorzystanie tych parametrów w modelu i nastawach regulatora.

## Najistotniejsze rzeczy

- Należy wypakować całą paczkę i pracować w jednym folderze, bo MATLAB/Simulink może mieć problemy ze ścieżkami do plików.
- W paczce są materiały pomocnicze, szablon/sprawozdanie i model do uruchomienia.
- Model najlepiej otwierać przez Simulink (`Open File`) i nie mieszać niepotrzebnie w zablokowanych blokach.
- W zadaniu trzeba wpisać odpowiednie dane, m.in. indeks lub wartości zależne od indeksu, bo od tego mogą zależeć parametry obiektu.
- Trzeba uruchomić symulację, sprawdzić wykresy i wyeksportować sygnały z `out`, np. przez ścieżki typu `out.scopeData.signals(...).values`.
- Kluczowa jest identyfikacja obiektu po odpowiedzi na skok: trzeba dobrać właściwy fragment po skoku i ocenić, czy obiekt wygląda jak inercja, inercja z opóźnieniem albo bardziej złożony przypadek.
- Parametry do wyznaczenia to przede wszystkim wzmocnienie `K`, stała czasowa `T` oraz opóźnienie `tau`/`T0`, wyznaczane z wykresu i punktów charakterystycznych, m.in. okolic 10% i 90% odpowiedzi.
- Skrypt warto uruchamiać etapami i regularnie sprawdzać wyniki, bo nie każdy błąd musi dać czerwony komunikat; czasem pojawiają się po prostu nielogiczne wykresy albo wartości typu `Inf` wynikające np. z dzielenia przez zero.
- Do zaliczenia/sprawozdania potrzebne są sensowne wykresy, opis matematyczny/transmitancja modelu, parametry i uzupełniony model, a nie tylko sam zrzut ekranu.
- Na wyższą ocenę pojawia się dodatkowy wariant z zakłóceniem/zmianą w modelu, np. przez dodanie bloku/sumatora i sprawdzenie odpowiedzi układu na zakłócenie.
- Prowadzący podkreśla, żeby nie uczyć się pojedynczego skryptu na pamięć, tylko rozumieć procedurę, bo na zaliczeniu obiekt lub parametry mogą być inne.

## Najważniejsze kroki techniczne

1. Wypakować materiały i trzymać pliki w jednym katalogu roboczym.
2. Otworzyć model w Simulinku i sprawdzić, czy wszystkie bloki oraz ścieżki działają.
3. Wpisać wymagane wartości/indeks i uruchomić symulację.
4. Obejrzeć wykres wejścia i wyjścia oraz upewnić się, że skok i odpowiedź są widoczne.
5. Zaimportować dane z symulacji do MATLAB-a.
6. Wybrać fragment odpowiedzi po skoku i odczytać próbki/czasy potrzebne do identyfikacji.
7. Obliczyć parametry modelu (`K`, `T`, opóźnienie) zgodnie z materiałami pomocniczymi.
8. Zbudować/zapisać transmitancję i porównać odpowiedź modelu z odpowiedzią obiektu.
9. Uzupełnić model regulatora oraz nastawy i ponownie sprawdzić wykresy.
10. Dla trudniejszego wariantu dodać zakłócenie i opisać jego wpływ na układ.

## Metadane transkrypcji

```text
language=pl probability=1 duration=5104.4693125
```

## Pełna transkrypcja

```text
[00:00:00 - 00:00:02] Późdź, jakoś czerwnają się a ja.
[00:00:02 - 00:00:12] Eee, wszyscy wiedzą, że tutaj byłeś w sambie wszystko.
[00:00:12 - 00:00:16] Okej.
[00:00:16 - 00:00:21] Eee, dlatego nie będę rozmowywał, ale będę przyszłym jeden.
[00:00:21 - 00:00:25] Dobra, czyli za dwa tygodnie, czy stół.
[00:00:25 - 00:00:29] U nim w koncie matlawa.
[00:00:29 - 00:00:33] I my będziemy kontynuować tak, jak ten pokazywał.
[00:00:33 - 00:00:37] Chcę wam pokazać to jeden do jeden, jak to mamy podrobione.
[00:00:37 - 00:00:42] Ale jeżeli wam to zrobiło, to proszę, żebyście ze mną pracowali.
[00:00:42 - 00:00:47] Czyli by pracowali po prostu tak samo.
[00:00:47 - 00:00:53] Oczywiście, jak i co cię z tym piszecie, to już ja nie mam najmieszczego problemu.
[00:00:53 - 00:00:55] To ma działo.
[00:00:55 - 00:00:59] Ja mam pokazuję jedno dwego, z wielu z tych, co przeszedłem na laboratorium.
[00:00:59 - 00:01:01] Ale jeżeli chcecie coś zmienić.
[00:01:01 - 00:01:02] Nie.
[00:01:03 - 00:01:08] Było za akurat policja, żeby nie musiały zapisać rodzinie na dwie.
[00:01:08 - 00:01:11] A może nie wiedziałem, co się zmieni.
[00:01:29 - 00:01:30] Tutaj.
[00:01:31 - 00:01:40] Na mojej wzgódce jest przypadowe zaliczenie do pogrania.
[00:01:40 - 00:01:43] I jest z IP.
[00:01:43 - 00:01:46] Kiedyś w środku pogracie, ja sobie do jednego podderzę.
[00:01:46 - 00:01:48] Jak i to jest dwie sza.
[00:01:48 - 00:01:49] Opiniemy polada.
[00:01:49 - 00:01:52] Z mojej strony pracujcie w jednym podderze.
[00:01:52 - 00:01:55] Jak się wypakujecie, piszecie w tym podderze.
[00:01:55 - 00:01:57] Ludzie sobie wypakowaliście.
[00:01:57 - 00:01:58] Dlaczego?
[00:01:58 - 00:02:01] Matlab lubi jeszcze w tym podderze.
[00:02:01 - 00:02:04] Miedliście mieli, by za ułatwę pobrany.
[00:02:04 - 00:02:05] Pojedziecie.
[00:02:05 - 00:02:08] A w drugiej strony z grudnia przeszedzienia pochwycie.
[00:02:08 - 00:02:11] To będzie ciągawa przeżycia w monii do zmiany podderzy.
[00:02:11 - 00:02:13] Także pracujcie w jednym podderze, w jakim nie macie.
[00:02:13 - 00:02:14] Może.
[00:02:14 - 00:02:16] I unikniecie niepotrzebnie.
[00:02:16 - 00:02:17] Trójmi roczarowanie.
[00:02:17 - 00:02:19] Ale to powinien działać.
[00:02:22 - 00:02:24] Tutaj jest dokumentacja.
[00:02:24 - 00:02:25] To jest szaunek.
[00:02:25 - 00:02:27] Może sobie go pomóc.
[00:02:28 - 00:02:35] Ja chodź poprowadnę dzisiaj trochę kuśroku.
[00:02:35 - 00:02:37] Tutaj mamy wszystkie zadania.
[00:02:37 - 00:02:39] Nie znali bardzo jakichś ułatwia.
[00:02:39 - 00:02:40] Chciałbym.
[00:02:43 - 00:02:47] Czekaj do mnie.
[00:02:47 - 00:02:48] Czekaj.
[00:03:03 - 00:03:05] Udało wam się poszukiwać?
[00:03:05 - 00:03:06] Nie działa.
[00:03:07 - 00:03:09] Nie działa.
[00:03:14 - 00:03:26] No bo jest, że oni nie ma,
[00:03:26 - 00:03:28] ale będę się wspierał w tym.
[00:03:28 - 00:03:29] To dotaknie ci też paczka odderzy.
[00:03:29 - 00:03:31] No bo nie chcieliśmy się szukać.
[00:03:31 - 00:03:32] Tego jak była widać,
[00:03:32 - 00:03:34] jak gdyby się taka jednoznacznie materiały
[00:03:34 - 00:03:37] poprosić, że ja się wyływałem.
[00:03:40 - 00:03:42] Będę się do niego wyływał.
[00:03:42 - 00:03:43] Tak chwilę tutaj.
[00:03:43 - 00:03:45] Zastaniecie je w paczce.
[00:03:45 - 00:03:47] Podsumowując, co dostajecie.
[00:03:54 - 00:03:56] Jest szablon do uzygonienia.
[00:03:56 - 00:03:58] Jest modele, które uruchomienia.
[00:03:58 - 00:03:59] Jest.
[00:04:03 - 00:04:05] Ten komplecik jest już pasto,
[00:04:05 - 00:04:07] pobieracie i zaczynacie zaliczenie.
[00:04:07 - 00:04:09] Tutaj zawsze tak samo to wygląda.
[00:04:09 - 00:04:11] Modele jest różny.
[00:04:11 - 00:04:13] Ale jak wspominałem wam,
[00:04:13 - 00:04:15] będzie albo to inercja,
[00:04:15 - 00:04:17] albo to inercja.
[00:04:23 - 00:04:24] I teraz tak.
[00:04:24 - 00:04:25] Jak chcecie uruchomić,
[00:04:25 - 00:04:26] jak wypróci na linucie,
[00:04:26 - 00:04:28] to nie tyle macie kłopot,
[00:04:28 - 00:04:29] co lepiej, jak widzicie,
[00:04:29 - 00:04:30] do MDL uruchomienia
[00:04:30 - 00:04:32] bez posiadania singulinka.
[00:04:32 - 00:04:34] Czyli wchodzimy sobie
[00:04:34 - 00:04:36] uruchomienie singulinka samodzielnie,
[00:04:36 - 00:04:38] a później wybieramy open file,
[00:04:38 - 00:04:40] wybieramy ten modele.
[00:04:40 - 00:04:41] Nie wiem, gdyby się zakrywa,
[00:04:41 - 00:04:43] lub do realizacji.
[00:04:44 - 00:04:49] Lidka skada dwa.
[00:04:58 - 00:04:59] Tutajcie uwagę, żeby dźwięk
[00:04:59 - 00:05:01] wcześniej wyplakować,
[00:05:01 - 00:05:02] bo dostali czerwone dźwięko,
[00:05:02 - 00:05:04] żeby było szybkie do wybrania.
[00:05:04 - 00:05:05] A to sami jest taki powód,
[00:05:05 - 00:05:07] że nie wiem, jak to jest.
[00:05:07 - 00:05:09] Przecież po prostu
[00:05:09 - 00:05:11] singulinko jest otwierany z dźwięk
[00:05:11 - 00:05:13] i jest to nie co zadziała.
[00:05:14 - 00:05:16] Jak to jest?
[00:05:16 - 00:05:18] To jest singulinko, tak?
[00:05:24 - 00:05:26] Zobaczcie mnie w czasie,
[00:05:26 - 00:05:28] pokazuję wam tutaj macie blocze.
[00:05:28 - 00:05:30] Ten bloczek jest wielka.
[00:05:33 - 00:05:35] W środku tego bloczka
[00:05:35 - 00:05:37] jest trochę remerzy.
[00:05:37 - 00:05:39] On jest zablokowany.
[00:05:39 - 00:05:40] Nie ma skierzowej wiedzą,
[00:05:40 - 00:05:41] można sobie zablokować,
[00:05:41 - 00:05:43] ale jest zablokowany,
[00:05:43 - 00:05:45] żebyście przetrzymali,
[00:05:45 - 00:05:47] i tam weszli,
[00:05:47 - 00:05:49] nic się nie zastosowali, jak z tego wyjść.
[00:05:49 - 00:05:51] Także on jest normalnie,
[00:05:51 - 00:05:53] jak my nie dostajemy także strzałka.
[00:05:53 - 00:05:55] Tutaj widzicie go, w ten sposób.
[00:05:55 - 00:05:57] I tak, jak opówiem, przed kolegą.
[00:05:57 - 00:05:59] Przez cały rok, weźcie?
[00:05:59 - 00:06:01] To się robi?
[00:06:01 - 00:06:03] Prawo zwalne jest tylko,
[00:06:03 - 00:06:05] żeby z powrotem,
[00:06:05 - 00:06:07] jak to pomieszczanie, jak samochód,
[00:06:07 - 00:06:09] nie ważne, to jest to śwoce.
[00:06:09 - 00:06:11] Ja pochodzę od waszych kolegów,
[00:06:11 - 00:06:13] kiedyś i teraz nawet
[00:06:13 - 00:06:17] bloczek nie patrzymy
[00:06:17 - 00:06:19] z perspektywy
[00:06:19 - 00:06:21] zadania,
[00:06:21 - 00:06:23] a dzisiaj mam kaskadę w dwóch biornikach.
[00:06:23 - 00:06:25] Dzisiaj mam kaskadę w trzech biornikach,
[00:06:25 - 00:06:27] bo ja miałem dwóch,
[00:06:27 - 00:06:29] jest problem.
[00:06:29 - 00:06:31] Proszę, podejdź do tego,
[00:06:31 - 00:06:33] jak do kombinacyjnej.
[00:06:33 - 00:06:35] Jak już macie to, weź wyjść,
[00:06:35 - 00:06:37] to macie zrobić jakiś schemat.
[00:06:37 - 00:06:39] I tutaj tym schematem, jak widzicie,
[00:06:39 - 00:06:41] się zastanawiam, a dzisiaj
[00:06:41 - 00:06:43] ujadę ciężarówką,
[00:06:43 - 00:06:45] damie zestaw czakiem.
[00:06:45 - 00:06:47] Abo odjadę zestaw czakiem,
[00:06:47 - 00:06:49] zaнюdowczo wówką.
[00:06:49 - 00:06:51] Jeśli będziecie tym stresowali, to znaczy,
[00:06:51 - 00:06:53] że nie wiedzimy się sobie jeszcze
[00:06:53 - 00:06:55] tej wiosy, patrzymy,
[00:06:55 - 00:06:57] proszę, na...
[00:06:57 - 00:06:59] tak, tak, tak, tak, tak, tak, tak,
[00:06:59 - 00:07:05] tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak, tak.
[00:07:05 - 00:07:07] Ktoś, odbana,
[00:07:40 - 00:07:46] to będzie nasze zakłócenie, bo wy zazwyczaj stanujemy jedną modą, a nie z obora.
[00:07:46 - 00:07:52] Zresztą to tak wychodzi z instrukcji i będziemy skarali się wygulować ten poziom wody w kłóce.
[00:07:52 - 00:07:56] Czyli tak przez pośrednika będziemy wygulować to.
[00:07:56 - 00:07:58] A to nie macie wpływu.
[00:07:58 - 00:08:00] I to jest właśnie prawie sądowolenia.
[00:08:00 - 00:08:04] Nie macie wpływu na wszystko w kolei i powstaje jakiś taki inercyjny.
[00:08:05 - 00:08:10] Ale tak jak wspomniałem, to od skończonego zdanie nie powinno być pierwszego znaczenia.
[00:08:10 - 00:08:12] Pan jest coś, który napisał.
[00:08:12 - 00:08:16] To pierwszego dla bada, otwrywa bota,
[00:08:16 - 00:08:18] to później otwrywa bada, otwrywiego.
[00:08:18 - 00:08:22] Znaczy, to opetnika.
[00:08:22 - 00:08:26] Nie że mamy napisane instrukcje, ale liczy się dla was to, o którym to robicie swój zówek.
[00:08:26 - 00:08:28] To jest napisana.
[00:08:28 - 00:08:30] W rzęku 1 to jest...
[00:08:32 - 00:08:34] Dodajemy strefa.
[00:08:35 - 00:08:39] Tu wpisujemy jaką walczość wieńsza w baju,
[00:08:39 - 00:08:48] w neruchu, a w fajnze w baju.
[00:08:48 - 00:08:50] I tutaj kolecza się robi na razie tam.
[00:08:50 - 00:08:52] Dlaczego na razie?
[00:08:52 - 00:08:57] Ponieważ musimy wyznaczyć jej ile czasu,
[00:08:57 - 00:09:00] kiedy szybujemy na stabilizację obiektu.
[00:09:00 - 00:09:04] Niektórzy z was już mieli okazję mieć na abalatowaniu obiektywne miejsce.
[00:09:04 - 00:09:10] Więc on się jakoś zastąpili tutaj.
[00:09:10 - 00:09:13] Nie wiemy jeszcze, ile czasu się to będzie stabilizować.
[00:09:13 - 00:09:14] Więc na razie nie lubimy skoczyć.
[00:09:14 - 00:09:16] Skoczyć lubimy, jak będziemy mieli taki projekt,
[00:09:16 - 00:09:17] żeby się dołożyć w tym obiektu.
[00:09:17 - 00:09:20] Tak, że na razie za dużo renamentów nie wprowadzamy,
[00:09:20 - 00:09:22] dostajemy tylko wartość,
[00:09:22 - 00:09:25] która dla nas ważna, bo chcemy nasz obiekt zdyfikować
[00:09:25 - 00:09:27] dla takiego pływu wody.
[00:09:27 - 00:09:28] Więc tu i tyle.
[00:09:28 - 00:09:30] Jednostki nie mają znaczenia.
[00:09:30 - 00:09:31] Do S2.
[00:09:31 - 00:09:33] Tutaj polecam do ten moment kontakt.
[00:09:33 - 00:09:36] Dlatego, że nie będziemy zmienić S2 w tym przykładzie.
[00:09:36 - 00:09:40] Te zmiana S2 dopiero zastępuje zalabią na 4 pływ.
[00:09:40 - 00:09:42] Dopiero wtedy zastępujmy się do nich,
[00:09:42 - 00:09:44] pokażę wam wtedy,
[00:09:44 - 00:09:46] zmieniamy tego hosta na stefa.
[00:09:46 - 00:09:51] Co wpisujemy tutaj?
[00:09:51 - 00:09:52] Zalabiam.
[00:09:52 - 00:09:53] Dokładnie.
[00:09:53 - 00:09:54] To jest tutaj.
[00:09:54 - 00:09:55] Czyli tych, tych, tych.
[00:09:55 - 00:09:56] Gotowe.
[00:09:56 - 00:09:57] Indeks jest to ważny.
[00:09:57 - 00:09:59] Indeks jest to, co tam napisane.
[00:09:59 - 00:10:03] I też kontakt.
[00:10:03 - 00:10:05] Wpisujecie swój indeks,
[00:10:05 - 00:10:13] albo wpisuje dzisiaj razem zalabiamy ten sam.
[00:10:13 - 00:10:15] Tak i wpisuje wszyscy.
[00:10:15 - 00:10:17] To zależy, że wszystko masz obiekt.
[00:10:17 - 00:10:19] Więc on może wszystko się zmienić.
[00:10:19 - 00:10:21] Jeżeli ten indeks jest inny,
[00:10:21 - 00:10:25] wyjście dzisiaj we samym ze mną.
[00:10:25 - 00:10:27] Będziecie mieć swoje indeksy na zaliczaniu.
[00:10:27 - 00:10:29] Dzisiaj piszczą się.
[00:10:29 - 00:10:31] A to w środku jak się też mamy zmieniać indeks
[00:10:31 - 00:10:33] na nasze takie zaliczania?
[00:10:33 - 00:10:35] Na zaliczaniu puszczącie.
[00:10:35 - 00:10:37] A tam, gdzie jest indeksy wpisane?
[00:10:37 - 00:10:38] O tu.
[00:10:38 - 00:10:39] Nie.
[00:10:39 - 00:10:40] To pod binacją...
[00:10:40 - 00:10:42] Gdzie to w ogóle nie zmienia?
[00:10:42 - 00:10:43] Nie, nie, nie.
[00:10:43 - 00:10:45] Od binacji sygnał o tej wartości.
[00:10:45 - 00:10:47] To zostało co ciekawe z zalicznanych.
[00:10:47 - 00:10:49] Nie chodziło o taką formę
[00:10:49 - 00:10:51] odpisania skwinów.
[00:10:51 - 00:10:53] Dużo skwinty pochodzą od tej osoby.
[00:10:53 - 00:10:55] Ale fajnie się sprawdza
[00:10:55 - 00:10:57] do takiej identyfikacji
[00:10:57 - 00:10:59] i zmiany
[00:10:59 - 00:11:01] o skleparamentach obiektów.
[00:11:01 - 00:11:03] Możecie mi to powiedzieć,
[00:11:03 - 00:11:05] jeżeli takie różne,
[00:11:05 - 00:11:07] nie zawsze wyczuwały się,
[00:11:07 - 00:11:09] że wasze obiekty mają,
[00:11:09 - 00:11:11] i to same wyniki
[00:11:11 - 00:11:13] od kolegi, koleżanki.
[00:11:13 - 00:11:15] W tym obiektu.
[00:11:15 - 00:11:17] O, ja nigdy nie miał oczkodzienia.
[00:11:17 - 00:11:19] Także to jest kwestia
[00:11:19 - 00:11:21] bardziej zmiany w przyszłości.
[00:11:21 - 00:11:23] Dobra.
[00:11:23 - 00:11:25] W końcu doszliśmy wywód.
[00:11:25 - 00:11:27] Maciemy świetnie wszystko gotowe,
[00:11:27 - 00:11:29] jeżeli chodzi o wejście.
[00:11:29 - 00:11:31] Na wyjściu pod finały
[00:11:31 - 00:11:33] z szkopa.
[00:11:33 - 00:11:35] I potrzebujemy sygnał,
[00:11:35 - 00:11:37] który nam trochę seksualizuje,
[00:11:37 - 00:11:39] kiedy coś się wydarzyło w obiektach
[00:11:39 - 00:11:41] i jakiego poziomu było to
[00:11:41 - 00:11:43] wywołujemy do obserwacji
[00:11:43 - 00:11:45] to, co jest na wejściu
[00:11:45 - 00:11:47] i to, co jest na wejściu.
[00:11:47 - 00:11:49] Także ten szkół będzie nam to przedstawia.
[00:11:49 - 00:11:51] I teraz popatrzcie jeszcze na instrukcję.
[00:11:51 - 00:11:53] Tutaj jest napisana taka podługa.
[00:11:53 - 00:11:55] Okej, wejście.
[00:11:55 - 00:11:57] Nie chcę wam nie czytać,
[00:11:57 - 00:11:59] i dzisiaj mądrzyliście o tym,
[00:11:59 - 00:12:01] ale proszę, żebyście przed egzaminem,
[00:12:01 - 00:12:03] nie przed moim urodniczeniem,
[00:12:03 - 00:12:05] bo ja tutaj wyjście o to,
[00:12:05 - 00:12:07] ale chciałbym, żebyście wyjście do mnie
[00:12:07 - 00:12:09] i nie powiedział, że tego nie zrobiłem.
[00:12:09 - 00:12:11] Otóż zadanie przykładowych
[00:12:11 - 00:12:13] znajdziecie coś takiego, że
[00:12:13 - 00:12:15] model,
[00:12:15 - 00:12:20] nie wiem,
[00:12:22 - 00:12:24] tu jest taka samowa wukaj,
[00:12:24 - 00:12:26] a to kiedyś przerabiałem
[00:12:26 - 00:12:28] na swój piosenmarker
[00:12:28 - 00:12:30] i przepokrymowałem.
[00:12:30 - 00:12:32] Zwróćcie uwagę, że zakres od 0 do 10 W
[00:12:32 - 00:12:34] odpowiada liniową wysokości
[00:12:34 - 00:12:36] cieszę pod 0 do 20 W,
[00:12:36 - 00:12:38] czyli jest sygnał przeskalowany
[00:12:38 - 00:12:40] dwukrotnie.
[00:12:40 - 00:12:42] Wiedzieć, że
[00:12:42 - 00:12:44] 10 W to jest 20 metrów
[00:12:44 - 00:12:46] trzeba użyć
[00:12:46 - 00:12:51] bloczka
[00:12:51 - 00:12:53] Ja tego na zaliczaniu
[00:12:53 - 00:12:55] nie daję, więc u mnie w ogóle nie potrzebna
[00:12:55 - 00:12:57] to w ogóle jest ta sama,
[00:12:57 - 00:12:59] ale zawsze z 0 do 20 W
[00:12:59 - 00:13:01] odnata 0 do 10 W
[00:13:01 - 00:13:03] nie ma tego przeskalowania
[00:13:03 - 00:13:05] ale na egzaminie
[00:13:05 - 00:13:07] wywało, zbywa
[00:13:07 - 00:13:09] albo i jest, nie wiem,
[00:13:09 - 00:13:11] więc tu przedam.
[00:13:11 - 00:13:13] U mnie tego nie będzie, więc
[00:13:13 - 00:13:15] nigdy tego nie będzie, proszę
[00:13:15 - 00:13:17] doprowadzić do modelu WTD
[00:13:17 - 00:13:19] ale złota zasada jest taka,
[00:13:19 - 00:13:21] już wyjażdżam,
[00:13:21 - 00:13:23] poza tym, że
[00:13:23 - 00:13:25] jest jeszcze kilka,
[00:13:25 - 00:13:27] jest jaka bardzo ważna informacja
[00:13:27 - 00:13:29] w instrukcji
[00:13:29 - 00:13:31] popatrzcie,
[00:13:31 - 00:13:33] model układ
[00:13:33 - 00:13:35] pomiarowo sterujący
[00:13:35 - 00:13:37] pracuje z cyklem
[00:13:37 - 00:13:39] 1 sekundem.
[00:13:39 - 00:13:41] Części z was, już na laboratorium,
[00:13:41 - 00:13:43] to dniałem. Części na tym do naćwiczenia
[00:13:43 - 00:13:45] pokazywamy
[00:13:45 - 00:13:47] prawidolny ruch
[00:13:47 - 00:13:49] jeżeli tak jest napisane
[00:13:49 - 00:13:51] 1 sekundę, to wystawiamy sobie 1 sekundę
[00:13:51 - 00:13:53] czyli wchodzimy tutaj
[00:13:53 - 00:13:58] tutaj prawidolny ruch
[00:13:58 - 00:14:01] tu, czy co nowe, to ok.
[00:14:01 - 00:14:03] pojawia
[00:14:03 - 00:14:05] właśnie to
[00:14:05 - 00:14:07] tutaj często jest
[00:14:07 - 00:14:09] laboratoria
[00:14:09 - 00:14:11] czyli zwiętny skór, wydecham regularnie
[00:14:11 - 00:14:13] i tu stawiamy wpis
[00:14:13 - 00:14:15] i tutaj zgodnie z dyskubu
[00:14:15 - 00:14:17] jest 1 sekund, ale jest tutaj 1
[00:14:17 - 00:14:19] 1 sekund
[00:14:19 - 00:14:21] oddać, a może was z tyłu niech będzie dziedziczą
[00:14:21 - 00:14:23] 2 sekundę kolejnego
[00:14:23 - 00:14:25] nie przesadzamy
[00:14:25 - 00:14:27] nie wpisujemy na zaś
[00:14:27 - 00:14:29] zawsze, ale tylko nie na na serce
[00:14:29 - 00:14:31] to jest to razy wiecie, że może będziecie
[00:14:31 - 00:14:33] długowieć prowadzić napisze
[00:14:33 - 00:14:35] a, chyba tak, że czasami nawet jak braknie
[00:14:35 - 00:14:37] na ruch przystniemy, chyba, czy szenictwo
[00:14:37 - 00:14:39] to panczy, ale dobrze
[00:14:39 - 00:14:41] do filmu czekam, jaka jest jedna piskacja z problemu na serce
[00:14:41 - 00:14:43] z dyskubu
[00:14:43 - 00:14:45] jak tego nie prowadzicie
[00:14:45 - 00:14:47] to skrypt nie zadziałam
[00:14:47 - 00:14:49] w podsłędach, objawiamy się to błędem
[00:14:49 - 00:14:51] który
[00:14:51 - 00:14:53] pojawia się we wcimie i mówi o tym, że
[00:14:53 - 00:14:55] encym nie pracuje na zmienieniu
[00:14:55 - 00:14:57] w skoku czasu
[00:14:57 - 00:14:59] tylko na powierzchnie jakaś ta
[00:14:59 - 00:15:01] erologiczna, ale on dyskukuje
[00:15:01 - 00:15:03] więc jeżeli nie chcecie tego problemu
[00:15:03 - 00:15:05] to
[00:15:05 - 00:15:07] proszę, dam się to ustawić
[00:15:07 - 00:15:09] nie dajcie na terenie
[00:15:09 - 00:15:11] kilka mirant, 4, 5
[00:15:11 - 00:15:13] powinno być oliczny, możecie być
[00:15:13 - 00:15:25] skąpał
[00:15:25 - 00:15:27] to jest
[00:15:27 - 00:15:29] to jest
[00:15:29 - 00:15:31] wyłącznie
[00:15:31 - 00:15:33] ustawinizowanie obiektu
[00:15:33 - 00:15:35] proszę, ale obiektu
[00:15:35 - 00:15:37] to jest
[00:15:37 - 00:15:39] ustawinizowanie obiektu
[00:15:39 - 00:15:41] proszę, ale obiektu
[00:15:41 - 00:15:43] ustawinizowanie obiektu
[00:15:43 - 00:15:45] to jest
[00:15:45 - 00:15:47] już 90%
[00:15:47 - 00:15:49] to
[00:15:49 - 00:15:51] okoczej niebanej wyspłaści
[00:15:51 - 00:15:53] no, może być to na przykład
[00:15:53 - 00:15:55] tak, ale nie trzeba ustawić, żebyście pamiętali
[00:15:55 - 00:15:57] albo tysiąc
[00:15:57 - 00:15:59] albo wśród 500 do tego dnia
[00:15:59 - 00:16:04] jeszcze jest kilkurezpokójna zmiana
[00:16:04 - 00:16:06] żeby sobie to sprawdzić
[00:16:06 - 00:16:08] coś tam właśnie, ale już nie wieram
[00:16:08 - 00:16:10] natomiast, gdybyście chcieli
[00:16:10 - 00:16:12] nie wiem, na pewno nie jest tak układać
[00:16:12 - 00:16:14] tylko usłyszymy
[00:16:14 - 00:16:16] tylko usłyszymy, nie chcielibyście
[00:16:16 - 00:16:18] tego, jak przeszedzwaliście
[00:16:18 - 00:16:20] kilkusem stop-time
[00:16:20 - 00:16:22] albo się odpędzicie, jeżeli się cerało milio
[00:16:22 - 00:16:24] to pojawia się taki wykres
[00:16:24 - 00:16:26] no i
[00:16:26 - 00:16:28] ani jaka nie na skrzynach na kawałkę
[00:16:28 - 00:16:30] ani wy do końca dobrze nie osłyszycie
[00:16:30 - 00:16:32] no, większości rzeczy nie widzę
[00:16:32 - 00:16:34] przydałobyśmy kawałkę
[00:16:34 - 00:16:36] no, wycisk wykres
[00:16:36 - 00:16:38] wtedy można nałożyć
[00:16:38 - 00:16:40] tak, że
[00:16:40 - 00:16:42] tysiąc, 22 tysiąca
[00:16:42 - 00:16:44] i teraz
[00:16:44 - 00:16:46] w tym sekundzie możemy zrobić
[00:16:46 - 00:16:48] skok sterowania
[00:16:48 - 00:16:50] czyli tutaj ten step, zmieniamy na coś 500
[00:16:50 - 00:16:52] i dodajemy
[00:16:52 - 00:16:54] dnożnik, jedna razy jedno
[00:16:54 - 00:16:56] to jest taki głód dnożnik, który będzie
[00:16:56 - 00:16:58] przeszedzwalony, dosłownie przeszedzimy
[00:16:58 - 00:17:00] na tym nawiczeniu
[00:17:00 - 00:17:02] i dodać nam wystarczy do oszacowania kawałki
[00:17:02 - 00:17:04] także zmieniam to
[00:17:04 - 00:17:06] na moment, w którym już się obień jest stabilny
[00:17:06 - 00:17:08] i wtedy dodajemy 10 prędów do sterowania
[00:17:08 - 00:17:10] i tam ok
[00:17:10 - 00:17:12] rażnie
[00:17:12 - 00:17:17] właściwie
[00:17:17 - 00:17:19] coś się pojawiło
[00:17:19 - 00:17:21] w przypadku tego wykresu
[00:17:21 - 00:17:23] nawet instrukcja mówię, rozdziel to na dwa
[00:17:23 - 00:17:25] rozdziałamy z nim na dwa
[00:17:25 - 00:17:27] zachęcam, żeby trzymać kolejny szkód samą
[00:17:27 - 00:17:29] czyli, że u góry jest w pół
[00:17:29 - 00:17:31] a do tego jest w kolejnym
[00:17:31 - 00:17:33] dlaczego?
[00:17:33 - 00:17:35] można przeżywkać
[00:17:39 - 00:17:41] nie leży wam makna
[00:17:41 - 00:17:43] to, żebyście sobie z nami nie wyzyknęło
[00:17:44 - 00:17:46] jak tu można je odwrócić?
[00:17:46 - 00:17:48] ma w ogóle dwie kolejności?
[00:17:48 - 00:17:49] no i na ciepło
[00:17:49 - 00:17:51] ujeźdźcie
[00:17:51 - 00:17:53] drugie czy drugie
[00:17:53 - 00:17:55] tak, że
[00:17:55 - 00:17:57] w tym momencie
[00:17:57 - 00:17:59] w tym momencie
[00:17:59 - 00:18:01] było nieco
[00:18:01 - 00:18:03] poszucenie w przypadku na zawiczenia
[00:18:03 - 00:18:05] kiedy coś nie działała
[00:18:05 - 00:18:12] a czasami się odwrotnie
[00:18:12 - 00:18:14] jesteśmy
[00:18:14 - 00:18:16] to jest masz
[00:18:16 - 00:18:18] to jest masz
[00:18:18 - 00:18:20] szalot
[00:18:20 - 00:18:22] i teraz tak, że modelu modelu symuniku
[00:18:22 - 00:18:24] identyfikacja obiektu czy modela na 10%
[00:18:24 - 00:18:26] wyruszenie skrótkowego
[00:18:26 - 00:18:28] sygna ustawiamy
[00:18:28 - 00:18:30] a prawda jest taka, że chcę
[00:18:30 - 00:18:32] oba skrytna to
[00:18:32 - 00:18:35] można ustawić coś takiego
[00:18:35 - 00:18:37] to, że będzie wszystko widać
[00:18:37 - 00:18:39] teraz, człowieka skryta
[00:18:39 - 00:18:41] u was, który jest prinskim po prostu
[00:18:41 - 00:18:43] skopi i dostoska i sklejacie
[00:18:43 - 00:18:45] jeżeli chcecie, możecie dzisiaj zrobić
[00:18:45 - 00:18:50] punkt pierwszy załatwiał
[00:18:50 - 00:18:52] punkt drugi
[00:18:52 - 00:18:54] i widzę okrębkę na razie
[00:18:54 - 00:18:56] dwa wejście, numer jeden to okrębka
[00:18:56 - 00:18:58] dwa wejście, numer jeden to okrębka
[00:18:58 - 00:19:00] i ten ską
[00:19:00 - 00:19:02] czy ktoś przygotowuje sobie
[00:19:02 - 00:19:12] to sprowadzanie ze mną
[00:19:12 - 00:19:14] tak, doda
[00:19:14 - 00:19:16] to znowu jak tam przykracie
[00:19:16 - 00:19:18] a czemu jest ze wstydzioł
[00:19:18 - 00:19:20] i to się wstydziało
[00:19:20 - 00:19:22] bo to z nimi
[00:19:22 - 00:19:24] bo jak wstydzioł
[00:19:24 - 00:19:26] jeżeli ktoś z nimi na ofis
[00:19:26 - 00:19:28] to będzie miał odpowiedź
[00:19:28 - 00:19:30] ok
[00:19:30 - 00:19:32] ok
[00:19:32 - 00:19:34] ok
[00:19:34 - 00:19:36] ok
[00:19:36 - 00:19:38] ok
[00:19:38 - 00:19:40] ok
[00:19:40 - 00:19:42] ok
[00:19:42 - 00:19:44] ok
[00:19:44 - 00:19:46] ok
[00:19:46 - 00:19:48] ok
[00:19:50 - 00:19:52] ok
[00:19:52 - 00:19:54] ok
[00:19:54 - 00:19:56] ok
[00:19:56 - 00:19:58] ok
[00:20:00 - 00:20:02] dlaczego mówię o ofis, bo musicie się przyzwyczaić
[00:20:02 - 00:20:04] wiesz, że
[00:20:04 - 00:20:06] jak ktoś tutaj zrobi tego dzisiaj ze mną
[00:20:06 - 00:20:08] to za dwa tygodnie będzie miał
[00:20:08 - 00:20:10] ej, ja tego mówię
[00:20:10 - 00:20:12] naprawdę czasami powod
[00:20:12 - 00:20:14] więc ja mam się to sobie uwagać, że jest Libra Office
[00:20:14 - 00:20:16] to naszego ze swojej wystarczy
[00:20:16 - 00:20:18] ale jak już w momencie zdjęcia
[00:20:18 - 00:20:20] to odlejemy, że na pewno znajdziecie
[00:20:20 - 00:20:22] to jest tekst
[00:20:22 - 00:20:24] obrazek tekst, czyli sposób wyrobania tekstu
[00:20:24 - 00:20:26] wtedy nie musicie klikać
[00:20:26 - 00:20:28] 20 razy
[00:20:28 - 00:20:30] nie będzie nic wieszkiego
[00:20:30 - 00:20:32] ale wiem, że
[00:20:32 - 00:20:34] generuje to niepotrzebną złość
[00:20:34 - 00:20:36] i nie lubię, że trzeba się oklikać enterów
[00:20:36 - 00:20:38] żeby ten tekst jakoś rozłożyć
[00:20:38 - 00:20:40] w rekardce
[00:20:40 - 00:20:42] a tak naprawdę to się odczuwa
[00:20:42 - 00:20:44] tak, że kopiujcie z oczówka
[00:20:44 - 00:20:46] nie do klików
[00:20:46 - 00:20:48] po prostu zawsze cały ekran
[00:20:48 - 00:20:50] tak, że jeżeli macie wykres
[00:20:50 - 00:20:52] to proszę opuścić do baksenalizowania
[00:20:52 - 00:20:54] i te drugie z kopiujesz
[00:20:54 - 00:20:56] ale jeżeli macie wykres
[00:20:56 - 00:20:58] ale stoi w lotopie, będzie różny napisań
[00:20:58 - 00:21:00] i jak by generujecie kandałów
[00:21:00 - 00:21:02] a będę go na pewno świetnie widział
[00:21:02 - 00:21:04] to się niech zawsze da się dobrze
[00:21:14 - 00:21:16] tak, że jak rzuca Cię
[00:21:16 - 00:21:18] jak rzuca Cię wykresu
[00:21:18 - 00:21:20] to proszę w całości
[00:21:20 - 00:21:22] na swojej lotopie nie można pisać
[00:21:22 - 00:21:24] czy tylko w lotopie?
[00:21:24 - 00:21:26] też piszę Cię tak na egzaminie
[00:21:26 - 00:21:28] więc się tak otrzymowę
[00:21:28 - 00:21:30] wiem, że jest na swojej proście
[00:21:30 - 00:21:32] i nawet w perspektywie
[00:21:32 - 00:21:34] że jest swoje klawiatury
[00:21:46 - 00:21:48] jeszcze raz
[00:21:48 - 00:21:50] jeszcze raz zaznaczone
[00:21:50 - 00:21:52] całe zaliczenie możecie przeręcieć
[00:21:52 - 00:21:54] na skopiowanie z oczówka i skleju
[00:21:54 - 00:21:56] żadnych wycinek
[00:21:56 - 00:21:58] niektórzy oczają wymagini
[00:21:58 - 00:22:00] nie, nie, nie
[00:22:00 - 00:22:02] do 40 minut macie
[00:22:02 - 00:22:04] jak widzę, że ktoś oprawia modkę w bilbie
[00:22:04 - 00:22:06] to nie jest
[00:22:06 - 00:22:08] set na tego problemu
[00:22:08 - 00:22:10] całe zaliczenie te się zróbcemy
[00:22:10 - 00:22:12] tylko plejają uroczy
[00:22:12 - 00:22:14] ewentualnie coś śpiszemy z klawiatury
[00:22:14 - 00:22:16] i taki ładny
[00:22:16 - 00:22:18] to jest wszystko podstawowe
[00:22:18 - 00:22:20] dobrze
[00:22:20 - 00:22:22] wróczmy do tematu
[00:22:22 - 00:22:24] identyfikacji
[00:22:24 - 00:22:26] w inercja
[00:22:26 - 00:22:28] to nas interesuje
[00:22:28 - 00:22:30] ten fragment, czyli po skoku
[00:22:30 - 00:22:32] nie przejdziemy
[00:22:32 - 00:22:34] i inercja
[00:22:34 - 00:22:36] to stawia na inercje
[00:22:36 - 00:22:38] dobra, to stawia
[00:22:38 - 00:22:40] na podwójne inercje
[00:22:40 - 00:22:42] a kto ma inercje do płynienia
[00:22:43 - 00:22:45] jej, ja poczęciałam, co jest dobra
[00:22:47 - 00:22:49] dlaczego jeszcze do płynienia?
[00:22:49 - 00:22:51] to mać się tutaj
[00:22:51 - 00:22:53] od całego skoku
[00:22:53 - 00:22:55] jest
[00:22:55 - 00:22:56] od płynienia
[00:22:56 - 00:22:58] jest z tym całym
[00:22:58 - 00:23:00] mimo, że tu wzór
[00:23:00 - 00:23:02] tu jeszcze trzymał się
[00:23:02 - 00:23:04] bez miast
[00:23:04 - 00:23:06] to znaczy, że jest od płynienia
[00:23:06 - 00:23:08] bywają pomady po dwójnej inercji
[00:23:08 - 00:23:10] które mają takie bardzo łamanie
[00:23:11 - 00:23:13] i czasami to może być
[00:23:13 - 00:23:15] podwójne inercje
[00:23:15 - 00:23:17] jak byśmy dołożyli do tej kaskady jeszcze jeden zbiornik
[00:23:17 - 00:23:19] to już powstanie dosłownie inercje
[00:23:22 - 00:23:24] że jak dorzucę zbiornik to jest podwójne?
[00:23:24 - 00:23:26] nie
[00:23:26 - 00:23:28] ja Wam pokażę to
[00:23:28 - 00:23:30] na końcu skrytu
[00:23:30 - 00:23:32] że jeżeli użyjemy złego
[00:23:32 - 00:23:34] obiektu
[00:23:34 - 00:23:36] dla naszego prawdziwego obiektu
[00:23:36 - 00:23:38] to się wewnątrz się skryty
[00:23:38 - 00:23:40] a jeżeli ten skrypt będzie dopasowany
[00:23:40 - 00:23:42] do podwójnej inercji
[00:23:42 - 00:23:44] a w rzeczywistości obiektu
[00:23:44 - 00:23:46] to jest podwójne inercja
[00:23:46 - 00:23:48] to Wam się nie nołożę
[00:23:48 - 00:23:50] będziecie widzieć, że obiektu
[00:23:50 - 00:23:52] Wam się rozbiechało
[00:23:52 - 00:23:54] i trzeba go poprawić
[00:23:54 - 00:23:56] więc zobaczcie
[00:23:56 - 00:23:58] będę zaraz nie kontywał obiektu
[00:23:58 - 00:24:00] ale pokażę dobrze
[00:24:00 - 00:24:02] jeżeli ubraliście żuby
[00:24:02 - 00:24:04] to ta się to wychwyci
[00:24:04 - 00:24:06] na podstawie jednego wykresu
[00:24:06 - 00:24:08] jeżeli nie
[00:24:12 - 00:24:14] zobaczcie tu, ale wygórny ruch
[00:24:14 - 00:24:16] ustawienia
[00:24:16 - 00:24:18] logic, log day
[00:24:18 - 00:24:20] ja wczoraj żyję to na tym ustawieniu
[00:24:26 - 00:24:28] tutaj
[00:24:28 - 00:24:30] rybik
[00:24:30 - 00:24:32] ta zakładka i te ustawienia
[00:24:32 - 00:24:34] i tak
[00:24:34 - 00:24:36] i tak
[00:24:36 - 00:24:39] a nie ma tego
[00:24:39 - 00:24:41] rybików
[00:24:41 - 00:24:43] i tak
[00:24:43 - 00:24:45] i tak
[00:24:45 - 00:24:47] i tak
[00:24:47 - 00:24:49] i tak
[00:24:49 - 00:24:51] i tak
[00:24:51 - 00:24:53] i tak
[00:24:53 - 00:24:55] i tak
[00:24:55 - 00:24:57] i tak
[00:24:57 - 00:24:59] i tak
[00:24:59 - 00:25:01] i tak
[00:25:01 - 00:25:03] i tak
[00:25:03 - 00:25:05] i tak
[00:25:05 - 00:25:07] i tak
[00:25:19 - 00:25:21] czekam
[00:25:23 - 00:25:25] i tak
[00:25:27 - 00:25:29] a ale
[00:25:29 - 00:25:35] Bez zadejścia, dobra? Zegarków na tłocze, telefonów, różne, do co?
[00:25:35 - 00:25:42] Uczciwiajmy, uczciwiajmy, że to będzie ok, a jedna rzecz.
[00:25:42 - 00:25:46] Jeżeli chcecie to napisać na pierwszym terminie, to przeluczy sobie wszystkie zadania.
[00:25:46 - 00:25:50] Jakieście jest w głowie. Bo ja wiem dzisiaj, gdy mówię teraz po pierwsze półtorek,
[00:25:50 - 00:25:54] to ja mówię na godzinę i mówię ci, ej, tam rzeczy się ogadam, czyli to jest takie trudne.
[00:25:54 - 00:25:56] Zrobicie to pięć razy do rzędu.
[00:25:56 - 00:25:58] Pokażę się, że to jest wyklikanie.
[00:25:58 - 00:26:01] Muszę być w tą opcję, muszę być w tą opcję, muszę być w tą opcję.
[00:26:01 - 00:26:02] Przeklikać.
[00:26:02 - 00:26:04] Ale tak jak z kombinacji nie wiem nigdy.
[00:26:04 - 00:26:09] Jeżeli chcesz się załapieć, to już te dodalki karnała, zaznaczenia robię po to klikanie.
[00:26:09 - 00:26:11] I to wykład nie dostaną.
[00:26:11 - 00:26:15] Ale jeżeli będziecie wychodzić z tego, że zobaczymy, co będzie na ręczeniu,
[00:26:15 - 00:26:18] i jak to będzie, to to będzie ciekawe.
[00:26:18 - 00:26:20] Mówię uczciwie, bo wiem ile jest klikanie.
[00:26:20 - 00:26:24] Ale jak lubicie to w domu, będziecie więcej przeklikać.
[00:26:24 - 00:26:26] Dlaczego to klikacie?
[00:26:26 - 00:26:28] Nikt z was tu nie zaskoczył.
[00:26:28 - 00:26:30] A na egzaminie jest troszkę szybciej,
[00:26:30 - 00:26:32] i podobno jeszcze są pytania.
[00:26:32 - 00:26:34] Nie wiesz, tak będzie.
[00:26:34 - 00:26:36] Bywało coś.
[00:26:36 - 00:26:38] Panie.
[00:26:42 - 00:26:44] Ale ja to słyszałem.
[00:26:44 - 00:26:46] Są pytania czasami od drzwickiego.
[00:26:46 - 00:26:48] Ja nic się żaden nie pytałem,
[00:26:48 - 00:26:50] chyba że ktoś szczęga to w ten zadań.
[00:26:51 - 00:26:53] I jest by to wykres.
[00:26:53 - 00:26:56] On po kliknięciu ramy powinien się dobrze nie dowodzawać.
[00:26:56 - 00:26:58] Podleci tej innej auty.
[00:26:58 - 00:27:02] Jeżeli się komuś nie przeniosło,
[00:27:02 - 00:27:05] to trzeba kliknieć tego, że raz ramy,
[00:27:05 - 00:27:08] albo jeszcze na ręce,
[00:27:08 - 00:27:10] czy nie uskróci.
[00:27:10 - 00:27:12] Nie wiszemy tego w komentu jedną.
[00:27:12 - 00:27:14] Mam.
[00:27:14 - 00:27:16] Mam.
[00:27:18 - 00:27:20] Teraz tak.
[00:27:21 - 00:27:24] I teraz jeszcze linijek.
[00:27:24 - 00:27:26] Powtarzający się linijek.
[00:27:28 - 00:27:30] Trzeba zainfortować te dane.
[00:27:38 - 00:27:40] To jest duża stura.
[00:27:40 - 00:27:42] Z tym, która z czasem,
[00:27:42 - 00:27:44] to są dane.
[00:27:44 - 00:27:46] Czyli to nasze sygnały.
[00:27:46 - 00:27:48] Nie mam skupy.
[00:27:48 - 00:27:50] Nie mam skupy.
[00:27:50 - 00:27:52] Aby wybraliście spraktyły w tajm,
[00:27:52 - 00:27:54] w tym miejscu?
[00:27:54 - 00:27:56] Tak.
[00:27:56 - 00:27:58] Nie mam skupy.
[00:27:58 - 00:28:00] Nie mam skupy.
[00:28:00 - 00:28:02] Nie mam skupy.
[00:28:02 - 00:28:04] Nie ma skupy.
[00:28:04 - 00:28:06] Nie ma skupy.
[00:28:06 - 00:28:08] Nie ma skupy.
[00:28:08 - 00:28:10] Podlecimy.
[00:28:10 - 00:28:12] Potrzebujemy.
[00:28:12 - 00:28:14] Na trójkę nie trzeba skryty.
[00:28:14 - 00:28:16] Na czwórkę już tak.
[00:28:16 - 00:28:18] Tak, że
[00:28:18 - 00:28:20] a poza danym potrzebom.
[00:28:20 - 00:28:22] Ale jak ktoś ma, że chciał mi rodzić
[00:28:22 - 00:28:24] o później sobie w czasie
[00:28:24 - 00:28:26] naukę to można zrobić
[00:28:26 - 00:28:28] to metodą, jaką pokazywają
[00:28:28 - 00:28:30] w ostatniu, czyli nawet dobrać na pokro
[00:28:30 - 00:28:32] to ustawienie, nałożyć linie, na linie.
[00:28:32 - 00:28:34] Takie się za laboratorium,
[00:28:34 - 00:28:36] więc próbuj ręcznie.
[00:28:36 - 00:28:38] I też się da.
[00:28:38 - 00:28:40] Natomiast to jest tylko wyjścia, jak wyjście na trójkę
[00:28:40 - 00:28:42] i na razie miejsce ma głowę
[00:28:42 - 00:28:44] albo czas, tak jak wyjście.
[00:28:44 - 00:28:46] A tu mamy sygnały.
[00:28:46 - 00:28:48] Nie mogę już tego bardziej wymienić.
[00:28:48 - 00:28:50] Sorry.
[00:28:50 - 00:28:52] I tutaj będziecie w czas,
[00:28:52 - 00:28:54] to macie tak odnośnik.
[00:28:54 - 00:28:56] To jest jak ścieżka do klik.
[00:28:56 - 00:28:58] Outkropka, stąd ta kropka, tak.
[00:28:58 - 00:29:00] Jak odrożne, a u nas jest chyba od dwóch.
[00:29:00 - 00:29:02] I możecie sobie to
[00:29:02 - 00:29:04] plajdą.
[00:29:04 - 00:29:06] Ja to powiększyłam,
[00:29:06 - 00:29:08] żebym z tego daje wyjść.
[00:29:12 - 00:29:14] Ja do tego do razu wypełnijcie
[00:29:14 - 00:29:16] wszystkie okierka
[00:29:16 - 00:29:18] i wyskupamy.
[00:29:18 - 00:29:20] Czeka do nas.
[00:29:20 - 00:29:22] Nie no, wchodzić super.
[00:29:22 - 00:29:24] Tak.
[00:29:24 - 00:29:26] To do karłom, nie?
[00:29:26 - 00:29:28] A ja chciałam całą zsunaczyć.
[00:29:28 - 00:29:30] Nie, nie, nie, nie.
[00:29:30 - 00:29:32] Nie, nie, nie, nie, nie.
[00:29:32 - 00:29:34] A to ma całą całą zsunaczyć?
[00:29:36 - 00:29:38] Jak ścieżkę do kliku
[00:29:38 - 00:29:40] to dobra i wączy.
[00:29:48 - 00:29:50] Widzicie, to jest ja.
[00:29:56 - 00:29:58] O, to co się dzieje?
[00:29:58 - 00:30:00] Z końca dzieje się.
[00:30:00 - 00:30:02] To jest takie z krzętu.
[00:30:02 - 00:30:04] Z kręci.
[00:30:04 - 00:30:06] To jest jedna ścieżka.
[00:30:06 - 00:30:08] To jest ścieżka do
[00:30:08 - 00:30:10] T.
[00:30:10 - 00:30:12] Jak podpisuje to ten pof.
[00:30:12 - 00:30:14] Z nami zmiennych to umówne.
[00:30:14 - 00:30:16] Jak się wkleja na minutu?
[00:30:16 - 00:30:18] Zobaczcie, zawsze podprawiam się,
[00:30:18 - 00:30:20] w tym piosie, powiem, że za to,
[00:30:20 - 00:30:22] jak to się wypiję na minutu.
[00:30:22 - 00:30:24] Zobaczcie, jak macie węzku.
[00:30:24 - 00:30:26] Jak się wypiję na minutu.
[00:30:26 - 00:30:28] Ale węzku to zjawam.
[00:30:29 - 00:30:31] Kupiowanie w matlamie na tym minutu
[00:30:31 - 00:30:33] jest od A do B.
[00:30:33 - 00:30:35] Ale jak chcecie, jak tutaj?
[00:30:35 - 00:30:36] Zobaczcie, jak przypomnieć,
[00:30:36 - 00:30:37] żeby skróty do pary,
[00:30:37 - 00:30:38] żeby pomyślać,
[00:30:38 - 00:30:40] żeby zobaczyć, jak to tam.
[00:30:40 - 00:30:42] A z tego kontroli gry.
[00:30:42 - 00:30:44] Nie trzeba zapomnieć.
[00:30:44 - 00:30:46] Tak, że nie trzeba zapamiętać.
[00:30:46 - 00:30:48] Słuchaj, słuchaj.
[00:30:48 - 00:30:49] Pamiętaj, że można sobie
[00:30:49 - 00:30:51] jak to podejmować.
[00:30:51 - 00:30:53] I teraz, jak wejść
[00:30:53 - 00:30:55] zmienne sygnałowe,
[00:30:55 - 00:30:56] go chodzić do samego końca
[00:30:57 - 00:30:58] czyli wchodzimy
[00:30:58 - 00:31:00] out, scope data, signals
[00:31:00 - 00:31:02] i sygnał pierwszy, values
[00:31:02 - 00:31:04] powstaje wam taka duża ścieżka.
[00:31:09 - 00:31:11] Out, scope data,
[00:31:11 - 00:31:12] signals
[00:31:12 - 00:31:13] i tu są dwa sygnały,
[00:31:13 - 00:31:14] czyli pierwszy, no, pół,
[00:31:14 - 00:31:16] drugi ten sygnał
[00:31:16 - 00:31:17] i wchodzimy w niego
[00:31:17 - 00:31:19] i powstaje wam taka ścieżka.
[00:31:19 - 00:31:21] Jak widzicie.
[00:31:21 - 00:31:23] Tego nie zapamiętujemy,
[00:31:23 - 00:31:24] to kopiujemy,
[00:31:24 - 00:31:25] wtedy wiemy, że na pewno
[00:31:25 - 00:31:27] wszystko jest dobrze.
[00:31:30 - 00:31:32] Warto używać silników.
[00:31:32 - 00:31:34] Wasze sygnały będą działać szybciej.
[00:31:39 - 00:31:41] A jak się wkleja?
[00:31:41 - 00:31:43] No, pomóżcie.
[00:31:43 - 00:31:45] Maj, mi kopiujemy.
[00:31:51 - 00:31:53] Ja sobie tak piszę,
[00:31:54 - 00:31:56] kopie albo...
[00:31:57 - 00:31:59] No i tam ubiegamy z editora.
[00:32:00 - 00:32:02] Wiesz, co tu nie ma?
[00:32:02 - 00:32:03] Nie wiem.
[00:32:03 - 00:32:05] Próbuję, ale nie działa.
[00:32:05 - 00:32:07] Nie działa?
[00:32:07 - 00:32:09] No i jak pan tak ojdzie?
[00:32:09 - 00:32:11] Ej, do torny.
[00:32:11 - 00:32:13] I tutaj wklej.
[00:32:15 - 00:32:17] Z jakichś innych?
[00:32:17 - 00:32:19] Nieprawym przyciskiem, tu.
[00:32:19 - 00:32:21] Nie, wejść.
[00:32:21 - 00:32:23] Jakim było prawie przycisk, Myszy?
[00:32:23 - 00:32:25] Jeszcze raz kontroli, Krek.
[00:32:27 - 00:32:29] Kontroli, Krek.
[00:32:29 - 00:32:31] Panie, kontroli.
[00:32:37 - 00:32:39] Ty mówisz o tym, że macie jakiś pomal.
[00:32:39 - 00:32:41] Jeszcze raz do wszystkich.
[00:32:41 - 00:32:43] Jak chcecie, sprawdźcie sobie, jak jest skrót,
[00:32:43 - 00:32:45] bo do tego nikt nie będzie pamiętał.
[00:32:45 - 00:32:47] Dobra, przy tym wyższym raz skrót,
[00:32:47 - 00:32:49] dzisiaj ja nie pojawię obaw, że to...
[00:32:49 - 00:32:51] Ale, ale...
[00:32:51 - 00:32:53] A nie kopiemy?
[00:32:53 - 00:32:55] Nie wiem.
[00:32:57 - 00:32:59] My nie podtworzymy.
[00:32:59 - 00:33:01] Bo co to jest?
[00:33:01 - 00:33:03] Nie wiem, czy powinienem wistać,
[00:33:03 - 00:33:05] co jest skrót, czerwia, taniej albo...
[00:33:05 - 00:33:07] Mało wygodne.
[00:33:07 - 00:33:09] Robimy sobie takie
[00:33:09 - 00:33:11] pomocnicze zmienne.
[00:33:11 - 00:33:13] No to nazywajcie ten, Krek.
[00:33:16 - 00:33:19] I będzie nam łatwiej wistać.
[00:33:37 - 00:33:39] Nie skupam.
[00:33:39 - 00:33:41] Ręcznie można.
[00:33:45 - 00:33:47] Nie…
[00:33:47 - 00:33:49] Ale tak.
[00:33:49 - 00:33:51] Jeszcze raz,
[00:33:51 - 00:33:53] jak nie.
[00:34:01 - 00:34:03] Chyba...
[00:34:03 - 00:34:05] I zobaczcie, czy...
[00:34:05 - 00:34:07] Robert.
[00:34:09 - 00:34:11] Cześć, kreśmy.
[00:34:11 - 00:34:13] Dlaczego?
[00:34:13 - 00:34:17] I gdyby ktoś zamienił, żeby je zgadzał, to już teraz zobaczę coś innego niż...
[00:34:17 - 00:34:19] Odpowiedźmy bardzo.
[00:34:19 - 00:34:21] Naszym żodaniem jest teraz...
[00:34:23 - 00:34:25] Może średnik dałeś na końcu?
[00:34:25 - 00:34:27] Nie.
[00:34:27 - 00:34:29] O.
[00:34:31 - 00:34:33] Szukajmy.
[00:34:33 - 00:34:35] O.
[00:34:41 - 00:34:45] O.
[00:34:47 - 00:34:49] Znowu chcę pała z tym.
[00:34:49 - 00:34:51] Nie, chyba nie.
[00:34:53 - 00:34:55] Ten.
[00:34:55 - 00:34:57] Jest, ale ma pan...
[00:34:57 - 00:34:59] Najpierw szeregi.
[00:34:59 - 00:35:01] O.
[00:35:09 - 00:35:11] O, to się zgadza.
[00:35:11 - 00:35:13] O.
[00:35:15 - 00:35:17] O.
[00:35:31 - 00:35:33] O.
[00:35:33 - 00:35:35] O.
[00:38:21 - 00:38:23] O.
[00:38:51 - 00:38:53] O.
[00:38:53 - 00:38:55] O.
[00:38:55 - 00:38:57] O.
[00:39:07 - 00:39:09] O.
[00:39:09 - 00:39:11] O.
[00:39:11 - 00:39:13] O.
[00:39:13 - 00:39:15] O.
[00:39:15 - 00:39:17] O.
[00:39:17 - 00:39:19] O.
[00:39:19 - 00:39:22] Wydaje mi się, że ma takie same, ale zbuduje mi to, że nie da się do rądu.
[00:39:22 - 00:39:24] To już mówię.
[00:39:24 - 00:39:28] Jeżeli w policzycie, w mocieniu, w mocieniu to jest dosunek sygnału.
[00:39:28 - 00:39:30] Wejście od tego do wejście wego.
[00:39:30 - 00:39:32] Ile na wyjściu jest 1?
[00:39:32 - 00:39:34] Dobra.
[00:39:34 - 00:39:35] Czyli na wyjściu jest 1.
[00:39:35 - 00:39:36] Na wejściu ile jest?
[00:39:36 - 00:39:38] Dlaczego tego wykresuje?
[00:39:38 - 00:39:42] No...
[00:39:42 - 00:39:43] Zero.
[00:39:43 - 00:39:45] 1,3,0 po...
[00:39:45 - 00:39:47] Nie skończaj.
[00:39:47 - 00:39:49] A bo nie robimy tak.
[00:39:50 - 00:39:55] Znaczy poważną pokażuję, ponieważ taki bądź się pojawia regularnie od parola.
[00:39:55 - 00:39:58] Chcę, żebyście wiedzieli, że jeżeli sobie nie wiem, czy to taki bądź 1,
[00:39:58 - 00:40:01] to wy robicie dzielenie przez 0,
[00:40:01 - 00:40:04] Mataw skarzy wam infinity by...
[00:40:04 - 00:40:06] ...przestrząsniają.
[00:40:06 - 00:40:10] I ogólnie dużo takich infinity się pojawi tak, tak?
[00:40:10 - 00:40:11] To musi być inwizja.
[00:40:11 - 00:40:13] Dlaczego inwizja jest 1?
[00:40:13 - 00:40:17] Bo my chcemy, żeby cały ten wykres tu pokazywał,
[00:40:17 - 00:40:20] żeby nam o ile skończyło sterowanie.
[00:40:20 - 00:40:22] Nasze sterowanie skończyło do...
[00:40:22 - 00:40:24] ...500.
[00:40:24 - 00:40:30] Bo mieliśmy pięćdziesiątych i poniesieć dwudziestu.
[00:40:30 - 00:40:32] Która tu skończyło 500?
[00:40:32 - 00:40:34] Jeżeli odejmujemy...
[00:40:34 - 00:40:37] ...próbka tysiąc pięćset lat od tej 30 tysiąc pięćset lat pierwszej,
[00:41:08 - 00:41:16] Pamiętajcie, że jeżeli to odobieracie, to odnoście się od tego, co macie w tych bloczku.
[00:41:16 - 00:41:21] Symoniku do kimś bloczek jedyny, żeby uniać się to pora metra.
[00:41:21 - 00:41:22] 4.
[00:41:22 - 00:41:23] Step.
[00:41:23 - 00:41:25] To jest dokładnie to, że jest stepie.
[00:41:25 - 00:41:27] Okej, to jest step.
[00:41:27 - 00:41:29] To jest stepie.
[00:41:29 - 00:41:31] To jest step.
[00:41:38 - 00:41:40] To jest stepie.
[00:41:40 - 00:41:42] A to nie ma testa.
[00:41:42 - 00:41:45] Jest stepie z tego, co ja widziałam.
[00:41:50 - 00:41:52] Płonoczenie nie robi się.
[00:41:52 - 00:41:53] Tak.
[00:41:53 - 00:41:56] Płonoczenie nie robi się, bo chcesz odnościać, a nie...
[00:41:56 - 00:41:58] ...zrobić tylko na połowę szykusek.
[00:42:07 - 00:42:09] O, nie, nie.
[00:42:14 - 00:42:16] Kurwa, kurwa, kurwa.
[00:42:25 - 00:42:27] A to jest tak, że nie ma testa.
[00:42:27 - 00:42:30] 15 tysiąc pięćset lat od tej 30 tysiąc.
[00:42:30 - 00:42:32] Dobra, nie ma testa.
[00:42:32 - 00:42:34] Tak, to jest tak, że nie ma testa.
[00:42:34 - 00:42:36] Zobiejmy, że to jest tak, że nie ma testa.
[00:42:36 - 00:42:38] Zobiejmy, że te...
[00:42:38 - 00:42:40] ...nie ma testa.
[00:42:40 - 00:42:42] Tak, że nie ma testa.
[00:42:42 - 00:42:44] Ja teraz.
[00:42:44 - 00:42:46] Zobiejmy, że to jest tak, że nie ma testa.
[00:42:46 - 00:42:48] Tak, to jest tak, że nie ma testa.
[00:42:48 - 00:42:50] O nie, tak, tak.
[00:42:50 - 00:42:52] O nie, tak, tak.
[00:42:52 - 00:42:54] Nie pokazuję.
[00:42:54 - 00:42:56] Jesteśmy w końcu.
[00:42:56 - 00:42:58] O nie, nie.
[00:42:58 - 00:43:00] O nie, nie, nie.
[00:43:00 - 00:43:02] O nie, nie.
[00:43:02 - 00:43:04] O nie, nie.
[00:43:04 - 00:43:06] O nie, nie, nie.
[00:43:06 - 00:43:08] O nie, nie, nie.
[00:43:08 - 00:43:10] O nie, nie, nie, nie.
[00:43:10 - 00:43:27] Oglądamy na ciebie, że doszło do tego momentu, tylko w boliwarnie, z ekranetką musimy wydać chyba.
[00:43:27 - 00:43:34] Także, takie coś jak macie, jest pochłoki, mamy wycięty, wykres.
[00:43:34 - 00:43:40] Jeżeli wczoraj jest na wejściu, możemy zaczynać tą identyfikację już z kryptomu.
[00:43:40 - 00:43:42] Ja nazywam to w ten sposób.
[00:43:42 - 00:43:49] Szukamy ostatniej próbki, wejścia od pracy o próbki.
[00:43:49 - 00:43:51] Wejścia.
[00:43:51 - 00:43:56] Czyli chcemy dzięki temu oszacowe przyszłość się pokazać.
[00:43:56 - 00:43:59] I to nam się przyda, nie tylko w tym wieku.
[00:44:04 - 00:44:06] I teraz tak, materiały pomoców, czym mówią.
[00:44:06 - 00:44:15] Jeżeli jest to inna akcja dotrudnienia, o której ja tutaj wspomniałem, to te będziemy liczyć jako te 90-10 przez te dwa.
[00:44:15 - 00:44:18] Ta kolejna będzie na 10-10, tak.
[00:44:18 - 00:44:24] Zróbcie uwagę na jedną charakterystyczną cechę tego skrytu, który mam tutaj pokażę.
[00:44:25 - 00:44:28] Nie są ferni zbieżne z czterema obiektami.
[00:44:28 - 00:44:30] Czterema, która decyduje żonę do nadaliczeniem.
[00:44:30 - 00:44:32] Czyli macie ten wiek 10.
[00:44:32 - 00:44:34] Jeżeli umiecie je znaleźć w ten maszyl, tak.
[00:44:34 - 00:44:38] To możecie powiedzieć, że inna akcja, inna akcja dotrudnienia, pokójna inna akcja, pokójna inna akcja dotrudnienia,
[00:44:38 - 00:44:41] leksonunia, czy też kryptury wyniki powód.
[00:44:41 - 00:44:44] Czyli czasami dzielot 3, 2, a czasami 3, 3.
[00:44:44 - 00:44:48] Czasami licząc tał, a czasami nie, ok.
[00:44:48 - 00:44:51] Także, jedna metoda, cztery obieki.
[00:44:52 - 00:44:57] Teraz to, co będziemy robić, będziecie skupiać na terenie zielotych punktów T10 i T90,
[00:44:57 - 00:45:00] czyli z jakiejbym sterowania.
[00:45:00 - 00:45:02] I teraz, jak to zrobić?
[00:45:02 - 00:45:04] Metoda jest ta sama, to wyżej.
[00:45:04 - 00:45:07] Czyli linika, kwierna, linika, kąpion, to głównie.
[00:45:07 - 00:45:09] Tylko one się teraz pozyskają w 10.
[00:45:09 - 00:45:17] To jest maks od 5, od Y, który jest mniejszy lub równy Y,
[00:45:17 - 00:45:20] czyli maksywalną wyjściu.
[00:45:21 - 00:45:24] To, co wam ostatnio pokazywałem i robiliście ręcznie.
[00:45:24 - 00:45:27] Szukaliście skoku od skoku, policzyliście na korporatorze.
[00:45:27 - 00:45:28] Aha, tak.
[00:45:28 - 00:45:30] Mam też poczuć, podróż z piorniku.
[00:45:30 - 00:45:32] Co szukamy, jakiegoś tam punktu 63%.
[00:45:32 - 00:45:33] No, pamiętacie.
[00:45:33 - 00:45:36] Mam nadzieję, że było coś takiego przed majówką.
[00:45:36 - 00:45:43] Linika, tak jak mówiłem, zbierda w pełni z tą liniką w przyszniejszą.
[00:45:43 - 00:45:47] Tutaj nie ma żadnych nowości.
[00:45:47 - 00:45:49] Dlaczego jest to lubite?
[00:45:50 - 00:45:52] Tak, jak poprzedni.
[00:45:52 - 00:45:57] Nie znamy, czy z nuda trupki jest nasz obiad.
[00:45:57 - 00:45:59] Więc musimy znaleźć trupkę, linika,
[00:45:59 - 00:46:01] a później dopiero możemy znaleźć prawidłego czasu.
[00:46:01 - 00:46:12] Idziemy tutaj.
[00:46:12 - 00:46:14] Ja nas proszę, żebyście się zrobili również tak.
[00:46:14 - 00:46:16] 90.
[00:46:16 - 00:46:18] Ile dla was, tak?
[00:46:18 - 00:46:19] A ja...
[00:46:19 - 00:46:26] To nam prawie w głębie.
[00:46:42 - 00:46:46] Jak ktoś ma problem, to mogę teraz podejść,
[00:46:46 - 00:46:48] a międzyczasiem proszę, żebyście jeszcze będzie chcieli.
[00:46:48 - 00:46:49] No, szybkie pytanie.
[00:46:49 - 00:46:51] Dobra.
[00:47:11 - 00:47:14] To jest to, żeby znaleźć dziewięć minut prostych z tym,
[00:47:14 - 00:47:16] ale mogli być lewe, line i ten.
[00:47:16 - 00:47:17] Aha, jeszcze jest...
[00:47:17 - 00:47:19] Jedy fiedl.
[00:47:19 - 00:47:21] To będzie pora zero na całość.
[00:47:21 - 00:47:22] Line.
[00:47:22 - 00:47:24] A ta uroba na siłowe?
[00:47:24 - 00:47:25] To jest...
[00:47:25 - 00:47:27] Siłowa uroba na siłowe.
[00:47:27 - 00:47:29] To będzie oznany na świetnie.
[00:47:29 - 00:47:30] Czyli jak mamy...
[00:47:30 - 00:47:31] Aha.
[00:47:32 - 00:47:34] To już się całkiem ciężko wyśpiewa.
[00:47:34 - 00:47:36] To jest to, żeby on to nie wyśpiewał,
[00:47:36 - 00:47:37] i zainteresować.
[00:47:37 - 00:47:38] Tak, nie wierzę.
[00:47:38 - 00:47:40] I tak, to będzie ten punkt.
[00:47:40 - 00:47:42] Ech!
[00:48:10 - 00:48:12] To jest...
[00:48:12 - 00:48:14] ...cena z kompleksu.
[00:48:14 - 00:48:15] To do razu.
[00:48:15 - 00:48:16] Dwa określa.
[00:48:16 - 00:48:17] No i jedna kolumna.
[00:48:17 - 00:48:18] Dwa pierwsze.
[00:48:18 - 00:48:20] Dwie pierwsze zapisane jako zmienia.
[00:48:20 - 00:48:21] Dzień dobry.
[00:48:21 - 00:48:22] Dzień dobry.
[00:48:22 - 00:48:23] Ale mówię, co robimy.
[00:48:23 - 00:48:24] Dobra.
[00:48:24 - 00:48:25] To jest...
[00:48:25 - 00:48:26] ...trzciemy zapisać.
[00:48:26 - 00:48:28] To jest jedyny wakn.
[00:48:28 - 00:48:31] Raz, dwa, jedna, pierwszy wychłysk.
[00:48:31 - 00:48:33] Dwa, jedna, druga.
[00:48:33 - 00:48:34] Dzień dobry.
[00:48:34 - 00:48:35] Dzień dobry.
[00:48:35 - 00:48:36] Ale...
[00:48:36 - 00:48:37] To jest do tego duszy.
[00:48:38 - 00:48:39] O!
[00:48:41 - 00:48:43] A, w ogóle te persycenia,
[00:48:43 - 00:48:44] okładz.
[00:48:44 - 00:48:45] Dwie...
[00:48:45 - 00:48:46] Dwa pierwsze.
[00:48:46 - 00:48:48] Dwie ta kolumna.
[00:48:48 - 00:48:49] Pierwszy wychłysk.
[00:48:49 - 00:48:50] Dwa dnia na świętna.
[00:48:50 - 00:48:52] Dwa do opłata.
[00:48:52 - 00:48:53] Dwa pieresze.
[00:48:53 - 00:48:54] Dwa pora.
[00:48:54 - 00:48:55] Dwojej wykresy.
[00:48:55 - 00:48:56] Dzień dobry.
[00:48:56 - 00:48:57] Dzień dobry.
[00:48:57 - 00:48:58] Dzień dobry.
[00:48:58 - 00:48:59] Dwa rzadko.
[00:48:59 - 00:49:00] Dwa...
[00:49:00 - 00:49:01] Dzień dobry.
[00:49:01 - 00:49:02] Dwa rzadko.
[00:49:02 - 00:49:03] Dwa rzadko.
[00:49:03 - 00:49:04] Dwa wierzę.
[00:49:04 - 00:49:05] Dwa rzadko.
[00:49:05 - 00:49:06] Dwa rzadko.
[00:49:06 - 00:49:26] 12 mamy identyczne, tylko szukamy maksymalnego artystiku, żeby to wszystko działało, to musimy wiedzieć dość dobrze, kiedy się wydarzyło, więc musimy mać krótkę efekcji, dobra, poszło.
[00:49:27 - 00:49:48] I tutaj, uwaga, odpalamy regularnie skrypt. Wiem, że część uczy się na DZD. Zresztą nikt nie wie, że pamiętaj z tym, że skrypt nie kilka rada sam w końcu, ale jeżeli są błędy po drodze, to nie jest tragicznie, ciężko, z tego ryzyny, to jest takie stanie i w kombinowania, który jest błąd, który jest błąd, który jest błąd, który jest błąd.
[00:49:49 - 00:50:03] A bo przeczyta jak autospacja, a tu coś. Lepiej uruchamiać regularnie i patrzeć już następnie, są błędy, bo powinny te wykresy i takie wartości sensowne tu się pojawiać, jeżeli dobrać te same będa, albo jakieś inkliniki, to pewnie już po prostu wcześniej, nie tak.
[00:50:04 - 00:50:09] A jeżeli, uwaga, tutaj myślisz, że cały skrypt nie cię ramy i wychodzi, że się nie dostałem do pokolenia, to trzeba się trochę oszykać.
[00:50:10 - 00:50:20] A nie każdy błąd da jebą erą, czerwone, tylko po prostu dziwne wyniki, no i wtedy trzeba komentować, wycinać, uszedam, lepszy pie jest czasami kliknąć, wcześniej nie ramy, zobaczysz.
[00:50:22 - 00:50:27] Dobra, co chcemy zrobić teraz? Sprawdź, czy termologi są na miejscu.
[00:50:57 - 00:51:03] To są te modifikatory, postaci gwiazdki i wygląda to następnie.
[00:51:08 - 00:51:12] Pamiętajcie, do bardzo ładnie odgwiazdkowany wykres termologii.
[00:51:13 - 00:51:15] Jak się wyłączymy?
[00:51:16 - 00:51:21] Dzień gotowski, trafiłem około 10-90% całej wysokości.
[00:51:24 - 00:51:29] 10% za jeden około, a tutaj coś tam jest do jedynki, no bo mieliśmy chyba włącznie na jeden.
[00:51:29 - 00:51:44] 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1
[00:51:45 - 00:51:52] A jakbyśmy na zalikaniu to całkiem jej ręcznie, wszystko, mamy znalezienia przed tych punktów 10-90%.
[00:51:53 - 00:51:55] A dobra, nie ma się tego.
[00:51:56 - 00:51:57] Na oko.
[00:51:57 - 00:51:59] To dobra, dobra.
[00:51:59 - 00:52:01] Czyli to trzy.
[00:52:01 - 00:52:03] Ja.
[00:52:03 - 00:52:09] A wie pan, może jak u panów terażowiskiego to wygląda, że wy to wyprzestawiasz?
[00:52:09 - 00:52:12] Ale co na cztery? Czy na więcej?
[00:52:12 - 00:52:14] Nie pisałem tego, nie wiem.
[00:52:14 - 00:52:16] A tak wysokosobnie?
[00:52:16 - 00:52:18] Tak, że mniej więcej, jak to powinienem wyprzestawić.
[00:52:18 - 00:52:20] Ja pisałem na dworze, nie wiem.
[00:52:20 - 00:52:22] Tak, chyba zespiega.
[00:52:22 - 00:52:25] Zakomentowajcie.
[00:52:53 - 00:52:55] Ciekawe, wyprzestawiamy sobie.
[00:52:55 - 00:52:57] No, ale nie pisałem tego.
[00:52:57 - 00:52:59] Czekaj, czekaj.
[00:52:59 - 00:53:02] Zobaczcie, o czym ja się robię, żeby czekać.
[00:53:02 - 00:53:05] Ja mam wkroki, tylko nie odzykac.
[00:53:05 - 00:53:07] Ja mam wkroki, tylko nie odzykac.
[00:53:07 - 00:53:09] Chodzą od tego czasu.
[00:53:09 - 00:53:11] Ja mam już nie wyprzestawiamy.
[00:53:11 - 00:53:13] Żeby nie obchodzić tego, to już słowo, i zaraz wróci.
[00:53:13 - 00:53:15] Teraz tak.
[00:53:15 - 00:53:17] Jak policzyć, zmucnienie, układu?
[00:53:17 - 00:53:20] No teraz poszczególujemy tak naprawdę osiącowanie naszego emocji.
[00:53:20 - 00:53:23] Można powiedzieć, że chodzi, jeżeli chodzi o identyfikację,
[00:53:23 - 00:53:25] o parametrów.
[00:53:25 - 00:53:28] Popatrzcie, materiały pomocnicze i nasza doprzynienie wygląda tak.
[00:53:28 - 00:53:30] Ma trzy parametrów.
[00:53:30 - 00:53:34] Raka obiektu, matę, czyli stały, czas zaoprowadzania.
[00:53:34 - 00:53:36] I ma stał, czyli opróźnienie.
[00:53:36 - 00:53:38] Trzy parametrów.
[00:53:38 - 00:53:40] Trzy musimy odnaleźć.
[00:53:40 - 00:53:42] I teraz ostatni punkt wyjścia do ostatnich punktu wejścia.
[00:53:42 - 00:53:44] Jakie by były dzienne?
[00:53:44 - 00:53:46] Które to przeprowywały?
[00:53:47 - 00:53:50] Wydaje się na skręcie.
[00:53:50 - 00:53:54] Jakie zmiany przechowują ostatnie punkty na wykresie?
[00:53:56 - 00:54:00] Te ostatnie punkty?
[00:54:00 - 00:54:04] Kikrytem.
[00:54:04 - 00:54:07] Oto przeprowywały te punkty.
[00:54:07 - 00:54:09] 107.
[00:54:09 - 00:54:11] No zobaczmy, tutaj jest 107.
[00:54:11 - 00:54:13] Kikrytem.
[00:54:14 - 00:54:17] No i nic, napisaliście, jakie są ostatnie punkty?
[00:54:17 - 00:54:19] Więc k to jest.
[00:54:19 - 00:54:21] Kikrytu.
[00:54:21 - 00:54:26] Duże T to jest.
[00:54:26 - 00:54:29] I teraz proszę, żebyście z tych materiałów pomocniczy.
[00:54:29 - 00:54:32] Nie mogę je wychać, ale tutaj.
[00:54:32 - 00:54:34] Napisali sami.
[00:54:34 - 00:54:36] O nie.
[00:54:47 - 00:54:50] Napiszmy już te linii.
[00:54:50 - 00:54:52] Czyli T to jest.
[00:54:52 - 00:54:55] Ten dziewięć minut, ten dziesięć minut przez dwa dwa.
[00:54:59 - 00:55:02] Dlaczego chcesz, żebyście sobie sami zrobili i w ten sposób?
[00:55:02 - 00:55:05] Bo tych linii nie powinniście zapamiętać,
[00:55:05 - 00:55:07] jak w prozna pamięć, tylko wziąć sobie z tego.
[00:55:07 - 00:55:09] Macie inny obiekt?
[00:55:09 - 00:55:12] Będzie trzeba i dacie napisać, więc nauczenie się czterech skryptów,
[00:55:12 - 00:55:15] a wtedy to, wtedy to...
[00:55:16 - 00:55:18] Tak jest.
[00:55:24 - 00:55:27] I właśnie chciałbym, żebyście przepisywali sobie z tego.
[00:55:33 - 00:55:36] 33,688,9.
[00:55:36 - 00:55:39] Jakie pytał ten dziewięciak?
[00:55:39 - 00:55:42] I teraz, jak już ktoś oblicze ten,
[00:55:42 - 00:55:44] którzy hamamy,
[00:55:44 - 00:55:46] napisałem wstłunie z wami,
[00:55:46 - 00:55:48] tylko jest takie samo.
[00:55:50 - 00:55:53] Ja podpisuję, to pakuje wytało.
[00:55:53 - 00:55:55] Ah, bardzo.
[00:55:55 - 00:55:58] Proszę, proszę, te ta.
[00:55:58 - 00:56:00] No, jak blisko.
[00:56:00 - 00:56:03] Tak, tak, tak.
[00:56:11 - 00:56:14] U, u, u.
[00:56:14 - 00:56:16] Chyba u, nie wiem.
[00:56:16 - 00:56:19] Ja bym chciał napisać na kora.
[00:56:19 - 00:56:21] No bo ty pamiętysz, jak się pojechał.
[00:56:21 - 00:56:23] A może tak, ale nie zaczniesz.
[00:56:23 - 00:56:26] Jak jest i u, to nie u, nie zaczniesz.
[00:56:26 - 00:56:28] A u, u, u.
[00:56:58 - 00:57:01] Chcecie, jak wiemy, czy to, to trzeba zadać w ten sposób.
[00:57:01 - 00:57:02] Pójdziecie grać?
[00:57:02 - 00:57:03] Nie.
[00:57:03 - 00:57:04] Dobra.
[00:57:04 - 00:57:05] Dobra.
[00:57:05 - 00:57:06] Dobra.
[00:57:06 - 00:57:07] Dobra.
[00:57:07 - 00:57:08] Dobra.
[00:57:08 - 00:57:09] Dobra.
[00:57:09 - 00:57:10] Dobra.
[00:57:10 - 00:57:11] Dobra.
[00:57:11 - 00:57:12] Dobra.
[00:57:12 - 00:57:13] Dobra.
[00:57:13 - 00:57:14] Dobra.
[00:57:14 - 00:57:15] Dobra.
[00:57:15 - 00:57:16] Dobra.
[00:57:16 - 00:57:17] Dobra.
[00:57:17 - 00:57:18] Dobra.
[00:57:18 - 00:57:19] Dobra.
[00:57:19 - 00:57:20] Dobra.
[00:57:20 - 00:57:21] Dobra.
[00:57:21 - 00:57:32] Dobra.
[00:57:32 - 00:57:35] Dobra.
[00:57:35 - 00:57:50] Dobra.
[00:57:50 - 00:57:55] i jeżeli tylko je spróbujemy zapamiętać.
[00:57:55 - 00:58:00] To jest wygadzierowanie transmitacji o opóźnienia.
[00:58:00 - 00:58:03] Lidnika ma zawsze wyglądacz padek.
[00:58:03 - 00:58:06] Licznik padek, wiadomo w nim padek,
[00:58:06 - 00:58:09] funkcja padek z opóźnieniem tału,
[00:58:09 - 00:58:11] czyli wiem, co wcześniej było,
[00:58:11 - 00:58:13] dwunastego żenu przybliżenie.
[00:58:13 - 00:58:16] Zapamiętujecie, czy tak zastosujecie.
[00:58:16 - 00:58:18] Jeżeli jest, to tak wygląda.
[00:58:19 - 00:58:21] Jeżeli chcecie sprzedam,
[00:58:21 - 00:58:24] nie trzeba tego kawałka skryptu robić,
[00:58:24 - 00:58:25] skrypcie.
[00:58:25 - 00:58:27] Mądra tracenych elementów,
[00:58:27 - 00:58:29] który, pod którego dorzymy,
[00:58:29 - 00:58:31] żeby wypełnić te sprawy,
[00:58:31 - 00:58:34] zrobić w cydoliku, jeżeli ktoś chce narysować,
[00:58:34 - 00:58:36] czy się wygrze zakłada,
[00:58:36 - 00:58:38] czy ta robina,
[00:58:38 - 00:58:40] można zrobić cydoliku,
[00:58:40 - 00:58:42] ale robię to skrypcem,
[00:58:42 - 00:58:44] jak widać, pamiętajcie,
[00:58:44 - 00:58:46] co myślę, że stanie się to jazdy.
[00:58:47 - 00:58:49] Nie, to podpisze.
[00:58:50 - 00:58:52] A to będzie intercja.
[00:58:53 - 00:58:57] Czyli licznik i nerw,
[00:58:57 - 00:58:59] a mianownik nerw,
[00:59:00 - 00:59:02] jak wygląda intercja od mianowników?
[00:59:09 - 00:59:11] I nerw,
[00:59:11 - 00:59:13] teraz kursienie.
[00:59:14 - 00:59:16] Czyli teraz kursienie.
[00:59:16 - 00:59:18] To jest wypowiedź,
[00:59:18 - 00:59:20] że są sami sprawy, które są w funkcie.
[00:59:22 - 00:59:24] Żeby połączyć kinięcy z okieniem,
[00:59:24 - 00:59:26] użyjemy takiej pozycji,
[00:59:26 - 00:59:28] jak w kące.
[00:59:46 - 00:59:48] To jest takie stworzenie,
[00:59:48 - 00:59:50] nawiązane w samym dziewczynku.
[00:59:50 - 00:59:52] Nie można napisać sobie,
[00:59:53 - 00:59:55] a nerw,
[00:59:55 - 00:59:57] z tego połączenia,
[00:59:57 - 00:59:59] do potęgi.
[01:00:00 - 01:00:02] To k, to miało być in?
[01:00:04 - 01:00:06] Nie, inf, to znaczy, że dzielę po prostu 0,
[01:00:06 - 01:00:08] bo tu jest 0,
[01:00:08 - 01:00:10] o to właśnie było,
[01:00:10 - 01:00:12] będzie mieć 0-0.
[01:00:12 - 01:00:20] Właśnie jest,
[01:00:20 - 01:00:22] jak tylko nie dam tego,
[01:00:22 - 01:00:24] to jest jedno.
[01:00:29 - 01:00:31] Okej,
[01:00:31 - 01:00:33] i to, co tutaj jest po tych wynikach,
[01:00:33 - 01:00:35] o tych wynikach,
[01:00:36 - 01:00:42] i ostatnio w wynikach,
[01:00:42 - 01:00:44] którego trwuję,
[01:00:44 - 01:00:46] model,
[01:00:46 - 01:00:48] czyli Helsing-Pittrick, model
[01:00:48 - 01:00:50] również funkcja Helsing-Pittrick,
[01:00:50 - 01:00:52] ona wykszata się,
[01:00:52 - 01:00:54] jeżeli nie ma całego czasu,
[01:00:54 - 01:00:56] czyli w ten sposób skarczy Wam,
[01:00:56 - 01:00:58] co regularnie jest,
[01:00:58 - 01:01:00] licznik,
[01:01:00 - 01:01:02] sterowanie
[01:01:02 - 01:01:04] czas przyjrzyjmy.
[01:01:04 - 01:01:06] Teraz przyjmujemy to,
[01:01:06 - 01:01:08] to wyszło,
[01:01:08 - 01:01:10] T, T,
[01:01:10 - 01:01:12] może,
[01:01:12 - 01:01:14] można sobie do góry?
[01:01:16 - 01:01:18] Está mi w hodowę dając.
[01:01:18 - 01:01:20] Wyspowałeś?
[01:01:20 - 01:01:22] Ja, tak, i tak.
[01:01:22 - 01:01:24] I jak?
[01:02:17 - 01:02:22] Zawsze, że nasza tradycja musi być idealne uzerowanie oryginalne.
[01:02:22 - 01:02:24] Bardzo, żeby była lepsza niż reszta.
[01:02:24 - 01:02:28] Co za uzerowanie pokażę, że jeżeli jest w imię, to będzie...
[01:02:32 - 01:02:38] Tak, to nic nie szkodzi. Ta droga użyta na początku, jest przyjmowalna.
[01:02:38 - 01:02:40] Nie ma to wpływu...
[01:02:41 - 01:02:45] ...z względu na to, że bardzo łatwo i tak przumowna policzyć.
[01:02:46 - 01:02:48] I teraz tak...
[01:02:49 - 01:02:51] ...pozupełnimy może...
[01:02:54 - 01:02:57] ...z jakich panów ten odkrywów będzie śledził?
[01:02:57 - 01:03:00] Opis i nerwcja ze okuźnieniem.
[01:03:00 - 01:03:04] Ja lubię pokazać ten po prostu mnie.
[01:03:04 - 01:03:08] Jak chcecie, możecie napisać na przykład na to, czy nie?
[01:03:08 - 01:03:09] Nie, nie życi.
[01:03:09 - 01:03:11] Bo ten człowiek mija też...
[01:03:12 - 01:03:17] Tak jest matematyczny, wyznaczony, paramentowy, transmitancji układu.
[01:03:17 - 01:03:23] Tutaj proszę, nie wzór, nie ten wzór, tak odkrywany, czyli kardelny.
[01:03:23 - 01:03:26] G od S równa księg.
[01:03:26 - 01:03:28] Jak jest tam?
[01:03:29 - 01:03:33] Chodzi jeszcze 1, 37.
[01:03:33 - 01:03:37] Jest reakcja to dobrze.
[01:03:38 - 01:03:40] Zacznę na miucie.
[01:03:41 - 01:03:45] To właśnie coś mi się nie daje, specjalnie to było ubracane tak.
[01:03:45 - 01:03:46] Przygotowane.
[01:03:46 - 01:03:48] No nie wiem, ale wyszło tak i...
[01:03:48 - 01:03:50] ...zawsze tak samo cieszę.
[01:03:50 - 01:03:52] Nie, nie...
[01:03:52 - 01:03:53] Wydziwie się.
[01:03:53 - 01:03:54] Przygotowałem.
[01:03:54 - 01:03:55] Przygotowałem.
[01:03:55 - 01:03:56] K2.
[01:03:56 - 01:03:58] S2 i 1.
[01:03:58 - 01:04:00] I jeszcze mamy tał, nie?
[01:04:00 - 01:04:01] Więc tam jest...
[01:04:01 - 01:04:03] ...ja nie wytworzę.
[01:04:03 - 01:04:05] E, tał, minutał.
[01:04:05 - 01:04:06] No to dobra.
[01:04:06 - 01:04:08] Teraz E...
[01:04:08 - 01:04:11] ...no potęgi, minutł i nał wyszło ile?
[01:04:11 - 01:04:15] I wyszło.
[01:04:15 - 01:04:20] 33,7.
[01:04:20 - 01:04:26] To jest transmitancja i proszę, że tak wyglądało do was.
[01:04:26 - 01:04:32] W tym nie jakieś inne rzeczy, tylko wasza transmitancja.
[01:04:32 - 01:04:35] Skąd skończę na pasz model, na uszło wypowiedź widać.
[01:04:35 - 01:04:39] Transfittancja zgadza się to już jest coś na dobrego drzewa, może na co.
[01:04:39 - 01:04:41] Tylko wszystkie kontyktury.
[01:04:41 - 01:04:44] Bornanie w elniku zarejestrowania odpowiedzi przyjętego modelu.
[01:04:44 - 01:04:47] To jest dokładnie to.
[01:04:47 - 01:04:50] Ja drobię sobie skirę wycika, ale wy po prostu...
[01:04:50 - 01:04:52] Ej, cześć.
[01:04:52 - 01:04:56] I...
[01:04:56 - 01:04:58] Teraz.
[01:04:58 - 01:05:01] Odgrupę jakoś dziennikaryzację.
[01:05:01 - 01:05:03] Jak byście to zainteresowali?
[01:05:03 - 01:05:06] Czyli różnica odpowiedzi rzeczywistego obiektu i modelu.
[01:05:06 - 01:05:08] Jak to zapisać?
[01:05:08 - 01:05:11] Przeglizy, co tego planu, a to wino się nie zbyt.
[01:05:11 - 01:05:14] Ale co wygad na całego grada?
[01:05:18 - 01:05:20] Zlecę nam sekret.
[01:05:20 - 01:05:22] Polskie teraz.
[01:05:22 - 01:05:23] Teraz.
[01:05:23 - 01:05:28] Drugi, trzeci, backstage.
[01:05:28 - 01:05:33] I jest kolejny punkt.
[01:05:33 - 01:05:35] Jak widać się pytam, dlaczego?
[01:05:35 - 01:05:38] Chciałem, żeby było więcej punktów, żeby...
[01:05:38 - 01:05:40] Tego, czy już byliście.
[01:05:40 - 01:05:44] Bo pierwszy proces jest tak umownie na okręci, na dwójkę.
[01:05:44 - 01:05:47] Już było dużo punktów na początku do podbierania.
[01:05:47 - 01:05:51] To jest taki wykres, który się robi bardzo.
[01:05:52 - 01:05:54] Także to...
[01:05:54 - 01:05:57] Pokażę konieczne, tylko...
[01:05:59 - 01:06:01] Może ja go zapiszę?
[01:06:01 - 01:06:12] Wreszcie sobie pod uwagę do decyzji.
[01:06:12 - 01:06:15] Nie zapamiętujemy te dwa procenty.
[01:06:15 - 01:06:18] Tu mógłby się to pisać.
[01:06:18 - 01:06:25] Tak, tylko te dwa ploty.
[01:06:25 - 01:06:30] I jeszcze chwilę.
[01:06:30 - 01:06:32] Co teraz mamy dalej?
[01:06:33 - 01:06:35] Takie już skrętowe.
[01:06:35 - 01:06:38] Jeżeli kość ma jeszcze jakieś pięć, dziesięć minut,
[01:06:38 - 01:06:42] to dochodzimy do korejku.
[01:06:42 - 01:06:44] Chodzimy do jaja.
[01:06:44 - 01:06:46] Naprawdę więcej tutaj już da.
[01:06:46 - 01:06:48] Nie trzeba, żeby dozyskać wyższą ocenę.
[01:06:48 - 01:06:50] Więc jeżeli chcieliby wiatki rową na tu...
[01:06:50 - 01:06:52] 40,5,
[01:06:52 - 01:06:54] to naprawdę wiele nie trzeba się narzucić.
[01:06:54 - 01:06:56] Zrób się tego regulatora.
[01:06:56 - 01:06:58] Hej, Dejna, pod oto dolejka.
[01:06:58 - 01:07:00] Tu jest fajny szalec.
[01:07:00 - 01:07:02] Otóż...
[01:07:03 - 01:07:05] Wyrobicie taki rzut.
[01:07:05 - 01:07:10] W którym punkcie jest to?
[01:07:10 - 01:07:11] Z rzutem?
[01:07:11 - 01:07:12] Z rzutem.
[01:07:12 - 01:07:13] Dobra.
[01:07:13 - 01:07:16] Kasia.
[01:07:16 - 01:07:19] Zadajcie punkt za to,
[01:07:19 - 01:07:21] że w tej liście rzut z materiałów możliwek,
[01:07:21 - 01:07:23] żeby widzicie liczyć w tym i następnym.
[01:07:23 - 01:07:29] Można najpierw to skleić, a po to robi z nią 1,2,3.
[01:07:29 - 01:07:31] Nie polecam.
[01:07:31 - 01:07:33] Dlatego, że jak tak liczę do momentu,
[01:07:33 - 01:07:35] w którym zakręczyliście pracę,
[01:07:35 - 01:07:37] to to jeżeli ktoś narysuje model,
[01:07:37 - 01:07:39] a nie policzył nastaw,
[01:07:39 - 01:07:41] to już się nie daje.
[01:07:41 - 01:07:43] Bo on nie jest zupełniony modelem.
[01:07:43 - 01:07:45] To, że jest screen tego modelu,
[01:07:45 - 01:07:47] nie znaczy, że może jest zupełniony to,
[01:07:47 - 01:07:49] że on nie ma, to nie działa.
[01:07:49 - 01:07:51] Tak, że jak ktoś to wieszka,
[01:07:51 - 01:07:53] punkty dalsze to tam zobaczy,
[01:07:53 - 01:07:55] teraz tak, wyznaczone na stały.
[01:07:55 - 01:07:57] Jak najpierw trzeba jeść na stały?
[01:07:57 - 01:07:59] O, tutaj, jeśli bo mi połówki i gór.
[01:07:59 - 01:08:01] Proszę, żebyście sami teraz zainteresowali.
[01:08:01 - 01:08:02] D.
[01:08:02 - 01:08:04] Na stały.
[01:08:04 - 01:08:06] W zeznacji, czyli 0,34 policzki,
[01:08:06 - 01:08:08] kaka i kaj.
[01:08:08 - 01:08:10] Dzieciak.
[01:08:10 - 01:08:12] Dzień dobry, dzień dobry.
[01:08:12 - 01:08:14] Proszę pamiętać, a ja będę nie połóżę,
[01:08:14 - 01:08:16] czy to, żebyśmy się tam nie znać.
[01:08:16 - 01:08:18] Bo...
[01:08:18 - 01:08:20] A ten wzór?
[01:08:20 - 01:08:22] Tak, tak, tak.
[01:08:22 - 01:08:24] Ani na butyn wzór.
[01:08:24 - 01:08:26] Dariusz się cztery.
[01:08:26 - 01:08:28] U nas jest ten słodzio.
[01:08:28 - 01:08:30] Jakie sam to w ogóle?
[01:08:30 - 01:08:32] 4,5,6,7.
[01:08:32 - 01:08:34] O, jak się to징.
[01:08:34 - 01:08:36] A ja zaqing mam.
[01:08:36 - 01:08:38] A, ja oj, ja oj.
[01:08:38 - 01:08:40] A w ogóle, a...
[01:08:40 - 01:08:42] A, w ogóle, oj...
[01:08:42 - 01:08:44] A, a ja oj.
[01:08:44 - 01:08:46] A, A, A, A, a...
[01:08:46 - 01:08:50] A, a, a, oj, ja oj.
[01:08:50 - 01:08:52] A, a, a, a, a, a, a.
[01:08:52 - 01:08:54] Na spoko moved...
[01:08:54 - 01:08:56] A, a, a, a, a, a, a, a, a,
[01:08:56 - 01:08:58] A, a, a, a, a, a, a...
[01:08:58 - 01:09:06] Mamy, mamy.
[01:09:06 - 01:09:14] Krabulamy, czyli materiał i pomocnicze egzamy.
[01:09:14 - 01:09:16] Teraz to samo.
[01:09:23 - 01:09:25] Coś tu jest, nie tak.
[01:09:30 - 01:09:33] Jeszcze nie wiem.
[01:09:33 - 01:09:35] Jeszcze nie wiem, co jest, nie tak.
[01:09:37 - 01:09:39] No, ja też nic nie daję.
[01:09:44 - 01:09:46] Kasi.
[01:09:46 - 01:09:48] Co to jest, kamer?
[01:09:48 - 01:09:49] To jest tutaj...
[01:09:49 - 01:09:50] To jest tutaj...
[01:09:50 - 01:09:51] To jest tutaj...
[01:09:51 - 01:09:52] To jest tutaj...
[01:09:52 - 01:09:53] To jest tutaj...
[01:09:53 - 01:09:54] To jest tutaj...
[01:09:54 - 01:09:56] To jest tutaj...
[01:11:55 - 01:12:00] Ja gdzieś, tylko z tym fakt, ja nie wiem, co jest, co jest.
[01:12:00 - 01:12:02] To jest tutaj...
[01:12:02 - 01:12:04] To jest tutaj...
[01:12:10 - 01:12:13] Wszystko jest niekogo życzne, bo rano jest, jest...
[01:12:13 - 01:12:15] Nie tak.
[01:12:15 - 01:12:17] To jest tutaj...
[01:12:17 - 01:12:18] To jest tutaj...
[01:12:18 - 01:12:19] To jest tutaj...
[01:12:19 - 01:12:20] To jest tutaj...
[01:12:20 - 01:12:21] To jest tutaj...
[01:12:21 - 01:12:22] To jest tutaj...
[01:12:23 - 01:12:25] To jest tutaj...
[01:12:28 - 01:12:31] To jest tutaj...
[01:12:31 - 01:12:32] To jest tutaj...
[01:12:48 - 01:12:50] To jest tutaj...
[01:12:50 - 01:12:52] Jak tam szkoda?
[01:12:52 - 01:12:54] Nie masz kajn?
[01:12:54 - 01:12:56] Nie masz!
[01:13:00 - 01:13:02] Działam dwie domu, dwóch tok.
[01:13:06 - 01:13:08] Tak zapisaliście?
[01:13:08 - 01:13:10] Dobrze, tak dobrze.
[01:13:10 - 01:13:12] To ma tak dobrze.
[01:13:12 - 01:13:14] Dalej.
[01:13:14 - 01:13:16] Nie, powodnik, tu nie są, czy nie?
[01:13:16 - 01:13:18] Tak.
[01:13:18 - 01:13:27] Pamiętajcie o nawiasach, bo tutaj często myslimy, a miastur jest błąd obliczeń, bo wtedy zostały ludzie wyczynników.
[01:13:27 - 01:13:38] Jeżeli to chcecie w ten sposób, żeby wziąć, bez nawiasów trzeba użyć takiego nawisów, jest inny niż taka człowiek, który się powiedzi, więc zachęcam, żeby używać nawiasów.
[01:13:39 - 01:13:51] KT6TI, a Wasze TI to jest inaczej T.
[01:13:51 - 01:13:53] Najwyższe maskeny w połowie.
[01:13:53 - 01:13:56] T, A, KT.
[01:13:56 - 01:13:58] Wydzisz? Wydzisz? Zastanawiam.
[01:13:58 - 01:14:00] Wyszło coś?
[01:14:00 - 01:14:02] I teraz tak.
[01:14:02 - 01:14:05] Wszystko trzeba poświęcić, żeby zostać w czterej kół.
[01:14:05 - 01:14:14] Otóż od tego momentu jesteśmy już w zapisie matematycznym i tutaj, jak wiecie, w dowództwie do końca macie 3 kół.
[01:14:14 - 01:14:17] W następnym jest macie 4.
[01:14:17 - 01:14:20] Zapis matematyczny, czyli wystarczony na stałe reguła w konie.
[01:14:20 - 01:14:22] Jakie małej kaffe to jest to.
[01:14:22 - 01:14:27] Możecie robić też na takim zasadzie, żeby k, p, u nas się wkleje.
[01:14:28 - 01:14:31] K i z.
[01:14:31 - 01:14:33] Muszę Cię wczoraj wyprzedeć.
[01:14:33 - 01:14:35] Muszę Cię wczoraj wyprzedeć.
[01:14:35 - 01:14:37] Wczoraj wyprzedeć.
[01:14:37 - 01:14:41] Proszę Pana, bym chciał Ci mówić o KI, gdzie będzie w tym pomocniczych.
[01:14:41 - 01:14:44] T i to jest T.
[01:14:44 - 01:14:47] K i to jest to.
[01:14:47 - 01:14:49] K i to jest T.
[01:14:49 - 01:14:51] To jest T.
[01:14:51 - 01:14:53] To zawsze.
[01:14:53 - 01:14:57] K i to jest T.
[01:14:57 - 01:14:59] K i to jest K.
[01:14:59 - 01:15:01] To jest K.
[01:15:01 - 01:15:03] K i to jest K.
[01:15:03 - 01:15:05] Rady T.
[01:15:05 - 01:15:08] Zazwyczaj macie 4.
[01:15:08 - 01:15:10] Nikt, które wojarą się z kluczynikami.
[01:15:10 - 01:15:13] To jest to, co jest w tej kartce.
[01:15:13 - 01:15:16] A nikt, które została, to została o poprowadzeniu.
[01:15:16 - 01:15:18] Przecież to nie będzie?
[01:15:18 - 01:15:20] Wtedy trzeba sobie smellsy.
[01:15:20 - 01:15:22] Na takie zasady, czyli jak...
[01:15:22 - 01:15:24] ...automaczki...
[01:15:24 - 01:15:26] ...wytrzał...
[01:15:26 - 01:15:28] ...to wyrzucał...
[01:15:28 - 01:15:30] ...dyszła w ten sposób...
[01:15:30 - 01:15:32] ...z cały smut, czyli kłopiejecie...
[01:15:32 - 01:15:34] ...konkrólcej...
[01:15:34 - 01:15:36] ...wyła, że zmieścicie.
[01:15:36 - 01:15:38] Wyła, że zmieścicie.
[01:15:38 - 01:15:40] To w pręcie wygrywa.
[01:15:40 - 01:15:42] Też jest ok.
[01:15:42 - 01:15:44] Czyli się w czołku wygrywa.
[01:15:44 - 01:15:46] To ma się pojawić tutaj.
[01:15:46 - 01:15:48] W tym czołku.
[01:15:49 - 01:15:50] Może w simuliku.
[01:15:50 - 01:15:52] I teraz chciałbym Wam pokazać, co...
[01:15:52 - 01:15:54] ...w tej...
[01:15:54 - 01:15:56] ...zachowienie, że zakończymy zaliczać.
[01:15:56 - 01:15:58] Kiedy się nie chciałbym opowiadać na pytania,
[01:15:58 - 01:16:00] ...wytrzał nie dostanie czasu.
[01:16:00 - 01:16:02] A nie...
[01:16:02 - 01:16:04] ...to...
[01:16:04 - 01:16:06] ...można...
[01:16:06 - 01:16:08] ...przestawać imię.
[01:16:08 - 01:16:10] Słucham się trochę, jak to doszło.
[01:16:10 - 01:16:12] I już pokazuję.
[01:16:12 - 01:16:14] Kąpliujemy sobie kaskanę.
[01:16:14 - 01:16:18] Tutaj idę.
[01:16:18 - 01:16:19] Doklariamy.
[01:16:19 - 01:16:21] Tutaj jemy w sumatoru.
[01:16:21 - 01:16:23] Myślę, że już nie powinienem być...
[01:16:23 - 01:16:25] ...jakieś...
[01:16:25 - 01:16:27] ...toszkakujące, bo zrobimy to wiele razy...
[01:16:27 - 01:16:29] ...na...
[01:16:29 - 01:16:31] ...zaboratoru.
[01:16:51 - 01:16:53] To jest wszystko.
[01:16:53 - 01:16:55] I teraz, zróbcie uwagi na wszystko.
[01:16:55 - 01:16:57] Zróbcie uwagi na wszystko.
[01:16:57 - 01:16:59] I jakaś okolicz bloczki.
[01:16:59 - 01:17:01] To będzie bloczek.
[01:17:01 - 01:17:03] To będzie bloczek, który...
[01:17:03 - 01:17:05] ...będzie miał jakąś wartość...
[01:17:05 - 01:17:07] ...zgodną z dokumentacją...
[01:17:07 - 01:17:09] ...i lepiej...
[01:17:09 - 01:17:11] 0,05.
[01:17:11 - 01:17:17] Tutaj będzie...
[01:17:17 - 01:17:19] 0,05 razy.
[01:17:19 - 01:17:21] Idziemy.
[01:17:21 - 01:17:23] OK?
[01:17:23 - 01:17:25] Zrobimy jakieś wymuszenie.
[01:17:25 - 01:17:27] Kiedy zarazował?
[01:17:27 - 01:17:29] Myślę, że tutaj 2 tysiące, ale to...
[01:17:29 - 01:17:31] ...dobro, żeby nie było w jednym momencie.
[01:17:32 - 01:17:34] To ma być kolejne wstaje 15 tutaj...
[01:17:34 - 01:17:36] ...szedł sumatorem.
[01:17:36 - 01:17:41] Bo to jest takie zazwyczaj dobre wymusienie.
[01:17:45 - 01:17:46] No właśnie nie.
[01:17:46 - 01:17:48] Popatrzcie, jak sterujecie w jakim samochodzie...
[01:17:48 - 01:17:50] ...to macie coś nie związanego z prędkością...
[01:17:50 - 01:17:52] ...i mi zyskujecie jakąś prędkość.
[01:17:52 - 01:17:54] Sterujecie czymś, co czujecie...
[01:17:54 - 01:17:56] ...jaką wypowiada w samochodzie...
[01:17:56 - 01:17:58] ...i dodajcie prędkość.
[01:17:58 - 01:18:00] Zostajecie pępoma, to nie sterujecie już czymś...
[01:18:00 - 01:18:02] ...małgienany.
[01:18:03 - 01:18:04] 120.
[01:18:04 - 01:18:06] Czyli sterujemy tym, co chce.
[01:18:06 - 01:18:08] Obserwować.
[01:18:10 - 01:18:12] Czyli czym sterujemy?
[01:18:12 - 01:18:14] Wysokością wody, więc teraz...
[01:18:14 - 01:18:16] ...takich rzeczach pojawią się...
[01:18:16 - 01:18:18] ...tu zniszczy.
[01:18:18 - 01:18:20] Już ten prędkość.
[01:18:20 - 01:18:22] Bo sterujemy...
[01:18:22 - 01:18:24] ...tak jak...
[01:18:24 - 01:18:26] ...zplanowali.
[01:18:26 - 01:18:28] 5.1 razy 1.1
[01:18:28 - 01:18:30] No bo...
[01:18:30 - 01:18:34] ...i tutaj...
[01:18:34 - 01:18:36] ...a tutaj zmieniamy pęki...
[01:18:36 - 01:18:38] ...na pęki, bo tak mówimy nam...
[01:18:38 - 01:18:40] ...pędkość na materiałek...
[01:18:40 - 01:18:42] ...przei...
[01:18:42 - 01:18:44] ...na stawę regulatora...
[01:18:44 - 01:18:46] ...kfc...
[01:18:46 - 01:18:48] ...i...
[01:18:48 - 01:18:50] ...przepisujemy w ten sposób.
[01:18:50 - 01:18:52] Mamy, jedno tamie...
[01:18:52 - 01:18:54] ...i ma sensu sobie tego wyzwować.
[01:18:54 - 01:18:56] Wszystko jest...
[01:18:56 - 01:18:59] ...ruka miany...
[01:18:59 - 01:19:03] ...pojawia się na top.
[01:19:03 - 01:19:05] Aż na pokolei wszystko pokazuje się.
[01:19:05 - 01:19:07] Teraz...
[01:19:07 - 01:19:09] ...ja byłam, chciałem tylko zakończyć etap...
[01:19:09 - 01:19:11] ...i ten skrzyn...
[01:19:11 - 01:19:13] ...wyja, czy to jest dobre, czy jest głyb...
[01:19:13 - 01:19:15] ...i...
[01:19:15 - 01:19:17] ...poza powiedź, że jesteśmy...
[01:19:17 - 01:19:19] ...na wyłacze dla 4.5...
[01:19:19 - 01:19:21] ...ja jest dla uperkwentnych...
[01:19:21 - 01:19:23] ...którzy czują bardzo temat tych rezywatorów...
[01:19:23 - 01:19:25] ...sobo pisać...
[01:19:25 - 01:19:27] ...przed nimi byłoby...
[01:19:27 - 01:19:29] ...dobrze się stanowili...
[01:19:29 - 01:19:31] ...przeliczą przerobowanie...
[01:19:31 - 01:19:33] ...to jest kwestia tylko...
[01:19:33 - 01:19:35] ...jak czujecie temat tego bliskiego...
[01:19:35 - 01:19:37] ...chcecie tego...
[01:19:37 - 01:19:39] ...odowalcie do przemiany.
[01:19:39 - 01:19:41] Iż wyjaźnię...
[01:19:41 - 01:19:43] ...ten model wygląda praktycznie...
[01:19:43 - 01:19:45] ...tak jak ten poprzedni...
[01:19:45 - 01:19:47] ...tych podeszedztw...
[01:19:47 - 01:19:49] ...dla tego, że w ciałe...
[01:19:49 - 01:19:51] ...i wprowadzić zakłócenie do układu...
[01:19:51 - 01:19:53] ...ale w innym momencie...
[01:19:53 - 01:19:55] ...niż...
[01:19:55 - 01:19:57] ...przepisamy...
[01:19:57 - 01:19:59] ...przepisamy...
[01:19:59 - 01:20:01] ...a ten rekres...
[01:20:01 - 01:20:03] ...bymy te ruch�ypienia tylko i wyłącznie...
[01:20:03 - 01:20:05] ...bo ten...
[01:20:05 - 01:20:07] ...że naród z podrówną...
[01:20:07 - 01:20:09] ...słabiliśmy jako raniu sobie...
[01:20:09 - 01:20:11] ...zupuszamy...
[01:20:11 - 01:20:13] ...wyszamy...
[01:20:13 - 01:20:15] ...bym rysował...
[01:20:15 - 01:20:17] ...to będzie kiedy jedziemy na przykład w hulkę...
[01:20:17 - 01:20:19] ...cinak jest parło...
[01:20:19 - 01:20:21] ...i przyspieszamy...
[01:20:21 - 01:20:23] ...to to będzie...
[01:20:23 - 01:20:25] ...zobaczmy...
[01:20:25 - 01:20:27] ...dobaczmy...
[01:20:27 - 01:20:29] ...począć sprzęt...
[01:20:29 - 01:20:31] ...mówiłem...
[01:20:31 - 01:20:33] ...tych podeszedztw...
[01:20:33 - 01:20:35] ...to zimno obry…
[01:20:35 - 01:20:37] ...to jest...
[01:20:37 - 01:20:39] ...na po 4,5...
[01:20:39 - 01:20:41] ...tak naprawdę...
[01:20:41 - 01:20:43] ...tyle...
[01:20:43 - 01:20:45] ...tyle...
[01:20:45 - 01:20:47] ...a ten ruch...
[01:20:47 - 01:20:49] ...to takim w porządku...
[01:20:49 - 01:20:51] ...pytanie, macie ten...
[01:20:51 - 01:20:53] ...gober...
[01:20:53 - 01:20:55] ...przed nami...
[01:20:55 - 01:21:05] Wiem, która nie wszyscy to dnożyłem zrobić, tylko wstawiasz.
[01:21:56 - 01:22:01] Ja w ten sposób tylko chciałbym ci dochycić do przepisania tego obkodu, chociaż raz.
[01:22:02 - 01:22:04] Bardzo.
[01:22:05 - 01:22:08] Tu jest, czy nie?
[01:22:13 - 01:22:20] Mam pan tak szeroko, tworzymy ten zawór, że wylewa się woda w lewa i matka po prostu śledzi ci próbki.
[01:22:25 - 01:22:28] Nie dana, nie dala.
[01:22:55 - 01:22:57] Wydaje mi się, czy ma.
[01:22:57 - 01:22:59] O, pani Kajsty.
[01:23:01 - 01:23:03] Kajsty?
[01:23:03 - 01:23:05] Kto miał pani Kajsty?
[01:23:05 - 01:23:07] To był.
[01:23:07 - 01:23:09] To był.
[01:23:09 - 01:23:11] Ile?
[01:23:11 - 01:23:13] Ile?
[01:23:13 - 01:23:15] Jak będzie pani Kajsty?
[01:23:15 - 01:23:17] Jak będzie pani Kajsty?
[01:23:17 - 01:23:19] Jak będzie pani Kajsty?
[01:23:19 - 01:23:21] Jak będzie pani Kajsty?
[01:23:21 - 01:23:23] No teraz.
[01:23:26 - 01:23:28] Ile się działa ci?
[01:23:28 - 01:23:31] Nie, bo ten korzy pełnialiśmy.
[01:23:31 - 01:23:34] Chodzi o to, że powolnie.
[01:23:34 - 01:23:38] Właśnie to, że wszyscy odwołniają się.
[01:23:38 - 01:23:40] A potem to odwiedźmy.
[01:23:40 - 01:23:42] Zobaczcie.
[01:23:42 - 01:23:44] Zobaczcie.
[01:23:44 - 01:23:46] Zobaczcie.
[01:23:46 - 01:23:49] Zobaczcie.
[01:23:49 - 01:23:51] Zobaczcie.
[01:23:51 - 01:23:55] Zobaczcie.
[01:23:55 - 01:23:58] Zobaczcie.
[01:23:58 - 01:24:01] Zobaczcie.
[01:24:01 - 01:24:04] Zobaczcie.
[01:24:04 - 01:24:07] Zobaczcie.
[01:24:07 - 01:24:10] Zobaczcie.
[01:24:10 - 01:24:15] Podoba mi się.
[01:24:15 - 01:24:18] Pamiętaj o to, że nie wolna im się pojaźnić.
[01:24:18 - 01:24:21] Zobaczcie.
[01:24:51 - 01:24:57] Ja bym chciał polić kamień, ale byłbym chłopakiem.
[01:24:57 - 01:25:02] 261, 316, 314, 0, 0, 0.
[01:25:02 - 01:25:03] Dzień dobry.
[01:25:03 - 01:25:04] Dzień dobry.
[01:25:04 - 01:25:05] Dzień dobry.
[01:25:05 - 01:25:07] Dzień dobry.
```
