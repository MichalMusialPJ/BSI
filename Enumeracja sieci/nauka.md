# 🕵️‍♂️ **Enumeracja Sieci**

## 2.1 
### 📌 **Polecenie**
Celem zadania jest przeskanowanie hosta `192.168.100.2` za pomocą narzędzia **nmap** i znalezienie portu, na którym nasłuchuje usługa **SSH**.

---

### ✅ **Rozwiązanie**

Przed połączeniem przez **ssh**:
```bash
nmap 192.168.100.2
```

Po połączeniu przez **ssh**:
```bash
nmap -A 192.168.100.2
```

---

### ❓ **Wytłumaczenie**
- Czym jest `nmap`?
> Nmap to narzedzie, ktore pozwala nam na skanowanie sieci komputerowych. Mozemy dzieki niemu wykrywac urzadzenia w sieci, sprawdzanie otwartych portow oraz sprawdzac uslugi i systemy operacyjne na tych urzadzeniach. Jest uzywany m.in w pentestach oraz audytach bezpieczenstwa. Sama komenda nmap bez zadnych flag sprawdza nam tylko porty.
- Co robi flaga `-A`?
> Ogolnie sluzy nam do bardziej szczegolowego skanowania, pozwala nam na sprawdzenie systemu operacyjnego, wersji uslug oraz skanowanie skryptow.
- Czemu potrzebowaliśmy użyć `nmap`?
> W zadaniu bylo zdefiniowane, ze musimy sprawdzic port na ktorym nasluchuje usluga ssh na danym hoscie. Natomaist mielismy alternatywe do tego rozwiazania. Moglismy uzyc komendy `nc -zv <adres_IP> <zakres_portow>`, natomaist na pierwszy rzut oka widac, ze jest to bardziej skomplikowane rozwiazanie.

---

## 2.1 p 
### 📌 **Polecenie**
Celem zadania jest przeskanowanie maszyny `192.168.200.52`. Warto dodać również opcję `-p-`, która skanuje wszystkie porty (zamiast top1000) oraz `-vv`, która wyświetla więcej informacji w czasie rzeczywistym.

---

### ✅ **Rozwiązanie**
```bash
nmap -sT -sV -sC -O --osscan-guess -p- -vv 192.168.200.52
```

---

