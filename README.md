# Laboratorium 00 — Git, GitHub i środowisko pracy

**Programowanie obiektowe · 2026/2027**

## Po co ta praca?

Przygotujesz środowisko do kolejnych laboratoriów i poznasz sposób pracy używany na kursie w **Classroom 50**.

Przećwiczysz:

- przyjęcie zadania w Classroom 50;
- sklonowanie własnego repozytorium;
- lokalną zmianę kodu;
- `git status`, `diff`, `add`, `commit`, `push` i `pull`;
- pracę w osobnej gałęzi;
- tworzenie i scalanie Pull Request;
- uruchamianie GitHub Actions;
- analizę błędu kompilacji.

Uruchomisz również gotowe programy w **C++** i **Java**.

Nie implementujesz jeszcze klas ani testów. Nie musisz znać OOP. Gotowe programy służą do sprawdzenia narzędzi oraz całego workflow Git/GitHub.

**Forma:** indywidualna  
**Ocena:** zaliczono / nie zaliczono  
**Czas:** około 90 minut przy zainstalowanych narzędziach  
**Oddanie:** przez repozytorium utworzone dla Ciebie przez Classroom 50

Po ukończeniu laboratorium potrafisz:

- odróżnić Git od GitHub;
- odróżnić repozytorium lokalne od zdalnego;
- wyjaśnić rolę Classroom 50 i repozytorium szablonowego;
- wykonać `clone`, `status`, `diff`, `add`, `commit`, `push` i `pull`;
- utworzyć gałąź;
- utworzyć i scalić Pull Request;
- uruchomić program C++ i Java;
- znaleźć błąd w logu GitHub Actions;
- wyjaśnić, dlaczego `commit` nie wysyła automatycznie zmian na GitHub.

> **WAŻNE**
>
> Nie twórz własnego repozytorium przyciskiem **Use this template** i nie pracuj bezpośrednio w repozytorium szablonowym prowadzącego.
>
> Po zaakceptowaniu zadania **Classroom 50 automatycznie tworzy Twoje indywidualne repozytorium**. Całą pracę wykonujesz właśnie w tym repozytorium.

---

# 1. Przygotowanie narzędzi

Potrzebujesz:

- konta GitHub;
- Git;
- **JDK 17 lub nowszego** — nie tylko JRE;
- kompilatora **g++ obsługującego C++17**;
- edytora lub IDE.

## Windows

Zalecana konfiguracja:

**WSL + Ubuntu + edytor obsługujący WSL**

Jeżeli masz już działające JDK i `g++` w Windows, możesz również użyć PowerShell.

Samo Visual Studio z kompilatorem MSVC nie zapewnia polecenia `g++`.

### Ubuntu / WSL Ubuntu

Jeżeli narzędzi brakuje:

```bash
sudo apt update
sudo apt install git g++ openjdk-17-jdk
```

### Windows bez WSL

Zainstaluj:

- Git for Windows;
- Temurin JDK 17+;
- `g++`, np. przez MSYS2.

Po instalacji otwórz nowy terminal.

### macOS

Zainstaluj Git, JDK 17+ oraz kompilator C++17.

Systemowe polecenie `g++` może uruchamiać Apple Clang — dla tej pracy jest to wystarczające.

## Sprawdzenie narzędzi

W terminalu wykonaj:

```bash
git --version
g++ --version
java -version
javac -version
```

Każde polecenie powinno wypisać wersję programu.

Jeżeli `java` działa, ale `javac` nie, sprawdź instalację **JDK** i konfigurację `PATH`.

Używaj tego samego środowiska do klonowania repozytorium i kompilowania programu.

## Konfiguracja autora commitów

Jeżeli jeszcze tego nie zrobiłeś/aś:

```bash
git config --global user.name "Twoja nazwa autora"
git config --global user.email "TWÓJ_EMAIL_DO_COMMITÓW"
```

Możesz użyć adresu `noreply` dostępnego w:

**GitHub → Settings → Emails**

Jest to identyfikacja autora commita, a nie sposób logowania do GitHub.

---

# 2. Krótki słownik

