# 📚 Sieci Komputerowe — Powtórka Teorii do Quizu

---

## Spis treści

1. [System liczbowy — konwersja DEC ↔ BIN ↔ HEX](#1-system-liczbowy)
2. [Wartości bajtów z ustawionymi MSB](#2-wartości-bajtów-z-ustawionymi-najbardziej-znaczącymi-bitami)
3. [Model ISO/OSI — warstwy](#3-model-isoosi--7-warstw)
4. [Model TCP/IP](#4-model-tcpip)
5. [Model IEEE 802 — podwarstwy](#5-model-ieee-802)
6. [Standardy Ethernet i media transmisyjne](#6-standardy-ethernet-i-media-transmisyjne)
7. [Topologie sieciowe](#7-topologie-sieciowe)
8. [Media transmisyjne — właściwości](#8-media-transmisyjne--właściwości)
9. [Urządzenia sieciowe — warstwy i funkcje](#9-urządzenia-sieciowe--warstwy-i-funkcje)
10. [Domeny kolizyjne i rozgłoszeniowe](#10-domeny-kolizyjne-i-rozgłoszeniowe)
11. [Adresowanie IP (IPv4 i IPv6)](#11-adresowanie-ip-ipv4-i-ipv6)
12. [Maska podsieci (netmask) i subnetting](#12-maska-podsieci-netmask-i-subnetting)
13. [Obliczanie adresu sieci, broadcastu, zakresów](#13-obliczanie-adresu-sieci-broadcastu-i-zakresów-hostów)
14. [Klasy adresów IP i pożyczanie bitów](#14-klasy-adresów-ip-i-pożyczanie-bitów-na-podsieci)
15. [Adres MAC (fizyczny)](#15-adres-mac-fizyczny)
16. [Protokoły sieciowe — przegląd](#16-protokoły-sieciowe--przegląd)
17. [Protokoły rutowalne vs rutujące](#17-protokoły-rutowalne-vs-rutujące)
18. [Kapsułkowanie (enkapsulacja)](#18-kapsułkowanie-enkapsulacja)
19. [Tryby transmisji](#19-tryby-transmisji-simplex-half-duplex-full-duplex)
20. [Typy sieci: LAN, MAN, WAN](#20-typy-sieci-lan-man-wan)
21. [Numeracja IP urządzeń w sieci](#21-ile-adresów-ip-potrzebują-urządzenia-sieciowe)
22. [Bridge (most) — szczegóły działania](#22-bridge-most--szczegóły-działania)
23. [Przełącznik (switch) — szczegóły działania](#23-przełącznik-switch--szczegóły-działania)
24. [Router — szczegóły działania](#24-router--szczegóły-działania)
25. [VLAN](#25-vlan)
26. [Token Ring](#26-token-ring)
27. [TTL (Time To Live)](#27-ttl-time-to-live)
28. [Komendy sieciowe](#28-komendy-sieciowe)
29. [Usługi i protokoły aplikacyjne](#29-usługi-i-protokoły-aplikacyjne)
30. [Modem, DSL, SLIP, PPP](#30-modem-dsl-slip-ppp)
31. [WWW, HTML, HTTP](#31-www-html-http)
32. [Pozostałe pojęcia](#32-pozostałe-pojęcia)

---

## 1. System liczbowy

### Konwersja dziesiętna → dwójkowa

Dzielisz liczbę przez 2, zapisujesz reszty od dołu do góry.

**Przykład: 157₁₀ → ?₂**

| Dzielenie | Wynik | Reszta |
|-----------|-------|--------|
| 157 ÷ 2  | 78    | **1**  |
| 78 ÷ 2   | 39    | **0**  |
| 39 ÷ 2   | 19    | **1**  |
| 19 ÷ 2   | 9     | **1**  |
| 9 ÷ 2    | 4     | **1**  |
| 4 ÷ 2    | 2     | **0**  |
| 2 ÷ 2    | 1     | **0**  |
| 1 ÷ 2    | 0     | **1**  |

Czytamy reszty od dołu: **10011101₂**

### Konwersja dwójkowa → dziesiętna

Mnożysz każdy bit przez odpowiednią potęgę 2:

```
10011101₂ = 1·128 + 0·64 + 0·32 + 1·16 + 1·8 + 1·4 + 0·2 + 1·1 = 157
```

### Wagi bitów w bajcie (8 bitów)

| Pozycja (od lewej) | 7   | 6  | 5  | 4  | 3 | 2 | 1 | 0 |
|---------------------|-----|----|----|----|---|---|---|---|
| Waga                | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

---

## 2. Wartości bajtów z ustawionymi najbardziej znaczącymi bitami

To jedno z najczęściej powtarzanych pytań. Wystarczy zapamiętać:

| Ustawionych MSB | Wzorzec binarny | Wartość dziesiętna |
|------------------|------------------|--------------------|
| 1 bit            | `10000000`       | **128**            |
| 2 bity           | `11000000`       | **192**            |
| 3 bity           | `11100000`       | **224**            |
| 4 bity           | `11110000`       | **240**            |
| 5 bitów          | `11111000`       | **248**            |
| 6 bitów          | `11111100`       | **252**            |
| 7 bitów          | `11111110`       | **254**            |
| 8 bitów          | `11111111`       | **255**            |

> 💡 **Wzór:** Wartość = 256 − 2^(8−n), gdzie n = liczba ustawionych MSB

---

## 3. Model ISO/OSI — 7 warstw

| Nr | Warstwa             | Funkcja kluczowa                                                                 | Jednostka danych |
|----|---------------------|----------------------------------------------------------------------------------|------------------|
| 7  | Aplikacji           | Interfejs dla użytkownika/aplikacji                                              | Dane             |
| 6  | Prezentacji         | Kodowanie, kompresja, szyfrowanie — format danych dobrany do poprawnego odbioru  | Dane             |
| 5  | Sesji               | Organizacja łączy punkt-punkt, zarządzanie sesjami                               | Dane             |
| 4  | Transportowa        | Niezawodna transmisja end-to-end (TCP/UDP)                                       | Segment/Datagram |
| 3  | **Sieciowa**        | **Wyznaczanie drogi pakietów (routing), adresowanie logiczne (IP)**              | **Pakiet**       |
| 2  | **Łącza danych**    | **Kontrola błędów transmisji, adresowanie fizyczne (MAC)**                       | **Ramka**        |
| 1  | **Fizyczna**        | **Napięcia, czasy, sposoby nawiązywania/rozłączania połączenia fizycznego**      | **Bity**         |

### Co się dzieje w poszczególnych warstwach (na quizie!):

- **Warstwa fizyczna (1):** wyspecyfikowane są napięcia sygnałów i czasy trwania transmisji, sposób nawiązywania połączenia i jego rozłączania
- **Warstwa łącza danych (2):** transmisja jest organizowana tak, aby dane przekazywane do wyższej warstwy nie zawierały błędów transmisji
- **Warstwa sieciowa (3):** wyznaczana jest droga pakietów, rozdział zadań pomiędzy węzły sieci i rozliczanie

---

## 4. Model TCP/IP

| Warstwa TCP/IP         | Odpowiednik OSI     | Jednostka danych    |
|------------------------|---------------------|---------------------|
| Aplikacji              | 7, 6, 5             | Dane                |
| Transportowa           | 4                   | Segment / Datagram  |
| Internetowa (sieciowa) | 3                   | Pakiet              |
| Dostępu do sieci       | 2, 1                | Ramka / Bity        |

> ⚠️ Uwaga z quizu: materiał źródłowy podaje, że pakiet jest przetwarzany w warstwie **transportowej**, co terminologicznie jest błędne. Pakiet IP należy do warstwy **internetowej/sieciowej**.

---

## 5. Model IEEE 802

Warstwa łącza danych modelu ISO/OSI w modelu IEEE 802 dzieli się na **dwie podwarstwy**:

| Podwarstwa | Pełna nazwa                    | Funkcja                                     |
|------------|--------------------------------|----------------------------------------------|
| **LLC**    | Logical Link Control           | Kontrola przepływu, multipleksacja protokołów |
| **MAC**    | Media Access Control           | Adresowanie fizyczne, dostęp do medium        |

> ✅ Warstwa łącza danych ISO/OSI = **MAC + LLC** (nie 802.3!)

---

## 6. Standardy Ethernet i media transmisyjne

### Konwencja nazewnictwa: `<prędkość>Base<medium>`

| Standard      | Prędkość  | Medium transmisyjne                                              |
|---------------|-----------|------------------------------------------------------------------|
| **10Base2**   | 10 Mb/s   | Cienki kabel koncentryczny 50 Ω (thin coax)                     |
| **10Base5**   | 10 Mb/s   | Gruby kabel koncentryczny 50 Ω (thick coax)                     |
| **100BaseTX** | 100 Mb/s  | Kabel skrętkowy 4-parowy (wykorzystywane 2 pary)                 |
| **100BaseFX** | 100 Mb/s  | Światłowód 2-włóknowy                                            |
| **1000BaseT** | 1 Gb/s    | Kabel skrętkowy 4-parowy (wykorzystywane **4 pary**)             |
| **1000BaseSX**| 1 Gb/s    | Światłowód 2-włóknowy (wielomodowy, krótki zasięg)               |

### Zasięgi standardu 100Base-FX:

| Typ światłowodu  | Zasięg         |
|-------------------|---------------|
| Wielomodowy       | do **400 m**  |
| Jednomodowy       | do **2000 m** |

### Przepustowość 100Base-FX: **100 Mb/s**

---

## 7. Topologie sieciowe

| Topologia     | Medium typowe        | Charakterystyka                                                    |
|---------------|----------------------|--------------------------------------------------------------------|
| **Magistrala** (bus)  | Kabel koncentryczny (BNC) | Wiele urządzeń na jednej linii transmisyjnej; sygnał rozchodzi się w obu kierunkach |
| **Gwiazda** (star)    | Skrętka (UTP/STP)   | Centralne urządzenie (hub/switch); każde urządzenie ma osobne łącze |
| **Pierścień** (ring)  | Skrętka/światłowód   | Dane krążą w pierścieniu; token passing                            |

---

## 8. Media transmisyjne — właściwości

### Podatność na zakłócenia (od najmniejszej)

```
światłowód < STP < UTP
```

> Światłowód jest **najodporniejszy** na zakłócenia elektromagnetyczne (używa światła, nie prądu).

### Typy mediów

| Medium               | Opis                                                                      |
|----------------------|---------------------------------------------------------------------------|
| **UTP**              | Skrętka nieekranowana — najpopularniejsza w LAN                           |
| **STP**              | Skrętka ekranowana — lepsza ochrona przed zakłóceniami                    |
| **Kabel koncentryczny** | Rdzeń + ekran, używany w topologii magistrali (BNC)                   |
| **Światłowód**       | Przezroczysta, zamknięta struktura z włókna szklanego; propagacja światła  |

### Światłowody

| Typ             | Cechy                                  | Zasięg (bez wzmacniaczy)   |
|-----------------|----------------------------------------|----------------------------|
| **Wielomodowy** | Wiele dróg propagacji światła          | Do **kilku km**            |
| **Jednomodowy** | Jedna droga propagacji, większy zasięg | Do **kilkudziesięciu km**  |

### Kategorie skrętki

- Najczęściej używana w okablowaniu strukturalnym: **kategoria 5** (i 5e)
- Maksymalna długość łącza skrętkowego kat. 5 w sieci 100 Mb/s: **około 100 m**
- Zakończenie: wtyk/gniazdo **RJ-45**
- W topologii gwiazdy LAN najczęściej: **skrętka kat. 5e**

### Transmisja w LAN

- W sieci LAN najczęściej używana jest transmisja **w paśmie podstawowym** (baseband)
- Szerokość pasma jest podawana w **bitach na sekundę** (bps)

---

## 9. Urządzenia sieciowe — warstwy i funkcje

| Urządzenie          | Warstwa OSI | Adresowanie   | Funkcja                                                    |
|---------------------|-------------|---------------|-------------------------------------------------------------|
| **Repeater/Hub**    | 1 (fizyczna)| Brak          | Wzmacnia sygnał, retransmituje do wszystkich portów         |
| **Bridge (most)**   | 2 (łącza)   | **MAC**       | Filtracja ramek na podstawie adresu MAC, zmniejsza domenę kolizyjną |
| **Switch (przełącznik)** | 2 (łącza) | **MAC**   | Filtracja + przełączanie ramek, każdy port = osobna domena kolizyjna |
| **Router**          | 3 (sieciowa)| **IP (logiczny)** | Łączy sieci, wyznacza trasy pakietów (routing)          |
| **Karta sieciowa**  | 2 (łącza)   | MAC           | Interfejs hosta do sieci                                    |

---

## 10. Domeny kolizyjne i rozgłoszeniowe

### Domena kolizyjna
Obszar sieci, w którym ramki mogą kolidować (jednoczesna transmisja = kolizja).

**Kolizja w Ethernet** = rezultat równoczesnej transmisji danych przez dwa węzły w jednym segmencie sieci.

### Jak urządzenia wpływają na domeny kolizyjne:

| Urządzenie       | Wpływ na domeny kolizyjne                                          |
|------------------|---------------------------------------------------------------------|
| **Repeater/Hub** | **Zwiększa** domenę kolizyjną (łączy segmenty w jedną domenę)      |
| **Bridge**       | **Zmniejsza** domenę kolizyjną (separuje segmenty)                 |
| **Switch**       | **Zwiększa liczbę** domen kolizyjnych + **zmniejsza** każdą z nich (każdy port = osobna domena) |
| **Router**       | Każdy port = osobna domena kolizyjna I rozgłoszeniowa               |

### Domena rozgłoszeniowa (broadcast/sygnalizacji)
Obszar, w którym ramki broadcast docierają do wszystkich urządzeń.

- Jeden port **przełącznika** stanowi jedną **domenę kolizyjną**
- Jeden port **routera** stanowi jedną **domenę rozgłoszeniową**
- Wymiana danych między oddzielnymi domenami rozgłoszeniowymi wymaga **routera**

### Obliczanie domen kolizyjnych — przykłady

| Topologia                                                      | Domeny kolizyjne |
|----------------------------------------------------------------|-------------------|
| Switch 16-portowy + switch 8-portowy (wszędzie komputery)      | Każdy port z komputerem + łącze trunk = **23** lub **24** (zależy od pytania — patrz uwagi) |
| Switch 16p ↔ switch 8p (oba bez komputerów w porcie łączącym) | Liczymy porty z komputerami + łącze między switchami |
| Hub 8p + hub 8p + repeater                                     | **1** (hub i repeater nie separują domen) |
| Hub 8p (podłączony do portu switcha 16p)                       | Switch: każdy port = 1 domena, hub = 1 wspólna domena. Liczymy porty switcha (15 z komputerami) + 1 port z hubem = **16** |

> ⚠️ Hub/koncentrator/repeater: **NIE** dzielą domeny kolizyjnej — tworzą jedną wspólną.  
> ⚠️ Switch/bridge: **TAK** dzielą — każdy port to osobna domena.

---

## 11. Adresowanie IP (IPv4 i IPv6)

### IPv4

- Długość: **32 bity** (4 bajty)
- Zapis: **notacja kropkowo-dziesiętna** (dotted decimal), np. `192.168.1.1`
- Każdy oktet oddzielony **kropką**
- Zakres oktetu: 0–255

### IPv6

- Długość: **128 bitów**
- Zapis: **szesnastkowo**, czterocyfrowe grupy oddzielone **dwukropkiem**, np. `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

### Adres MAC w systemie Windows

- Zapis: **szesnastkowo**, dwucyfrowe elementy oddzielone znakiem **myślnika (-)**, np. `00-1A-2B-3C-4D-5E`

### Adres MAC — ogólny zapis

- Najczęściej: **szesnastkowo**, dwucyfrowe elementy oddzielone **dwukropkiem (:)**, np. `00:1A:2B:3C:4D:5E`

---

## 12. Maska podsieci (netmask) i subnetting

### Czym jest netmask?

- Składa się z **32 bitów** (jak adres IPv4)
- Ciąg jedynek (część sieciowa) + ciąg zer (część hostowa)
- Służy do **wyznaczania numeru sieci** z pełnego adresu IP

### Domyślna maska podsieci

Określa, które bity adresu IP odnoszą się do **części sieciowej**; jest standardową maską dla danej klasy adresu IP.

### Notacja CIDR `/n`

`/n` oznacza, że `n` bitów maski jest ustawionych na 1.

### Tabela masek

| Prefix | Maska               | Adresy w podsieci | Adresy unicast (użyteczne) |
|--------|----------------------|--------------------|-----------------------------|
| /24    | 255.255.255.0        | 256                | **254**                     |
| /25    | 255.255.255.128      | 128                | **126**                     |
| /26    | 255.255.255.192      | 64                 | **62**                      |
| /27    | 255.255.255.224      | 32                 | **30**                      |
| /28    | 255.255.255.240      | 16                 | **14**                      |
| /29    | 255.255.255.248      | 8                  | **6**                       |
| /30    | 255.255.255.252      | 4                  | **2**                       |
| /23    | 255.255.254.0        | 512                | **510**                     |
| /22    | 255.255.252.0        | 1024               | **1022**                    |
| /20    | 255.255.240.0        | 4096               | **4094**                    |
| /19    | 255.255.224.0        | 8192               | **8190**                    |
| /11    | 255.224.0.0          | 2 097 152           | **2 097 150**               |
| /10    | 255.192.0.0          | 4 194 304           | **4 194 302**               |

> **Wzór:**
> - Liczba adresów w podsieci = 2^(32−n)
> - Adresy unicast (użyteczne) = 2^(32−n) − 2

---

## 13. Obliczanie adresu sieci, broadcastu i zakresów hostów

### Algorytm krok po kroku

1. **Maska:** Zamień prefix `/n` na maskę dziesiętną
2. **Adres sieci:** Wykonaj AND binarny: `adres IP AND maska`
3. **Adres broadcast:** Zaneguj maskę (hosty = same 1) i dodaj do adresu sieci: `adres sieci OR NOT maska`
4. **Min host:** adres sieci + 1
5. **Max host:** adres broadcast − 1

### Przykład: `54.214.155.21 /26`

1. Maska /26 → `255.255.255.192` (6 bitów hosta, `11000000` w ostatnim oktecie)
2. Ostatni oktet: 21 AND 192:
   - `21` = `00010101`
   - `192` = `11000000`
   - AND = `00000000` → **0**
3. Adres sieci: `54.214.155.0`
4. Broadcast: `54.214.155.0 + 63` = `54.214.155.63`
5. Min host: `54.214.155.1`
6. Max host: `54.214.155.62`

### Szybki sposób — bloki podsieci

Dla maski `/26` (64 adresy w bloku), podsieci zaczynają się co 64:

```
.0, .64, .128, .192
```

Adres `.21` wpada w blok `.0–.63`, więc:
- Sieć: `.0`, Broadcast: `.63`, Hosty: `.1–.62`

### Czy adres jest adresem sieci, broadcastu, czy hosta?

| Adres w podsieci          | Typ                    |
|---------------------------|------------------------|
| Wszystkie bity hosta = 0  | **Adres sieci**        |
| Wszystkie bity hosta = 1  | **Adres broadcastowy** |
| Inne kombinacje           | **Adres unicastowy**   |

**Przykład:** `19.59.45.224` w podsieci o masce `255.255.255.224` (/27):
- Bloki co 32: `.0, .32, .64, .96, .128, .160, .192, .224`
- `.224` jest początkiem bloku → **adres sieci**

**Przykład:** `83.9.14.207` w podsieci o masce `255.255.255.240` (/28):
- Bloki co 16: `.192, .208, ...`
- `.207` = `.192 + 15` → ostatni adres w bloku `.192–.207` → **adres broadcastowy**

---

## 14. Klasy adresów IP i pożyczanie bitów na podsieci

### Klasy adresów

| Klasa | Pierwszy oktet | Domyślna maska    | Bity sieci | Bity hosta |
|-------|-----------------|---------------------|------------|------------|
| A     | 1–126          | 255.0.0.0 (/8)      | 8          | **24**     |
| B     | 128–191        | 255.255.0.0 (/16)   | 16         | **16**     |
| C     | 192–223        | 255.255.255.0 (/24) | 24         | **8**      |

### Maksymalna liczba bitów do pożyczenia na podsieci

Muszą pozostać **co najmniej 2 bity** na adresy hostów.

| Klasa | Bity hosta | Max pożyczonych bitów        |
|-------|------------|------------------------------|
| **A** | 24         | 24 − 2 = **22**              |
| **B** | 16         | 16 − 2 = **14**              |
| **C** | 8          | 8 − 2 = **6**                |

---

## 15. Adres MAC (fizyczny)

- **Długość:** 48 bitów = 6 bajtów = **12 cyfr szesnastkowych**
- Pola adresowe w ramkach Ethernet II i 802.3 zawierają adres składający się z **12 cyfr szesnastkowych**
- **Adres IP** = adres logiczny (warstwa 3, sieciowa)
- **Adres MAC** = adres fizyczny (warstwa 2, łącza danych)
- Zapis w Windows: szesnastkowo z myślnikami (np. `00-1A-2B-3C-4D-5E`)
- Zapis ogólny/Linux: szesnastkowo z dwukropkami (np. `00:1A:2B:3C:4D:5E`)

---

## 16. Protokoły sieciowe — przegląd

| Protokół | Warstwa | Funkcja                                                        |
|----------|---------|----------------------------------------------------------------|
| **ARP**  | 2/3     | Translacja **IP → MAC** (zna IP, szuka MAC)                    |
| **RARP** | 2/3     | Translacja **MAC → IP** (zna MAC, szuka IP) — historyczny      |
| **ICMP** | 3       | Komunikaty kontrolne, sprawdzanie osiągalności (ping)           |
| **IP**   | 3       | Adresowanie logiczne, routing pakietów — **protokół rutowalny** |
| **IPX**  | 3       | Protokół rutowalny (Novell NetWare) — **protokół rutowalny**   |
| **TCP**  | 4       | Niezawodna transmisja, połączeniowy                             |
| **UDP**  | 4       | Transmisja bezpołączeniowa, bez gwarancji dostarczenia          |
| **DHCP** | 7       | Dynamiczne przydzielanie adresów IP                             |
| **BOOTP**| 7       | Przydzielanie adresów IP (prekursor DHCP)                       |
| **DNS**  | 7       | Zamiana nazwy domenowej na adres IP                             |
| **FTP**  | 7       | Transfer plików (klient–serwer, dwa kanały: sterujący + danych) |
| **HTTP** | 7       | Wymiana danych między klientem a serwerem WWW                   |
| **Telnet**| 7      | Zdalne logowanie i praca na komputerze w sieci                  |
| **SMTP** | 7       | Wysyłanie poczty elektronicznej                                 |

### Protokoły NIE służące do dynamicznego przydzielania IP:
- **ICMP**, **TCP**, **UDP**, **RIP** — żaden z nich nie przydziela dynamicznie adresów IP
- Protokoły, które MOGĄ: **DHCP**, **BOOTP**

---

## 17. Protokoły rutowalne vs rutujące

### Protokoły rutowalne (routable)
Mogą być przesyłane przez routery między sieciami:
- **IP**, **IPX**

### Protokoły rutujące (routing protocols)
Służą do wyznaczania tras w tablicach routingu:
- **RIP**, **OSPF**, **IGRP**, **IS-IS**, **EIGRP**

### Protokoły, które NIE są rutujące:
- **ICMP** — to protokół komunikatów kontrolnych, nie wyznacza tras

---

## 18. Kapsułkowanie (enkapsulacja)

Kapsułkowanie polega na tym, że **ramka warstwy wyższej jest traktowana jako dane w warstwie niższej**.

```
Dane → [Nagłówek L4 | Dane] → [Nagłówek L3 | Segment] → [Nagłówek L2 | Pakiet | Suma kontrolna]
```

Każda warstwa dodaje swój nagłówek do danych otrzymanych z warstwy wyższej.

---

## 19. Tryby transmisji (simplex, half-duplex, full-duplex)

| Tryb              | Kierunek                           | Opis                                              |
|-------------------|------------------------------------|----------------------------------------------------|
| **Simplex**       | Jednokierunkowy                    | Dane tylko w jednym kierunku                        |
| **Half-duplex**   | Dwukierunkowy naprzemienny         | W danej chwili transmisja tylko w **jednym** kierunku |
| **Full-duplex**   | Dwukierunkowy jednoczesny          | Każdy kierunek ma **osobny kanał transmisyjny**     |

---

## 20. Typy sieci: LAN, MAN, WAN

| Typ     | Zasięg                    | Cechy                                                                              |
|---------|---------------------------|-------------------------------------------------------------------------------------|
| **LAN** | Budynek/pomieszczenia     | Węzły nie potrzebują urządzeń warstwy sieciowej do wymiany danych; niewielki obszar, mała stopa błędu, transmisja ~10+ Mb/s |
| **MAN** | Miasto/metropolia         | Obszar pośredni między LAN i WAN; wiele łączy nadmiarowych o dużej przepustowości   |
| **WAN** | Kraj/kontynent            | Duży obszar geograficzny; łącza punkt-punkt, łącza dzierżawione                     |

---

## 21. Ile adresów IP potrzebują urządzenia sieciowe

### Zasada:
- **Hub/switch** — **NIE** potrzebuje adresu IP (działa na warstwie 2 lub 1)
- **Host (komputer)** — potrzebuje **1 adresu IP** na interfejs
- **Router** — potrzebuje adresu IP na **każdym** interfejsie

### Przykłady:

| Topologia                                                | Potrzebne adresy IP |
|----------------------------------------------------------|---------------------|
| 6 hostów → switch → Internet                            | **6** (switch nie potrzebuje IP) |
| 5 hostów → hub → Internet                               | **5** (hub nie potrzebuje IP) |
| 3 hosty → switch ↔ hub ← 3 hosty                        | **6** (tylko hosty) |
| 3 hosty → switch A ↔ switch B ← 3 hosty                 | **6** (tylko hosty) |

---

## 22. Bridge (most) — szczegóły działania

- Działa na **warstwie 2** (łącza danych)
- Opiera się na **adresach MAC** (sprzętowych)
- Filtruje ramki sprawdzając **docelowy unicastowy adres warstwy 2**
- **Ogranicza ruch ramek unicastowych** — ramki groupowe i broadcastowe **są przekazywane** dalej
- Wykorzystuje tablicę **adresów sprzętowych nadawców ramek** (uczy się z adresów źródłowych)
- **Zmniejsza domenę kolizyjną**
- **NIE zmniejsza domeny rozgłoszeniowej**

---

## 23. Przełącznik (switch) — szczegóły działania

- Działa na **warstwie 2** (łącza danych)
- Operuje w warstwie 2 i wykorzystuje **adres MAC**
- Filtruje ramki sprawdzając **docelowy unicastowy adres warstwy 2**
- **Zwiększa liczbę domen kolizyjnych** (każdy port = osobna domena)
- **Zmniejsza domenę kolizyjną** (izoluje segmenty)
- Ramki broadcastowe: odbiera w jednym porcie → wysyła do **wszystkich pozostałych portów**

### Gwiazda z przełącznikiem (po ustabilizowaniu):
- Unicast: przełącznik przesyła ramkę tylko do portu docelowego
- Broadcast/multicast: przesyłane do **wszystkich pozostałych portów**

### Gwiazda z koncentratorem (hubem):
- Wszystkie ramki (unicast, broadcast) przesyłane do **wszystkich portów**

---

## 24. Router — szczegóły działania

- Działa na **warstwie 3** (sieciowej)
- Opiera się na **adresach logicznych** (IP)
- Przeznaczony do łączenia **dwóch lub więcej sieci**
- Wykorzystuje **tablice routingu** konfigurowane przez **protokoły rutujące** (RIP, OSPF, etc.)
- Każdy port routera = osobna **domena kolizyjna** i **rozgłoszeniowa**
- Komunikat o wyzerowaniu pola TTL wysyła **router** (ICMP Time Exceeded)

---

## 25. VLAN

- Wirtualna sieć lokalna — logiczny podział przełącznika na osobne domeny rozgłoszeniowe
- Wymiana danych pomiędzy dwoma VLANami (= oddzielnymi domenami rozgłoszeniowymi) wymaga **routera**

---

## 26. Token Ring

- Technologia oparta na **pierścieniu z przesyłaniem znacznika (token)**
- Idea: przechwycenie znacznika transmitowanego przez kolejno podłączone stacje i wysłanie ramki z danymi
- Prędkości historyczne: **4 Mb/s** i **16 Mb/s** (istniały też warianty 100 Mb/s)

> ⚠️ W quizie pojawiają się różne odpowiedzi — sprawdź, czy pytanie dotyczy wersji źródłowej (która może podawać nietypowe wartości).

---

## 27. TTL (Time To Live)

- Pole w nagłówku pakietu IP
- Zmniejszane o 1 przez każdy router na trasie
- Gdy TTL = 0, **router** odrzuca pakiet i wysyła komunikat **ICMP Time Exceeded** do nadawcy
- Zapobiega nieskończonemu krążeniu pakietów w sieci

---

## 28. Komendy sieciowe

| Komenda       | Funkcja                                                        |
|---------------|----------------------------------------------------------------|
| **ping**      | Sprawdza osiągalność hosta (używa ICMP Echo Request/Reply)     |
| **tracert**   | Wyznacza trasę pakietu do celu (trasowanie)                    |
| **arp**       | Wyświetla/zarządza tablicą mapowania IP ↔ MAC                  |
| **netstat**   | Pokazuje aktywne połączenia i statystyki sieciowe              |
| **net**       | Zarządza zasobami sieciowymi (net use, net share, etc.)        |
| **ipconfig**  | Wyświetla konfigurację IP (Windows)                            |
| **hostname**  | Wyświetla nazwę komputera                                       |
| **mail**      | Wysyłanie listów elektronicznych (e-mail)                      |
| **HOLD**      | Wstrzymanie połączenia (zawieszenie rozmowy bez rozłączania)   |

---

## 29. Usługi i protokoły aplikacyjne

| Usługa/Protokół | Opis                                                                   |
|------------------|------------------------------------------------------------------------|
| **FTP**          | Protokół transmisji plików (klient–serwer, kanał sterujący + danych)   |
| **Telnet**       | Zdalne logowanie i praca na komputerze w sieci                         |
| **DNS**          | Zamiana adresu domenowego na adres IP                                  |
| **DHCP**         | Dynamiczne przydzielanie adresów IP                                    |
| **E-mail**       | Transfer listów elektronicznych przez sieć                             |
| **Proxy**        | Serwer pośredniczący między komputerem użytkownika a siecią            |

### FTP — tryby transferu

| Tryb       | Kiedy używać                                      |
|------------|---------------------------------------------------|
| **ASCII**  | Pliki tekstowe (np. z Notatnika, pliki `.txt`)     |
| **Binary** | Pliki binarne (np. pliki Worda `.docx`, obrazy)   |

---

## 30. Modem, DSL, SLIP, PPP

### Modem
- Urządzenie do **modulacji i demodulacji sygnału** — przekształca sygnał cyfrowy na analogowy (i odwrotnie)
- Transmisja danych **bit po bicie** przez łącze telefoniczne

### Modulacja
- Przekształcanie informacji cyfrowej na sygnał dostosowany do medium transmisyjnego (i odwrotnie po stronie odbiorczej)

### DSL (Digital Subscriber Line)
- Usługa dostępu do **szerokopasmowego Internetu** przez linię telefoniczną

### Protokoły modemowe (historycznie)
- Standard komunikacji modemów: **56K** (wcześniej V.42 bis — kompresja)
- Transmisja bezpośrednia: **PPP**

### SLIP vs PPP

| Protokół | Cechy                                                                    |
|----------|--------------------------------------------------------------------------|
| **SLIP** | Prostszy, opakowuje datagram IP, brak korekcji błędów                    |
| **PPP**  | Korekcja błędów, uwierzytelnianie, obsługa połączeń szeregowych          |

### Modem zwrotny (null modem)
- Skrętny kabel umożliwiający bezpośrednie połączenie komputerów tak, jakby między nimi były modemy i łącze telefoniczne

---

## 31. WWW, HTML, HTTP

### WWW (World Wide Web)
- Umożliwia dostęp do stron internetowych za pomocą przeglądarek; dokumenty hipertekstowe przesyłane protokołem HTTP

### HTML
- Język do tworzenia dokumentów hipertekstowych
- Plik tekstowy zawierający zbiór znaczników definiujących postać dokumentu
- Niesformatowany plik tekstowy przeznaczony do publikowania danych w WWW
- Pliki JPG **NIE** są wczytywane bezpośrednio jako część kodu — HTML zawiera **odnośniki** wskazujące, skąd załadować obrazy

### Odsyłacz (hiperłącze)
- Rodzaj znacznika zawierającego **URL** dokumentu, do którego prowadzi

### URL (Uniform Resource Locator)
- Ujednolicony sposób zapisu adresu i lokalizacji zasobu w Internecie

### Przeglądarka internetowa
- Program umożliwiający dostęp do stron internetowych; interpretuje HTML, CSS, JavaScript i wyświetla treść graficznie

### Wyszukiwarka internetowa
- Program do wyszukiwania dokumentów HTML w sieci Internet według podanych kryteriów

### HTTP (HyperText Transfer Protocol)
- Protokół wymiany danych między klientami a serwerami WWW

### Metody HTTP

| Metoda   | Opis                                                                         |
|----------|------------------------------------------------------------------------------|
| **GET**  | Żąda od serwera wskazanego zasobu (strony, obrazu, pliku)                    |
| **POST** | Przekazuje dane do serwera w części zasadniczej zapytania (np. pary nazwa=wartość) |
| **HEAD** | Przekazuje dane o wskazanym pliku z serwera **bez kopiowania** jego zawartości (tylko nagłówki) |

### Formant (form control)
- Element dokumentu HTML wykorzystywany do **wprowadzania danych** przeznaczonych dla procedur CGI

---

## 32. Pozostałe pojęcia

### Komunikacja multimedialna
- Transmisja różnych typów informacji (dane, głos, obraz) w jednym lub wielu strumieniach danych

### Protokół sieciowy
- Język (zbiór reguł) używany przez węzły sieci w komunikacji sieciowej

### Standard komunikacyjny
- Zbiór reguł i protokołów określających format, sposób przesyłania danych oraz kompatybilność sprzętu i oprogramowania

### Format
- Sposób organizacji, struktury lub prezentacji danych, informacji, dokumentów lub urządzeń

### Numer IP domyślnej bramy (default gateway)
- Umożliwia przekazywanie pakietów do innych sieci (router brzegowy)

### Outlook vs Outlook Express (historycznie)
- Outlook: rozbudowane narzędzie biznesowe
- Outlook Express: prostszy program pocztowy do użytku domowego

---

## 🎯 Szybkie podsumowanie — najważniejsze fakty do zapamiętania

1. **4 MSB** = 240, **5 MSB** = 248, **6 MSB** = 252
2. Warstwa 2 = łącza danych (MAC, bridge, switch); Warstwa 3 = sieciowa (IP, router)
3. Adresy unicast = 2^(32−n) − 2
4. ARP: IP → MAC; RARP: MAC → IP; DHCP: dynamiczne IP
5. ICMP: sprawdzanie osiągalności (ping); NIE jest protokołem rutującym
6. Switch: zwiększa liczbę domen kolizyjnych, zmniejsza ich rozmiar
7. Hub/repeater: zwiększa domenę kolizyjną (nie separuje)
8. Router: łączy sieci, każdy port = osobna domena rozgłoszeniowa
9. Skrętka kat. 5 = max ~100 m; RJ-45; baseband w LAN
10. IPv4 = kropki + dziesiętnie; IPv6 = dwukropki + szesnastkowo; MAC (Windows) = myślniki + hex

---

*Powodzenia na quizie! 🍀*
