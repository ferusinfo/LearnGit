#Git - wprowadzenie

## Informacje ogólne

Ten kurs powstał z potrzeby wytłumaczenia jak korzystać z tego Git'a dla osób które mają problemy ze zrozumieniem jak z niego korzystać podczas gdy uczą się z poradników w języku angielskim.

Wszelkie propozycje/opinie na temat kursu wprowadzającego są bardzo mile widziane - wystarczy, że skontaktujecie się ze mną poprzez maila: <mailto:kontakt@ferus.info> lub [@ferusinfo](http://twitter.com/ferusinfo).

Nie wykluczam dodatkowych częsci tego poradnika które obejmowałyby bardziej zaawansowane aspekty korzystania z Git'a takie jak *branching*.

Wszelkie poprawki do kodu możecie również umieszczać otwierając [issue](https://github.com/ferusinfo/LearnGit/issues) dla tego repozytorium.

##Proste zarządzanie swoim projektem w rozproszonym systemie kontroli wersji

*Git* jest prostym do opanowania systemem kontroli wersji - dzieki niemu jestesmy w stanie zarzadzac zmianami w naszym projekcie - m.in. sledzic zmiany poszczególnych linii kodu. Dzięki wykorzystaniu zdalnych repozytoriów mamy mozliwość współdzielenia naszego projektu z innymi programistami, co może pozwolić im na wprowadzanie własnych poprawek lub zgłaszanie korekt do już istniejącego kodu.

# Jak zacząc korzystać?

W zależności od systemu operacyjnego korzystanie z *Git'a* możemy zacząć na różne sposoby. Najgorzej chyba w chwili obecnej mają użytkownicy Windowsa, którzy muszą instalować specjalną nakładkę na terminal systemowy. Jeśli jednak korzystamy z innych systemów, możemy skorzystać z Git'a praktycznie od razu.

Aby dowiedzieć się jak zainstalować Gita na konkretnych systemach, sprawdź plik INSTALL.MD znajdujący się w tym repozytorium (w trakcie tworzenia).

Duża część z repozytoriów zdalnych gdzie możemy utrzymywać nasz kod wymaga autoryzacji po kluczach SSH - więcej na ten temat można przeczytać m.in. [na stronie pomocy GitHub'a](https://help.github.com/articles/generating-ssh-keys)

## Pierwsze kroki
Jeśli jesteśmy użytkownikami Linuxa lub MacOS, w większości przypadków Git będzie już zainstalowany w naszym systemie.
Aby sprawdzić, czy go posiadamy wystarczy, że wpiszemy komendę:

`git --version`

Jeśli naszym oczom ukaże się coś podobnego do ciągu znaków które widoczne są poniżej, to znaczy, że możemy rozpocząć pracę a Git jest już zainstalowany.

`git version 1.7.10.2 (Apple Git-33)`

## Przedstaw się!

Ważną kwestią w Gicie jest poprawne jego skonfigurowanie, toteż na samym początku musimy wykonać poniższe komendy.

```
git config -l
git config --global user.name "Imie i Nazwisko / Nick"
git config --global user.email "email@domena.pl"
```

## Inicjalizacja projektu

Załóżmy, że nasz projekt, napisany w języku PHP składa się (póki co) z katalogu, który znajduje się w naszym katalogu ze stronami i chcemy zacząć go wersjonować.

Dla celów tego poradnika, stworzyłem testowe repozytorium, które nazywa się **LearnGitTest** i zawiera w sobie jeden plik php o zawartości typowego Hello World.

W tym celu wchodzimy do katalogu z naszym projektem i wpisujemy następującą komendę:

`git init`

`Initialized empty Git repository in /XYZ/LearnGitTest/.git/`

Komenda ta stworzy puste repozytorium w naszym katalogu z projektem.

Chwila, chwila - dlaczego puste? Przecież mój projekt ma już swoje pliki - czy to oznacza, że straciłem je wszystkie bezpowrotnie?

*Spokojnie.* Repozytorium przechowuje tylko te pliki i informacje, które zostały do niego dodane - w następnym kroku dowiemy się jak to zrobić.

## Dodawanie kodu

Skoro stworzyliśmy już nasze pierwsze repozytorium nadszedł czas aby nauczyć się jak dodawać do niego nasz kod by zacząć go wersjonować.

Na początek jednak zapoznajmy się z jedną z bardziej używanych komend z których będziemy korzystać podczas codziennej pracy:

`git status`

```
$ git status
# On branch master
#
# Initial commit
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	project.php
nothing added to commit but untracked files present (use "git add" to track)
```

Jak widać, git informuje nas, że póki co nie dodaliśmy żadnych plików do naszego repozytorium, więc nie ma potrzeby wykonywania commita.

Aby dodać wszystkie pliki do naszego projektu (jak wykluczyć niektóre z nich dowiemy się innym razem) należy wykonać poniższą komendę:

`git add .`

Polecenie to doda wszystkie pliki z naszego projektu do repozytorium. Znaną nam już komendą `git status` sprawdzimy, że nasze pliki zostały poprawnie dodane:

```
$ git status
# On branch master
#
# Initial commit
#
# Changes to be committed:
#   (use "git rm --cached <file>..." to unstage)
#
#	new file:   project.php
#
```

Skoro nasz plik jest już przygotowany do tego, by być zawartym w naszym pierwszym commicie, wykonujemy komendę:

`git commit -m "Pierwszy Commit"`

Naszym oczom powinno się ukazać coś podobnego do kodu podanego poniżej - jedyne czym będzie się on różnił to unikalny identyfikator commita.

```
[master (root-commit) 3f70f30] Pierwszy Commit
 1 file changed, 3 insertions(+)
 create mode 100644 project.php
```

## Co teraz?
Właśnie utworzyliśmy nasz pierwszy commit w repozytorium - od tej pory plik o nazwie `project.php` będzie już wersjonowany. To co udało nam się teraz zrobić, to zmiany w repozytorium lokalnym. Jeśli teraz chcemy, by nasz kod zobaczył cały czas, musimy dodać nowe repozytorium zdalne i wysłać tam zmiany naszego lokalnego repozytorium.

#Repozytoria zdalne
Pisząc tą sekcję, skorzystam z GitHuba, jednak te same komendy można wykonywać korzystając z **BitBucketa** którego osobiście polecam jeśli potrzebujecie korzystać z repozytoriów prywatnych.

Pierwsze co musimy zrobić, to założyć repozytorium na GitHubie. Ten proces jest na tyle prosty, że nie będę go opisywał. Jedyną rzeczą o którą muszę Cię jednak poprosić. to nie zaznaczanie opcji tworzenia repozytorium wraz z automatycznie tworzonym plikiem `README.md` - my mamy już swój kod i chcemy go po prostu wrzucić na GH ;)

Po założeniu repozytorium, GitHub poprosi nas o dodanie **repozytorium zdalnego** do naszego istniejącego projektu. Kopiujemy więc komendę, która ukaże się naszym oczom i wykonujemy ją w terminalu:

`git remote add origin git@github.com:XYZ/LearnGitTest.git`

Kiedy dodamy już nasze repozytorium wystarczy, że "popchniemy" nasz kod na serwery GitHub'a:

`git push -u origin master`

Serwer powinien odpowiedzieć nam czymś podobnym do tego:

```
Counting objects: 3, done.
Writing objects: 100% (3/3), 256 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:XYZ/LearnGitTest.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

Teraz wchodząc na stronę naszego repozytorium, będziemy mogli zobaczyć, że nasze repozytorium zawiera już plik `project.php` wraz z komentarzem który dodaliśmy wcześniej.

## Zmiany, zmiany

Co jednak, jeśli chcemy wprowadzać jakieś zmiany?

Nie ma nic prostszego. Wystarczy zmienić odpowiednie pliki - załóżmy, że tym razem zmieniłem parę linii w naszym pliku `project.php` oraz dodałem plik `README.md` który zawiera informacje na temat naszego repozytorium i jest domyślnie wyświetlany podczas ładowania strony naszego projektu na GH.

Aby dodać wszystkie zmienione oraz nowe pliki i przygotować je do commita, wystarczy, że wpiszemy komendę `git add -A .`.
Nas jednak interesuje wykonanie dwóch commitów - pierwszy zawierał będzie zmiany w pliku `project.php`, drugi zaś będzie zawierał informacje o dodanym pliku `README.md`

Jak zwykle z pomocą przychodzi nam komenda `git status`:

```
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   project.php
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#	README.md
no changes added to commit (use "git add" and/or "git commit -a")
```

Widzimy, że Git wykrył zmiany w pliku `project.php`. Możemy je podejrzeć, wpisując komendę `git diff`:

```
diff --git a/project.php b/project.php
index fd51688..82697c5 100644
--- a/project.php
+++ b/project.php
@@ -1,3 +1,6 @@
 <?php
-    echo "Hello World";
+    $username = "Maciej";
+
+    // TODO: More methods, maybe classes?
+    echo "Witaj {$username} \n\n";
 ?>
\ No newline at end of file
```
Dodajemy więc nasz plik do aktualnie przygotowywanego commita za pomocą `git add project.php` a następnie wykonujemy znaną nam już komendę `git commit -m "zmiany, zmiany"`.
Takie same czynności wykonujemy dla pliku `README.md` który stworzyliśmy wcześniej.

Kiedy już dodamy nasz drugi plik, wystarczy, że wrzucimy nasze zmiany na GitHub'a za pomocą komendy `git push -u origin master`.

Kiedy odwiedzimy stronę naszego repozytorium po tak wykonanych czynnościach, powinniśmy w historii naszych zmian zobaczyć informacje o dwóch nowych commitach - możemy podejrzeć co dokładnie zostało zmienione i przez kogo.

## Co teraz?

Z tą wiedzą możemy śmiało korzystać z Git'a na co dzień - na samym początku nie będziemy potrzebować innych komend czy funkcjonalności tego systemu takich jak *gałęzie* czy *pull requesty*.

Mam nadzieję, że dzięki temu krótkiemu wprowadzeniu poczujesz, że **Git jest Git**. Jeśli miałbyś/miałabyś jakiekolwiek pytania na jego temat to zapraszam do kontaktu. Jeśli spodobał Ci się ten poradnik - podziel się nim ze znajomymi. Jestem pewien, że za parę miesięcy będziesz zachodzić w głowę, dlaczego do tej pory nie używałeś/używałaś tego systemu w swojej codziennej pracy.

## Licencja

Creative Commons Share Alike
http://creativecommons.org/licenses/by-sa/2.0/