| Pojęcie | Znaczenie |
|---|---|
| Git | lokalny system kontroli wersji |
| GitHub | serwis przechowujący repozytoria i narzędzia współpracy |
| Classroom 50 | system dystrybucji zadań i zbierania pracy studentów oparty na GitHub |
| Template repository | repozytorium wzorcowe przygotowane przez prowadzącego |
| Student repository | indywidualne repozytorium utworzone dla studenta po zaakceptowaniu assignmentu |
| Clone | pobranie repozytorium wraz z historią na komputer |
| Working tree | pliki, które aktualnie edytujesz |
| Stage / `git add` | wybór zmian do następnego commita |
| Commit | zapis wybranych zmian w lokalnej historii |
| Push | wysłanie lokalnych commitów do repozytorium zdalnego |
| Pull | pobranie i włączenie zmian ze zdalnego repozytorium |
| Branch | osobna linia pracy |
| Pull Request (PR) | propozycja włączenia zmian z jednej gałęzi do drugiej |
| Merge | scalenie zmian |
| GitHub Actions | automatyczne wykonywanie zadań, np. kompilacji |

Zapamiętaj:

**`commit` ≠ `push`**

oraz

**Pull Request ≠ `git pull`**

---

# Zadanie 1 — Przyjęcie zadania i własne repozytorium

## Krok 1. Przyjmij zadanie w Classroom 50

1. Otwórz link **Accept assignment** otrzymany od prowadzącego.
2. Zaloguj się do właściwego konta GitHub, jeżeli jest to wymagane.
3. Zaakceptuj zadanie.
4. Poczekaj, aż Classroom 50 przygotuje Twoje repozytorium.
5. Otwórz repozytorium przypisane do Ciebie.

Classroom 50 tworzy repozytorium na podstawie szablonu przygotowanego przez prowadzącego.

Nie musisz tworzyć własnej kopii szablonu.

> **Nie wykonuj:**
>
> `Use this template → Create a new repository`
>
> Nie rób również forka repozytorium szablonowego.
>
> Tak utworzone repozytorium **nie jest repozytorium przypisanym do Twojego zadania w Classroom 50**.

## Krok 2. Sklonuj swoje repozytorium

W repozytorium utworzonym dla Ciebie kliknij:

**Code → HTTPS**

i skopiuj URL.

Następnie w terminalu:

```bash
git clone <HTTPS_URL_TWOJEGO_REPOZYTORIUM>
cd <NAZWA_KATALOGU>
git remote -v
git status
```

Zastąp wartości `<...>` rzeczywistymi wartościami.

Polecenie:

```bash
git remote -v
```

powinno pokazać, że `origin` wskazuje na **Twoje repozytorium zadania utworzone przez Classroom 50**.

Nie powinno wskazywać na:

```text
put-teaching-2026-27/oop-lab00-template
```

Nie używaj **Download ZIP** jako sposobu pracy nad zadaniem. Potrzebujemy lokalnej historii Git oraz połączenia ze zdalnym repozytorium.

Otwórz sklonowany katalog w IDE.

Nie twórz nowego projektu poza tym katalogiem.

Pliki źródłowe znajdują się w:

```text
cpp/
java/
```

Przy pierwszym `clone` lub `push` może pojawić się logowanie do GitHub.

Nie zapisuj tokenów ani danych uwierzytelniających w repozytorium.

---

# Zadanie 2 — Gałąź i lokalne uruchomienie

Utwórz gałąź roboczą:

```bash
git switch -c lab00-setup
```

Sprawdź:

```bash
git branch
```

Przy aktywnej gałęzi powinien znajdować się znak `*`.

## Linux / WSL / macOS

Z katalogu głównego repozytorium:

```bash
mkdir -p build/cpp build/java

g++ -std=c++17 -Wall -Wextra -Wpedantic cpp/main.cpp -o build/cpp/hello
./build/cpp/hello

javac -encoding UTF-8 -d build/java java/Main.java
java -cp build/java Main
```

## Windows PowerShell

```powershell
New-Item -ItemType Directory -Force -Path build/cpp, build/java

g++ -std=c++17 -Wall -Wextra -Wpedantic cpp/main.cpp -o build/cpp/hello.exe
./build/cpp/hello.exe

javac -encoding UTF-8 -d build/java java/Main.java
java -cp build/java Main
```

Oczekiwane wyniki:

```text
Hello from C++!
Hello from Java!
```

Katalog:

```text
build/
```

przechowuje pliki wynikowe.

`.gitignore` powinien sprawić, że pliki binarne i `.class` nie zostaną dodane do repozytorium.

Sprawdź:

```bash
git status
```

