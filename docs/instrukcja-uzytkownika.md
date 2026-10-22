# VPN do domu: instrukcja

Panel urządzenia: `http://IP_ALIX` (w domu albo z włączonym VPN), login `root`.

## Dodanie telefonu lub laptopa

1. Network → Interfaces → przy `wg0` kliknij **Edit** → zakładka **Peers** → **Add peer**.
2. Uzupełnij:
   - Disabled: **odznaczone**
   - Description: nazwa urządzenia, np. `telefon-ania`
   - kliknij **Generate new key pair** i **Generate preshared key**
   - Allowed IPs: `10.10.10.X/32`, gdzie X to kolejny wolny numer (2, 3, 4...). Każde urządzenie musi mieć inny.
   - Persistent Keep Alive: `25`
   - Endpoint Host i Endpoint Port zostaw puste
3. Kliknij **Generate configuration...**
   - Connection endpoint: z listy wybierz **-- custom --** i wpisz adres domu (publiczne IP albo adres DuckDNS)
   - resztę zostaw bez zmian
4. Telefon: w aplikacji WireGuard **+** → **Skanuj kod QR**.
   Laptop: **Download peer configuration file** i zaimportuj plik w aplikacji WireGuard.
5. **Back to peer configuration** → **Save** → **Save** → **Save & Apply**.
6. Przy `wg0` kliknij **Restart**.

## Usunięcie urządzenia (np. zgubiony telefon)

`wg0` → **Edit** → **Peers** → **Delete** przy urządzeniu → **Save & Apply** → **Restart** przy `wg0`.

## Czy działa

- Status → WireGuard: przy urządzeniu widać **Latest Handshake**.
- Na telefonie z włączonym VPN strona ifconfig.me pokazuje adres domu.

## Czego nie ruszać

- Nie przekierowuj w routerze portów 80 ani 443 na ALIX-a.
- Nie zmieniaj ustawień `wg0` w General Settings ani stref firewalla.
- Nie klikaj **Generate new key pair** w samym `wg0`. Wszystkie urządzenia przestaną działać.

## Gdy coś nie działa

1. Odłącz zasilanie ALIX-a na 10 sekund i podłącz ponownie. Odczekaj 3 minuty.
2. Jeśli dalej nie działa, a VPN nie jest pilnie potrzebny: zostaw ALIX-a wyłączonego i usuń w routerze przekierowanie UDP 51820. Wyłączenie niczego nie psuje.

ALIX aktualizuje się sam w nocy z soboty na niedzielę i wtedy może przez kilka minut nie działać.
