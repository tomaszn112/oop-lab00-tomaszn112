# Moje wykonanie Lab00

- Login GitHub / pseudonim: tomaszn112
- System i terminal (np. Windows + WSL Ubuntu): Windows + WSL Ubuntu
- Edytor / IDE: Visual Studio Code
- Wersja Git: 2.43.0
- Wersja kompilatora C++: 13.3.0
- Wersje java i javac: 17.0.20.1
- Link do pierwszego PR (uzupełnij w zadaniu 5): https://github.com/tomaszn112/oop-lab00-tomaszn112/pull/1

## Uruchomienie lokalne
Wynik programu C++:
```
Hello from C++! Author: tomaszn112
```
Wynik programu Java:
```
Hello from Java! Author: tomaszn112
```

## Błąd i poprawka (zadanie 5)
- Krótki fragment komunikatu błędu i numer linii: error: expected ';' before 'return' (linia 5)
- Przyczyna oraz sposób naprawy: Brak średnika na końcu instrukcji std::cout. Naprawa: dodanie średnika.
- Commit z błędem (SHA lub link): https://github.com/tomaszn112/oop-lab00-tomaszn112/commit/39369d3819557b6488f370409abfbe8af6f81ffe
- Czy Actions pokazały błąd, a po naprawie sukces? Tak, Actions zatrzymały się na czerwonym błędzie kompilacji, a po naprawie zakończyły się zielonym sukcesem.

## Krótkie odpowiedzi
1. Co różni commit od push? Commit zapisuje zmiany wyłącznie lokalnie na komputerze (Git), natomiast push wysyła te zmiany do zdalnego repozytorium (np. na GitHub). 
2. Dlaczego po scaleniu PR wykonuję lokalnie pull? Polecenie merge zachodzi zdalnie na serwerze GitHub. Dlatego musimy wykonać pull, aby zsynchronizować nsze lokalne pliki na komputerze ze zmianami z repozytorium zdalnego na GitHubie.
3. Co potwierdza zielony wynik naszego CI, a czego nie potwierdza? Potwierdza, że kod poprawnie kompiluje się w środowisku automatycznym (na maszynie wirtualnej), nie potwierdza natomiast poprawnej konfiguracji na lokalnym komputerze ani kompletności wykonania wszystkich poleceń / zadań. 

## Ewentualne problemy środowiska
Brak / opis problemu i sposób rozwiązania: Problem z uwierzytelnianiem przy git push. Rozwiązano poprzez wygenerowanie i użycie tokenu PAT.