---

# Zadanie 3 — Zmiana, diff, commit i push

## 1. Zmień programy

Zmień tekst wypisywany przez oba programy.

Przykład:

```text
Hello from C++! Author: student123
```

oraz analogicznie w Java.

Użyj swojego loginu GitHub lub pseudonimu.

## 2. Uruchom programy ponownie

Skompiluj i uruchom oba programy.

Sprawdź, czy pojawia się zmieniony komunikat.

## 3. Uzupełnij STUDENT.md

Uzupełnij plik:

```text
STUDENT.md
```

Wpisz wymagane informacje dotyczące środowiska, wersji narzędzi i wykonanych ćwiczeń.

Nie potrzebujesz osobnego sprawozdania.

## 4. Sprawdź zmiany

```bash
git status
git diff
```

Następnie:

```bash
git add cpp/main.cpp java/Main.java STUDENT.md
```

Sprawdź staged changes:

```bash
git diff --staged
```

Wykonaj commit:

```bash
git commit -m "Personalize programs and document local setup"
```

Wyślij gałąź na GitHub:

```bash
git push -u origin lab00-setup
```

## 5. Sprawdź GitHub

Otwórz swoje repozytorium w GitHub.

Sprawdź, czy:

- istnieje gałąź `lab00-setup`;
- widoczny jest Twój commit;
- zmienione pliki znajdują się w repozytorium.

> Classroom 50 może zebrać tylko pracę znajdującą się w repozytorium GitHub.
>
> Sam lokalny `commit` bez `push` nie wysyła zmian na GitHub.

---

# Zadanie 4 — Pull Request i automatyczna kontrola

Na GitHub otwórz:

**Pull requests → New pull request**

lub użyj:

**Compare & pull request**

Ustaw:

```text
base: main
compare: lab00-setup
```

Obie gałęzie mają należeć do **Twojego repozytorium Classroom 50**.

Nie otwieraj Pull Request do repozytorium szablonowego prowadzącego.

## Pull Request

Tytuł:

```text
Lab00: przygotowanie środowiska
```

W opisie napisz:

- które pliki zmieniłeś/aś;
- czy oba programy działają lokalnie;
- czy wystąpił problem;
- jeśli tak — jak został rozwiązany.

Sprawdź zakładkę:

**Files changed**

Następnie sprawdź wyniki **GitHub Actions / Checks**.

Zielony wynik oznacza, że kod przeszedł skonfigurowaną automatyczną kontrolę.

Nie oznacza to automatycznie, że wykonano wszystkie wymagania laboratorium.

## Merge

Po udanej kontroli scal PR:

**Merge pull request → Confirm merge**

Następnie lokalnie:

```bash
git switch main
git pull --ff-only origin main
```

Sprawdź:

```bash
git status
git log --oneline -5
```

Twój lokalny `main` powinien zawierać zmiany scalone na GitHub.

---

# Zadanie 5 — Rozpoznanie i poprawienie błędu

Z aktualnej gałęzi `main` utwórz nową gałąź:

```bash
git switch -c lab00-debug
```

## 1. Wprowadź celowy błąd

W:

```text
cpp/main.cpp
```

usuń średnik na końcu instrukcji wypisującej tekst.

Spróbuj skompilować program.

Przeczytaj komunikat błędu.

## 2. Zapisz błędną wersję

```bash
git add cpp/main.cpp
git commit -m "Exercise: introduce a compilation error"
git push -u origin lab00-debug
```

## 3. Sprawdź GitHub Actions

Na GitHub otwórz wynik Actions dla tego commita.

Znajdź:

- nieudany krok;
- komunikat kompilatora;
- numer linii zawierającej błąd.

**Czerwony wynik jest w tym kroku oczekiwany.**

Nie traktuj czerwonego wyniku tego ćwiczenia jako problemu — celem jest nauczenie się czytania logów CI.

## 4. Napraw program

Przywróć średnik.

Ponownie skompiluj i uruchom program lokalnie.

## 5. Uzupełnij STUDENT.md

Wpisz:

- komunikat błędu;
- przyczynę błędu;
- sposób naprawy;
- link do pierwszego PR;
- krótką odpowiedź: co potwierdza GitHub Actions, a czego nie potwierdza?

## 6. Zapisz poprawkę

```bash
git add cpp/main.cpp STUDENT.md
git commit -m "Fix compilation error and complete Lab00 notes"
git push
```

