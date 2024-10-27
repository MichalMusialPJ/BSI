# 🕵️‍♂️ **Enumeracja Sieci - Praca domowa**

Dokladnie dzialanie komend oraz roznych flag uzytych w tych zadaniach znajduje sie w pliku nauka.md. Tutaj znajduja sie tylko rozwiazania zadan domowych oraz ewentualne uwagi dotyczace roznic miedzy tymi zadaniami a tymi z pliku nauka.

## 2.1 
### 📌 **Polecenie**
Celem zadania jest przeskanowanie hosta 192.168.100.102 za pomocą narzędzia nmap i znalezienie portu, na którym nasłuchuje usługa SSH.

Tym razem wypróbuj dodatkowo opcję -vv.

---

### ✅ **Rozwiązanie**
Jakims chujem ta komenda mi rozwiazala to zadanie XD idk

```bash
nmap -sT -sC 192.168.100.0/24 -vv
```

---

## 2.2
### 📌 **Polecenie**
W ramach tego zadania połącz się poprzez SSH ze znalezionym wcześniej portem.

---

### ✅ **Rozwiązanie**

Zadanie rozwiazujemy przez polaczenie sie komenda `ssh` do naszego hosta z uzyciem flagi `-p`
```bash
ssh student@<ip> -p <port>
```

---

## 2.3
### 📌 **Polecenie**

Uruchom manual (man) do polecenia nmap. Polecenie to pokaże nam listę wszystkich opcji i parametrów, z jakimi możemy uruchomić nmap. Warto się z nimi zapoznać choć pobieżnie. Niektóre będą nam później potrzebne.

---

### ✅ **Rozwiązanie**

Zadanie rozwiazujemy poprzez uzycie komendy `man`, Wazne jest ze aby zadanie zostalo zaliczone trzeba przejsc na sam dol outputu komendy (przynajmniej u mnie).

```bash
man nmap
```

---

## 2.4
### 📌 **Polecenie**
Celem zadania jest przeskanowanie sieci 192.168.100.0/24 pod kątem uruchomionych hostów bez skanowania portów i usług.

Tym razem wypróbuj dodatkowo opcję -vv.

---

### ✅ **Rozwiązanie**

Do rozwiazania tego zadania uzywamy komendy nmap wraz z flagami `-sn` oraz `-vv`.

```bash
nmap -sn 192.168.100.0/24 -vv
```

---

## 2.5
### 📌 **Polecenie**

Celem zadania jest przeskanowanie sieci 192.168.100.0/24 pod kątem uruchomionych hostów oraz otwartych portów TCP bez dokładnego skanowania usług.

Tym razem wypróbuj dodatkowo opcję -vv.

---

### ✅ **Rozwiązanie**
Do rozwiazania tego zadania uzywamy komendy nmap wraz z flagami `-sT` oraz `-vv`.

```bash
nmap -sT 192.168.100.0/24 -vv
```

---

## 2.6
### 📌 **Polecenie**

Celem zadania jest przeskanowanie sieci 192.168.100.0/24 pod kątem uruchomionych hostów oraz otwartych portów TCP z uwzględnieniem wersji usług.

Tym razem wypróbuj dodatkowo opcję -vv.

---

### ✅ **Rozwiązanie**
Do rozwiazania tego zadania uzywamy komendy nmap wraz z flagami `-sV` oraz `-vv`.

```bash
nmap -sV 192.168.100.0/24 -vv
```

---

## 2.7
### 📌 **Polecenie**

Celem zadania jest przeskanowanie sieci 192.168.100.0/24 pod kątem uruchomionych hostów, otwartych portów TCP oraz uruchomieniem domyślnych skryptów.

Tym razem wypróbuj dodatkowo opcję -vv.

---

### ✅ **Rozwiązanie**
Do rozwiazania tego zadania uzywamy komendy nmap wraz z flagami `-sC` oraz `-vv`.

```bash
nmap -sC 192.168.100.0/24 -vv
```

---

## 2.8
### 📌 **Polecenie**

Celem zadania jest przeskanowanie sieci 192.168.100.0/24 pod kątem uruchomionych hostów i systemów operacyjnych.

Tym razem wypróbuj dodatkowo opcję -vv.

---

### ✅ **Rozwiązanie**
Do rozwiazania tego zadania uzywamy komendy nmap wraz z flagami `-O`, `--osscan-guess` oraz `-vv`.

```bash
nmap -O --osscan-guess 192.168.100.0/24 -vv
```

---

## 2.1 p
### 📌 **Polecenie**

Celem zadania jest przeskanowanie maszyny 192.168.200.152. Warto dodać również opcję -p-, która skanuje wszystkie porty (zamiast top1000) oraz -vv, która wyświetla więcej informacji w czasie rzeczywistym.

Większość opcji nmapa możemy ze sobą łączyć.

---

### ✅ **Rozwiązanie**
Do rozwiazania tego zadania uzywamy komendy nmap wraz z flagami `-sT`, `-sV`, `-sC`, `-O`, `--osscan-guess` oraz `-vv`.

```bash
nmap -sT -sV -sC -O --osscan-guess -p- -vv  192.168.200.152
```

---

## 2.2 p
### 📌 **Polecenie**

Celem zadania jest odczytanie flagi z pliku **flag2.2p.txt** na serwerze **HTTP** i wklejenie do formularza na stronie.

---

### ✅ **Rozwiązanie**

By rozwiazac to zadanie musimy polaczyc sie z naszym serwerem **HTTP** uzywajac `curl`, lub `wget`. Nieoczywista rzecza w tym zadaniu byl fakt, ze domyslny port dla http, czyli **80** nie byl otwarty. Web-serwer ktory znajdowal sie na hoscie byl ustawiony pod przyjmowanie polaczen przez port **8080**, wiec musielismy dodac ten port po znaku `:` po adresie ip hosta. Zeby takie informacje pozyskac musielismy wczesniej uzyc komendy `nmap <ip>`.

```bash
curl http://192.168.200.152:8080/flag2.2p.txt
```

Output wrzucamy w odpowiedz na stronie.

---

## 2.3 p
### 📌 **Polecenie**

Celem zadania jest odczytanie flagi z pliku **flag2.3p.txt** na serwerze **FTP** i wklejenie do formularza na stronie.

---

### ✅ **Rozwiązanie**

Laczymy sie z serwerem ftp:

```bash
ftp 192.168.200.152
```
Logujemy sie:

>login: anonymous
>haslo: mozna po prostu enter

Pobieramy plik na nasza **lokalna** maszyne:

```bash
get flag2.3p.txt
```

Wychodzimy z serwera **FTP**:

```bash
exit
```

Odczytujemy zawartosc pliku:

```bash
cat flag2.3p.txt
```

Zawartosc wklejamy na strone w odpowiedzi.

---

## 2.4 p
### 📌 **Polecenie**

Celem zadania jest odczytanie flagi z pliku **flag2.4p.txt** na serwerze **SMB** i wklejenie do formularza na stronie.

---

### ✅ **Rozwiązanie**

Laczymy sie z serwerem **SMB** uzywajac narzedzia `smbclient`. Jednoczesnie od razu wskazujac, ze chcemy przejsc do folderu **FLAG**:

```bash
smbclient -N //192.168.200.152/FLAG/
```
Pobieramy plik przy uzyciu `get` na lokalna maszyne:

```bash
get flag2.4p.txt
```

Wychodzimy z serwera **SMB**:

```bash
exit
```

Odczytujemy zawartosc pliku:

```bash
cat flag2.4p.txt
```

---