### ❓ **Wytłumaczenie**
- Co dają nam flagi użyte w komendzie?
>`-sT` To flaga, ktora sprawia, ze nmap wykonuje pelne skanowanie TCP, jest ono widoczne dla administratora, bo nawiazuje pelne polaczenie z portem, natomaist nie potrzebujesz uprawnien root'a by to zrobic. <br>
`-sV` To flaga, ktora pozwala nam na sprawdzenie wersji uslug dzialajacyh na hoscie. <br>
`-sC` To flaga ktora uruchamia domyslne skrypy z bazy skryptow nmap. Sa to skrypty przeznaczone do wykonania podstawowych testow i wykrywania luk w zabezpieczeniach. <br>
`-O` To flaga, ktora pozwala nam na zidentyfikowanie systemu operacyjnego skanowanego hosta. (Czyli po prostu tego na ktorym wykonujemy nmap) <br>
`-p-` To flaga ktora sprawia, ze nmap skanuje wszystkie porty dostepne, czyli te z zakresu 1-65535. Bez tej flagi nmap skanuje tylko podstawowe porty (Co zwykle wystarcza). <br>
`--osscan-guess` Pomaga w zidentyfikowaniu systemu operacyjnego, gdy taka informacja nie jest jawna (jest wiele powodow ktore moga byc tego przyczyna m.in. brak uprawnien root'a). "Zgaduje" na podstawie danych. Odpowiedz nie zawsze jest precyzyjna.
- Co to jest `-vv`? 
> `-vv` Pozwala nam na otrzymanie "logow" wykonywania komendy, zwykle stosuje sie to w celu debugowania. Mozliwe jest uzycie `-v` , `-vv` lub `-vvv`. Roznia sie od siebie iloscia informacji ktore nam pokaze. `-v` pokaze nam najmniej a `-vvv` najwiecej. Ta flaga moze byc stosowana do wiekszosci komend, np do `ssh`.

---

## 2.2 p 
### 📌 **Polecenie**
Celem zadania jest odczytanie flagi z pliku `flag2.2p.txt` na serwerze **HTTP** i wklejenie do formularza na stronie.

---

### ✅ **Rozwiązanie**

Rozwiązaniem tego zadania będzie użycie jednej z dwóch komend `curl` lub `wget`.

Z uzyciem `curl`:

```bash
curl http://192.168.200.52/flag2.2p.txt
```

Z uzyciem `wget`:
```bash
wget http://192.168.200.52/flag2.2p.txt
cat flag2.2p.txt
```

---

### ❓ **Wytłumaczenie**
- Czym jest `curl`?
> `curl` to narzedzie, ktore pozwala na wykonywanie requestow **HTTP** lub **HTTPS** do danego adresu **ip** lub **url**. Czesto jest stosowany do tego, by sprawdzic czy nasz web-server dziala, w srodowiskach gdzie nie mamy przegladarki internetowej. Moze obslugiwac tez protokoly takie jak FTP IMAP POP3 i inne.
- Czym jest `wget`?
> `wget` to narzedzie, ktore sluzy znam do pobierania roznych plikow z serwerow internetowych za pomoca protokolow takich jak **HTTP**, **HTTPS** lub **FTP**. Jest dobrym narzedziem do pobierania pojedynczych plikow, calych stron jak i rekurencyjnego pobierania zasobow, np. mamy strone internetowa na jakims serwerze FTP i mozemy wgetem pobrac ja rekurencyjnie cala (Czyli wraz z zawartoscia podfolderow).
- Co sprawia, że jesteśmy w stanie do niektórych maszyn połączyć się po **HTTP**?
> To bardzo zasadne pytanie, ktore moze sie pojawic. Mozemy sie polaczyc po **HTTP** (Czyli przy uzyciu np. `curl`), gdy dany host ma skonfiguwany web-serwer, czyli jakiego nginx, apache albo IIS. Bardzo ogolnie mowiac, po prostu host musi byc przystosowany do tego, by przyjmowac takie requesty.

---

## 2.3 p 
### 📌 **Polecenie**
Celem zadania jest odczytanie flagi z pliku `flag2.3p.txt` na serwerze **FTP** i wklejenie do formularza na stronie.

---

### ✅ **Rozwiązanie**

Najpierw logujemy się do serwera **ftp** poprzez komendę i logujemy się przez credentiale podane w zadaniu:
```bash
ftp <ip>
```

Następnie używamy komendy:
```bash
dir
```

Następnie używamy komendy do pobrania zasobu do naszego serwera, na którym jesteśmy teraz:
```bash
get flag2.3p.txt
```

Potem przerywamy połączenie przez **ssh** używając:
```bash
exit
```

Odczytujemy zawartość pliku i wklejamy flagę do zadania na stronie:
```bash
cat <filename>
```

---

### ❓ **Wytłumaczenie**
- Czym jest komenda `ftp` i czym jest **ftp**?
> FTP jest protokolem, ktory sluzy do przesylania plikow miedzy komputerami w sieci. Dziala na zasadzie klient-serwer. Zwykle dziala on na porcie **21** i **20**, 21 sluzy do kontroli polaczenia a 20 do faktycznego przesylania plikow. <br>
 Sama komenda `ftp` umozliwia nam polaczenie z serwerem **FTP** z poziomu terminala i zarzadzanie przesylaniem plikow.
- Czym jest komenda `dir`?
> Po zalogowaniu na serwer **FTP** mozemy uzyc jej do wyswietlenie listy plikow i katalogow. To takie `ls` tylko ze na serwerze **FTP**.
- Czym jest komenda `get`?
> Sluzy nam po prostu do pobrania pliku z serwera **FTP** na **Lokalny** komputer.

---

## 2.4p 
### 📌 **Polecenie**
Celem zadania jest odczytanie flagi z pliku `flag2.4p.txt` na serwerze **SMB** i wklejenie do formularza na stronie.

---

### ✅ **Rozwiązanie**

Do rozwiązania użyjemy komendy **smbclient**.

Opcjonalnie na początku używamy:
```bash
smbclient -N -L //192.168.200.52/
```

Dlaczego opcjonalnie? Ta komenda pokazuje nam po prostu jakie mamy dostępne zasoby na tym serwerze, ale w poniższej komendzie przechodzimy od razu do odpowiedniego dysku **"FLAG"**:
```bash
smbclient -N //<ip>/FLAG
```

Następnie możemy użyć:
```bash
ls
```

Lecz również jest to opcjonalne, ponieważ w poleceniu mamy powiedziane, jakiego pliku szukamy. By go pobrać do nas lokalnie, używamy:
```bash
get flag2.4p.txt
```

Następnie wychodzimy przy użyciu:
```bash
exit
```

Odczytujemy zawartość pliku txt przy użyciu:
```bash
cat flag2.4p.txt
```

Odpowiedź wklejamy na stronę z zadaniem.

---

### ❓ **Wytłumaczenie**
- Czym jest serwer **SMB**?
> Jest to serwer, ktory sluzy nam do udostepniania plikow i folderow w sieci **lokalnej** korzystajac z protokolu **SMB**. Glowna roznica miedzy **SMB** a **FTP** to fakt, ze **SMB** pozwala nam na modyfikacje zawartosci pliku na serwerze co sprawia, ze nie musimy go pobierac lokalnie a potem wrzucac jeszcze raz na serwer tylko zmieniony. Istotnym faktem jest rowniez to ze **SMB** w przeciwienstwu do **FTP** uzywa szyfrowania.
- Czym jest `smbclient`?
> Jest to narzedzie, ktore pozwala nam na polaczenie oraz zarzadzanie serwerem **SMB** z poziomu terminala.
- Co robią flagi `-N` i `-L`?
> `-N` To flaga, ktora sprawia, ze nasz smbclient probuje polaczyc sie do serwera bez podawania hasla. Jest to mozliwe, gdy serwer pozwala na dostep anonimowy. <br>
 `-L` To flaga, ktora wyswietla nam liste dostepnych zasobow (np. foldery, dyski, drukarki) na danym serwerze **SMB**










## X.X 
### 📌 **Polecenie**
<!-- Wstaw treść polecenia tutaj -->

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
<!-- Wstaw komendy tutaj -->
```

---

### ❓ **Wytłumaczenie**
- <!-- Wstaw pytanie 1 -->
- <!-- Wstaw pytanie 2 -->
- <!-- Wstaw pytanie 3 -->

---
