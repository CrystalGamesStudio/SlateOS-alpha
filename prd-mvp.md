# PRD: Slate OS — MVP

## Overview

MVP Slate to minimalna, działająca wersja systemu operacyjnego potwierdzająca że graficzny interfejs (GUI) odpala się prawidłowo, płynnie i stabilnie. To jest punkt, na którym poprzednia próba budowy systemu upadła — terminal działał, GUI nie. Cel MVP: udowodnić że ten problem jest rozwiązany.

Brak person, brak Slate Store, brak kompatybilności plików, brak optymalizacji sprzętowej — tylko czysty, działający, płynny pulpit.

---

## Problem Statement

Poprzednia próba budowy systemu zatrzymała się na etapie GUI — terminal działał, interfejs graficzny nie chciał wystartować. MVP ma jednoznacznie zweryfikować, że ten blocker został pokonany, zanim zainwestowany zostanie czas w pozostałe funkcje Slate.

---

## Users

Ten sam developer (Adam) jako tester. Brak person — system w wersji MVP jest jednolity dla każdego.

---

## Goals & Success Criteria

- [ ] System odpala się w QEMU (lub innym emulatorze)
- [ ] Baza: Arch Linux
- [ ] Wayland + Hyprland compositor działa stabilnie
- [ ] Ekran bootowania — logo Slate + animowany loader (bars-style, przesuwa się i znika — jak https://cliloaders.com/bars_3); bez etykiety `_Starting_`
- [ ] Ekran logowania `_Login_` działa:
  - input hasła + Enter do zalogowania
- [ ] Główny pulpit (Main Screen) renderuje się poprawnie:
  - górny pasek (zegar live)
  - tapeta — domyślny obrazek (PNG/JPG) z logo Slate
  - dolny pasek (ikony klikalne, launchpad/apps otwiera widok wszystkich aplikacji)
- [ ] Terminal odpala się i działa poprawnie
- [ ] Przycisk okna ● (zamknij) działa

---

## User Stories

1. Jako **developer**, chcę odpalić Slate w QEMU i zobaczyć działający ekran bootowania z logo i animowanym loaderem, aby potwierdzić że boot sequence działa.
2. Jako **developer**, chcę zalogować się na ekranie `_Login_` wpisując hasło i naciskając Enter, aby potwierdzić że autentykacja i przejście do pulpitu działa.
3. Jako **developer**, chcę zobaczyć główny pulpit z górnym i dolnym paskiem renderującymi się poprawnie, aby potwierdzić że layout UI jest zaimplementowany.
4. Jako **developer**, chcę otworzyć terminal i wykonać podstawowe komendy, aby potwierdzić że terminal działa w środowisku graficznym.
5. Jako **developer**, chcę otworzyć launchpad (apps) z dolnego paska i zobaczyć listę aplikacji, aby potwierdzić że launcher działa.
6. Jako **developer**, chcę przetestować przycisk ●, aby potwierdzić że zamykanie okna działa.

---

## Scope

### W MVP

- Arch Linux jako baza systemu
- Wayland + Hyprland (auto-konfiguracja przez instalator Slate — gesty, sterowniki)
- Ekran bootowania — logo + animowany loader bars-style (bez etykiety `_Starting_`)
- Ekran `_Login_`:
  - hasło + Enter do zalogowania
- Główny pulpit:
  - górny pasek (zegar live)
  - tapeta — domyślny obrazek PNG/JPG z logo Slate (dostarczony przez Adama)
  - dolny pasek — działający: ikony klikalne, ikona apps otwiera launchpad (widok wszystkich aplikacji)
- Terminal (domyślny)
- Przycisk okna: ● (zamknij)

### Out of scope dla MVP

- System person / onboarding w Calamares
- Slate Store
- Kompatybilność plików (.exe, .dmg, .deb, .tar.gz, .AppImage)
- Auto-wykrywanie sprzętu i dynamiczna optymalizacja
- Centrum powiadomień + szybkie toggles
- Wirtualne pulpity / Mission Control (gest 3 palce)
- `_AppName_` jako przełącznik aplikacji w górnym pasku
- Zaokrąglone/ostre rogi okien (stylizacja okien)
- Window snapping
- Wielu użytkowników / przełączanie kont
- Konto Dziecka
- Edytowalny górny pasek
- Blur/frosted glass
- Motywy (jasny, kontrast)
- Aktualizacje + rollback
- Szyfrowanie dysku
- Firewall
- Domyślne aplikacje (poza terminalem) — Nautilus, Calculator, itd.
- Reset hasła przez email
- Dual-boot detection
- Accessibility opcje
- Nagrywanie ekranu / screenshot
- Tour po pierwszym uruchomieniu
- Submit button (trójkąt) — login przez Enter
- Touchpad gesty
- □ fill/unfill i ▽ minimalizuj (zostaje tylko ● zamknij)
- Power/sleep/restart na ekranie logowania
- WiFi/Bluetooth ikony i funkcjonalność
- Profil/zdjęcie użytkownika na ekranie logowania
- Etykieta `_Starting_` na boot screen
- Customowe animacje okien (otwieranie/zamykanie) — domyślny Hyprland wystarczy
- Search w dolnym pasku

### Dodatkowe propozycje do wycięcia z MVP

Te elementy są technicznie "ładne", ale nie testują samego faktu że GUI działa — można je przesunąć do Fazy 2:

- **Pogoda w górnym pasku** — wymaga internetu + API, niepotrzebne do testu GUI
- **Search w dolnym pasku** — funkcjonalność wyszukiwania to osobny moduł, nie blocker GUI
- **Ikony WiFi/BT z działającym menu** — wystarczy że ikony się renderują, klikalne menu to już warstwa funkcjonalna
- **Animowany loader bars-style na boot** — można zacząć od statycznego logo, animację dodać gdy reszta działa
- **Ekran logowania bez hasła (przycisk "Zaloguj")** — jeden tryb logowania (z hasłem) wystarczy do testu
- **Profil/avatar na ekranie logowania** — placeholder wystarczy, nie trzeba pełnego systemu avatarów
- **Power/sleep/restart na ekranie logowania** — opcjonalne, nie testuje GUI compositor-a
- **Dolny pasek w całości** — można zacząć tylko z górnym paskiem + pulpitem, dolny pasek dodać jako drugi krok

**Absolutny rdzeń MVP** (jeśli chcesz iść jeszcze bardziej minimalistycznie):
Arch + Hyprland bootuje się w QEMU → widać pulpit z tapetą → da się otworzyć terminal → da się go zamknąć/zminimalizować/zmaksymalizować z animacją. To jest dosłownie "GUI działa, nie jak w poprzednim projekcie".

---

## Implementation Decisions

| Decyzja | Wybór | Uzasadnienie |
|---|---|---|
| Baza systemu | Arch Linux | Najlżejszy, Hyprland natywnie w repo |
| GUI stack | Wayland + Hyprland | Płynne animacje, cel MVP |
| Loader bootowania | Bars-style (cliloaders.com/bars_3) | Element wizualny już zaprojektowany |
| Tapeta MVP | Jedna domyślna z logo watermark | Pełen wybór tapet to post-MVP |
| Terminal | Domyślny (np. Foot/Kitty pod Hyprland) | Cel: potwierdzić że terminal działa w GUI |
| Przycisk okna | ● (zamknij) tylko — fill/minimalizuj post-MVP | Najmniejszy zakres do potwierdzenia że window management działa |
| Login | Enter zamiast submit buttona | Mniejszy zakres UI |

---

## Validation Strategy

**Definicja "MVP gotowe":**

System bootuje się w QEMU → ekran bootowania z animowanym logo → ekran `_Login_` (hasło + Enter) → pulpit z tapetą (logo PNG/JPG), górnym paskiem (live zegar) i dolnym paskiem (klikalne ikony + launchpad/apps) → terminal się odpala i działa → przycisk ● zamyka okno.

Jeśli wszystko powyżej działa bez crashy i z płynnymi animacjami — Faza 1 (MVP) jest zamknięta, można przejść do Fazy 2 (persony, Slate Store, kompatybilność plików).

---

## References

- Pełny PRD: prd (Slate OS — wszystkie funkcje)
- UI Designs: slate-starting.pdf, slate-login.pdf, slate-main-screen.pdf
- Loader animation reference: https://cliloaders.com/bars_3