## 7. Utwórz drugi Pull Request

Utwórz:

```text
lab00-debug → main
```

Poczekaj na poprawny wynik automatycznej kontroli.

Następnie scal PR.

## 8. Zsynchronizuj lokalne repozytorium

```bash
git switch main
git pull --ff-only origin main
git status
git log --oneline -5
```

Nie scalaj celowo błędnego kodu do `main`.

Historia gałęzi powinna pokazywać zarówno commit zawierający błąd, jak i commit zawierający poprawkę.

---

# Zadanie 6 — Oddanie pracy w Classroom 50

**Nie tworzysz osobnego repozytorium do oddania.**

**Nie dodajesz prowadzącego jako Collaboratora.**

**Nie wysyłasz osobno repozytorium utworzonego poza Classroom 50.**

Twoim repozytorium submission jest repozytorium utworzone automatycznie po zaakceptowaniu assignmentu w Classroom 50.

## Przed zakończeniem pracy

Wykonaj:

```bash
git switch main
git pull --ff-only origin main
git status
git log --oneline -5
```

`git status` powinien pokazać czyste working tree.

Następnie otwórz repozytorium na GitHub i sprawdź, czy:

- oba Pull Request zostały scalone do `main`;
- `STUDENT.md` jest uzupełniony;
- finalny kod znajduje się na `main`;
- finalny wymagany workflow GitHub Actions zakończył się poprawnie.

Classroom 50 zbiera informacje o pracy z przypisanego Ci repozytorium.

**Nie wysyłaj prowadzącemu dodatkowego linku do repozytorium, chyba że zostaniesz o to poproszony/a.**

---

# Lista kontrolna przed zakończeniem

- [ ] Zaakceptowałem/am assignment przez Classroom 50.
- [ ] Pracuję w repozytorium utworzonym dla mnie przez Classroom 50.
- [ ] Nie utworzyłem/am własnego repozytorium przez `Use this template`.
- [ ] Sklonowałem/am właściwe repozytorium lokalnie.
- [ ] `origin` wskazuje na moje repozytorium zadania.
- [ ] Oba programy uruchomiłem/am lokalnie.
- [ ] Zmieniłem/am komunikaty w C++ i Java.
- [ ] `STUDENT.md` jest uzupełniony.
- [ ] Pierwszy PR `lab00-setup → main` został scalony.
- [ ] W historii znajduje się ćwiczenie z błędem kompilacji i jego poprawką.
- [ ] Drugi PR `lab00-debug → main` został scalony.
- [ ] Finalna wersja znajduje się na `main`.
- [ ] Lokalny `main` jest zsynchronizowany z GitHub.
- [ ] Finalne GitHub Actions są zielone.

---

# Krótka obrona

Przygotuj się do pokazania repozytorium oraz uruchomienia programów.

Możesz otrzymać pytania:

1. Czym różni się Git od GitHub?
2. Czym różni się `commit` od `push`?
3. Co robi `git add`?
4. Co oznacza `origin`?
5. Dlaczego po scaleniu PR na GitHub wykonujemy lokalnie `git pull`?
6. Czym różni się branch od oddzielnego repozytorium?
7. Co sprawdza GitHub Actions, a czego nie sprawdza?
8. Jaką rolę pełni Classroom 50?
9. Jaka jest różnica między template repository a Twoim student repository?

---

# Kryterium zaliczenia

Zaliczenie wymaga:

- pracy we właściwym repozytorium Classroom 50;
- działających programów C++ i Java;
- zmian wysłanych na GitHub;
- poprawnej historii Git;
- wykonania ćwiczeń z branchami;
- wykonania Pull Request;
- przeanalizowania celowego błędu kompilacji;
- uzupełnionego `STUDENT.md`;
- finalnej poprawnej wersji na `main`;
- umiejętności wyjaśnienia podstawowego workflow Git/GitHub.

---

# Schemat pracy

```text
Classroom 50
      ↓
Accept assignment
      ↓
indywidualne student repository
      ↓
git clone
      ↓
branch
      ↓
edit → compile → test
      ↓
git add → commit → push
      ↓
Pull Request
      ↓
GitHub Actions
      ↓
merge do main
      ↓
git pull
      ↓
Classroom 50 zbiera submission
```

Ten sam podstawowy model pracy będzie używany w kolejnych laboratoriach.
