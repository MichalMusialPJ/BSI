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
- Co robi flaga `-A`?
- Czemu potrzebowaliśmy użyć `nmap`?

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
- Co to jest `-vv`?

---

## 2.2 p 
### 📌 **Polecenie**
Celem zadania jest odczytanie flagi z pliku `flag2.2p.txt` na serwerze **HTTP** i wklejenie do formularza na stronie.

---

### ✅ **Rozwiązanie**

Rozwiązaniem tego zadania będzie użycie jednej z dwóch komend `curl` lub `wget`.

---

### ❓ **Wytłumaczenie**
- Czym jest `curl`?
- Czym jest `wget`?
- Co sprawia, że jesteśmy w stanie do niektórych maszyn połączyć się po **HTTP**?

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
- Czym jest komenda `dir`?
- Czym jest komenda `get`?

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
- Czym jest `smbclient`?
- Co robią flagi `-N` i `-L`?
