# 🌎 **Enumeracja Web - Zadania domowe**


## 4.1 
### 📌 **Polecenie**
Celem zadania jest znalezienie prawidłowego hasła dla pliku http://192.168.100.104/4.5.php?password=guess.

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
echo "jebac to, nie dziala xd"
```

---

## 4.2 
### 📌 **Polecenie**
Celem zadania jest znalezienie ukrytego pliku php w katalogu http://192.168.100.104/misc/

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-small-directories.txt -u http://192.168.100.104/misc/FUZZ
```

---

## 4.3 
### 📌 **Polecenie**
Celem zadania jest znalezienie ukrytego wirtualnego hosta skonfigurowanego na http://192.168.100.104

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
ffuf -w /usr/share/seclists/Discovery/Web-Content/raft-small-directories.txt -u http://192.168.100.104/ -H 'Host = FUZZ'
```

---

## 4.4 
### 📌 **Polecenie**
Celem zadania jest znalezienie subdomeny domeny channel.

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
ffuf -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://192.168.100.104// -H 'Host: FUZZ.channel'
```

---

## 4.5 
### 📌 **Polecenie**
Celem zadania jest znalezienie prawidłowego hasła dla pliku http://192.168.100.104/4.5.php?password=guess.

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
ffuf -w /usr/share/seclists/Passwords/darkweb2017-top100.txt -u 'http://192.168.100.104/4.5.php?password=FUZZ'
```

---

## 4.1p 
### 📌 **Polecenie**
Celem zadania jest odczytanie nazwy hosta (Common Name) z certyfikatu SSL strony https://192.168.100.154/, następnie połączenie się z wirtualnym hostem o tej nazwie.

---

### ✅ **Rozwiązanie**
<!-- Wstaw rozwiązanie tutaj -->

```bash
echo '192.168.100.154 developer' | sudo tee -a /etc/hosts
```

A nastepnie wchodzimy na strone:

```
https://developer
```

---


## 4.2p 
### 📌 **Polecenie**
Celem zadanie jest enumeracja subdomen domeny developer na serwerze 192.168.100.154. Zadanie zostanie automatycznie rozwiązane po znalezieniu ukrytych subdomen.
---

### ✅ **Rozwiązanie**

Znajdujemy subdomeny

```bash
gobuster vhost -u https://developer/ -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --domain developer --append-domain -k
```

Dodajemy ja do /etc/hosts

```
echo '192.168.100.154 beta.developer' | sudo tee -a /etc/hosts
```

Wchodzimy na jedna z nich

```
https://beta.developer/
```
---


## 4.3p 
### 📌 **Polecenie**
Celem zadania jest enumeracja katalogów domeny beta.developer na serwerze 192.168.100.154.
---

### ✅ **Rozwiązanie**

Szukamy odpowiedniego katalogu

```bash
gobuster dir -u https://beta.developer/ -w /usr/share/seclists/Discovery/Web-Content/raft-small-directories.txt -k
```

Wchodzimy na strone:
```
https://beta.developer/admin/
```
---


## 4.4p 
### 📌 **Polecenie**
Celem zadania jest enumeracja plików w katalogu https://beta.developer/admin/ na serwerze 192.168.100.154.

---

### ✅ **Rozwiązanie**

Przeszukujemy katalog admin w poszukiwaniu plikow

```bash
gobuster dir -u https://beta.developer/admin/ -w /usr/share/seclists/Discovery/Web-Content/raft-small-files.txt -k
```

Wchodzimy na strone:

```
https://beta.developer/admin/index_admin.php
```

---

## 4.5p 
### 📌 **Polecenie**
Celem zadania jest złamanie hasła metodą słownikową w panelu https://beta.developer/admin/index_admin.php

---

### ✅ **Rozwiązanie**

Szukamy pasujacego hasla:

```bash
hydra -l anything -P /usr/share/seclists/Passwords/darkweb2017-top100.txt 'https-post-form://beta.developer/admin/index_admin.php:p=^PASS^:Wrong password'
```

Wchodzimy na strone:
```
https://beta.developer/admin/index_admin.php
```

I wpisujemy haslo:
> princess

---



