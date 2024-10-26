# Enumeracja Sieci


## 2.1 
### Polecenie:
Celem zadania jest przeskanowanie hosta 192.168.100.2 za pomocą narzędzia nmap i znalezienie portu, na którym nasłuchuje usługa SSH.
##

### Rozwiazanie:

Przed polaczeniem przez ssh:

`nmap 192.168.100.2`

Po polaczeniu przez ssh:

`nmap -A 192.168.100.2`

### Wytlumaczenie:

Czym jest `nmap`?

Co robi flaga `-A`?