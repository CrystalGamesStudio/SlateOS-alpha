# SlateOS-alpha
Operating System. 


## Overview

Slate to lekki, płynny system operacyjny oparty na Linuxie, zaprojektowany jako bezpośrednia alternatywa dla Windows 11. System stawia na prywatność, szybkość, brak bloatware oraz inteligentne dopasowanie do użytkownika przez system person onboardingowych.

---

## Problem Statement

Windows 11 stał się systemem pełnym reklam, telemetrii, wymuszonego bloatware, planowego postarzania sprzętu i lock-inu do ekosystemu Microsoftu. Młodzi dorośli (do 30 lat) są coraz bardziej sfrustrowani tym kierunkiem, a istniejące dystrybucje Linuxa nie oferują wystarczająco przyjaznego, dopracowanego doświadczenia aby skutecznie zastąpić Windowsa dla przeciętnego użytkownika.

---

## Users

| Typ użytkownika | Opis | Wolumen |
|---|---|---|
| Zwykły użytkownik | Codzienne użytkowanie, brak specjalistycznych potrzeb | Największy segment |
| Gamer | Gaming PC, wysokie FPS, sklepy z grami | Duży segment (do 30 lat) |
| Programista | Dev environment, CLI, IDE, AI tools | Średni segment |
| Grafik | Narzędzia graficzne, HiDPI, zarządzanie kolorem | Średni segment |
| Pisarz | Edytory tekstu, brak dystrakcji, notatki | Mały-średni segment |
| Streamer/Twórca | OBS, edycja wideo, webcam | Średni segment |
| Muzyk/Producent | DAW, niskolatencyjne audio, JACK | Mały segment |
| Student | Nauka, PDF, notatki, komunikatory | Duży segment |
| Biznes | Biuro, email, kalendarz, wideokonferencje | Średni segment |
| Fotograf | RAW editing, import z aparatu, biblioteka zdjęć | Średni segment |
| Rozrywka | Spotify, VLC, Netflix, maksymalnie prosto | Duży segment |
| Digital Nomad | VPN, Notion, komunikatory, lekki system | Mały-średni segment |
| Dziecko | Zwykły + ograniczenia rodzicielskie, filtrowanie treści | Segment rodzinny |

---

## Goals & Success Criteria

- [ ] System uruchamia się w środowisku QEMU/wirtualnym z działającym GUI
- [ ] Interfejs graficzny jest płynny z animacjami (Wayland + Hyprland)
- [ ] Terminal działa poprawnie po uruchomieniu
- [ ] Ekran bootowania (`_Starting_`) wyświetla logo + animowany loader bars-style
- [ ] Ekran logowania (`_Login_`) działa z hasłem i bez hasła
- [ ] Główny ekran (`Main Screen`) wyświetla górny pasek, dolny pasek, tapetę z logo
- [ ] System działa płynnie na słabym sprzęcie (auto-degradacja UI)
- [ ] Kompatybilność z plikami `.exe`, `.deb`, `.dmg`, `.tar.gz`, `.AppImage`
- [ ] Onboarding z wyborem persony instaluje właściwy zestaw aplikacji
- [ ] Zero telemetrii użytkownika — tylko auto-raporty błędów

---

## User Stories

1. Jako **nowy użytkownik**, chcę wybrać personę podczas instalacji, aby system skonfigurował się automatycznie pod moje potrzeby bez ręcznej konfiguracji.
2. Jako **gamer**, chcę żeby moje gry z Windowsa działały przez Proton bez konfiguracji, aby nie musieć zostawać przy Windowsie dla gier.
3. Jako **programista**, chcę żeby ADM-CLI zainstalowało moje dev environment przez jeden curl command, aby w minuty mieć gotowe środowisko pracy.
4. Jako **użytkownik słabego sprzętu**, chcę żeby system wykrył mój hardware i dostosował wydajność, aby Slate działał płynnie na moim starym laptopie.
5. Jako **użytkownik dbający o prywatność**, chcę mieć pewność że system nie zbiera moich danych, aby móc mu zaufać inaczej niż Windowsowi.
6. Jako **rodzic**, chcę stworzyć konto dziecka z ograniczeniami, aby dziecko mogło bezpiecznie używać komputera.
7. Jako **dowolny użytkownik**, chcę kliknąć plik `.exe` i żeby się odpalił, aby nie myśleć o kompatybilności.
8. Jako **użytkownik**, chcę móc cofnąć aktualizację jeśli coś się posypie, aby nie bać się aktualizowania systemu.

---

## Scope

### MVP (Faza 1) — cel: działający system graficzny

- Działający GUI na QEMU/emulatorze
- Wayland + Hyprland compositor
- Ekran bootowania (`_Starting_`) z logo i loaderem bars-style
- Ekran logowania (`_Login_`) — z hasłem i bez hasła
- Główny ekran z górnym paskiem, dolnym paskiem, tapetą
- Terminal (domyślny)
- Stabilność i płynność animacji

### Pełny produkt (po MVP)

- Persona onboarding (13 person)
- Kompatybilność plików (Proton, Darling, dpkg, AppImage, tar.gz)
- Slate Store (Flatpak + apt + snap)
- Auto-wykrywanie sprzętu + dynamiczna optymalizacja
- Alerty przed przeciążającymi akcjami
- Aktualizacje w tle + rollback
- Konto Dziecka z ograniczeniami rodzicielskimi
- Raporty błędów w tle (zero telemetrii użytkownika)

### Out of scope (wszystkie wersje)

- Własna przeglądarka internetowa (Firefox jako domyślna)
- Slate Mobile
- Własna chmura / storage
- Własne konto online / wymaganie rejestracji

---

## System Components

```
┌─────────────────────────────────────────────────────┐
│                    SLATE OS                         │
├─────────────────────────────────────────────────────┤
│  BOOT LAYER                                         │
│  └── _Starting_ screen (logo + bars loader)         │
├─────────────────────────────────────────────────────┤
│  DISPLAY LAYER                                      │
│  └── Wayland + Hyprland compositor                  │
│      ├── _Login_ screen                             │
│      └── Main Screen                               │
│          ├── Top bar (menu apki, zegar, temp, bat)  │
│          ├── Desktop (tapeta + watermark logo)      │
│          └── Bottom bar (search, apps, separator)   │
├─────────────────────────────────────────────────────┤
│  PERSONA LAYER (post-MVP)                           │
│  └── Calamares installer + onboarding               │
│      └── 13 person → auto-konfiguracja              │
├─────────────────────────────────────────────────────┤
│  COMPATIBILITY LAYER (post-MVP)                     │
│  ├── Proton (.exe)                                  │
│  ├── Darling partial (.dmg)                         │
│  ├── dpkg (.deb)                                    │
│  ├── auto-detect (.tar.gz)                          │
│  └── native (.AppImage)                             │
├─────────────────────────────────────────────────────┤
│  PACKAGE LAYER (post-MVP)                           │
│  └── Slate Store → Flatpak + apt + snap             │
├─────────────────────────────────────────────────────┤
│  HARDWARE LAYER (post-MVP)                          │
│  └── auto-detect → dynamic optimization + alerts   │
└─────────────────────────────────────────────────────┘
```

---

## Persona Configurations

| Persona | Kluczowe apki | Optymalizacja |
|---|---|---|
| **Zwykły** | Firefox, terminal, menedżer plików | As-fast-as-possible, nic extra |
| **Gamer** | Game Center (Steam/Heroic/Lutris — user wybiera), Discord, MangoHud, Proton-GE | CPU governor performance, GPU sterowniki, GameMode |
| **Programista** | ADM-CLI (curl installer), IDE (user wybiera), tmux | Swap pod kompilację, I/O performance, Docker |
| **Grafik** | Krita, GIMP, Inkscape, Darktable, Blender; Affinity via Proton (user wybiera) | GPU acceleration, HiDPI, ICC color profiles |
| **Pisarz** | LibreOffice Writer, Obsidian, Typora, FocusWriter, Zotero, Notion | Focus mode domyślnie, Night Light, auto-backup |
| **Streamer/Twórca** | OBS, DaVinci Resolve / Kdenlive, webcam setup | GPU encoding, niskie latency |
| **Muzyk/Producent** | LMMS, Ardour, Carla | JACK audio, niskie latency audio |
| **Student** | Okular, Anki, Zotero, Teams/Zoom | Balans wydajności |
| **Biznes** | LibreOffice Suite, Thunderbird, Teams, Calendar | Stabilność, auto-updates |
| **Fotograf** | Darktable, RawTherapee, szybki import z aparatu | RAM pod duże pliki RAW, HiDPI |
| **Rozrywka** | Spotify, VLC, Firefox | Maksymalnie prosto, zero technikaliów |
| **Digital Nomad** | VPN pre-configured, Notion, komunikatory | Lekki system, bateria |
| **Dziecko** | Zwykły zestaw + filtrowanie treści, limity czasowe | Brak dostępu do ustawień systemowych |

---

## UI Design Decisions

| Element | Decyzja |
|---|---|
| `_AppName_` label | Interaktywny przełącznik w górnym pasku i w oknie — klik otwiera dropdown |
| `_AppName_` dropdown | Input bez obramowania (zmiana apki) + duże kwadratowe przyciski (Force Quit, Zamknij, Minimalizuj, Maksymalizuj) + opcje apki (File, Edit itp.) |
| `_AppName_` dropdown animacja | Płynna animacja przy otwieraniu |
| Menu aplikacji | Schowane pod kliknięciem `_AppName_` — górny pasek pozostaje czysty; dotyczy też .dmg apps via Darling |
| Force Quit | Wymaga potwierdzenia przed zamknięciem |
| Dolny pasek auto-hide | Opcjonalne w ustawieniach, domyślnie zawsze widoczny |
| Górny pasek auto-hide | Opcjonalne w ustawieniach |
| Launchpad animacja | Blur transition przy otwieraniu |
| Launchpad siatka | Auto-dopasowuje się do rozdzielczości ekranu |
| Wskaźnik aktywnej apki | Długa kreska pod ikoną = aktywna i używana |
| Wskaźnik nieaktywnej apki | Kropka = widoczna/zminimalizowana, nieużywana |
| Dolny pasek lewo | Slate Store (domyślny, usuwalny) + open-at-login apps |
| Dolny pasek separator | `|` pionowa kreska oddziela przypięte apki od systemowych |
| Dolny pasek prawo | Ikona Apps → Launchpad (wszystkie aplikacje) |
| Górny pasek | WiFi/BT → menu aktywnej apki → zegar + temp + bateria |
| Ekran startowy | Logo + bars-style animated loader (przesuwa się i znika) |
| Ekran logowania mocny sprzęt | Animowana tapeta + powiadomienia + profil + input hasła |
| Ekran logowania słaby sprzęt | Profil + input hasła / przycisk zaloguj |
| Przyciski okna | ● (oktagon) = zamknij, □ = fill/unfill (ostre rogi gdy fill), ▽ (odwrócony trójkąt) = minimalizuj |
| Rogi okien | Zaokrąglone domyślnie, ostre gdy zmaksymalizowane (fill) |
| Logo watermark | Na tapecie głównego ekranu |
| Powiadomienia pop-up | Wyskakują na górze ekranu na środku |
| Centrum powiadomień | Wysuwa się z boku jak Windows 10 Action Center, otwierane przez ikonę w górnym pasku |
| Szybkie toggles (domyślne) | Sieć, Wszystkie ustawienia, Bluetooth, Tryb nocny, Lokalizacja, Oszczędzanie baterii, VPN, Wycinanie ekranu, Tryb samolotowy, Pobliskie udostępnianie, Apps manager — edytowalne |
| WiFi/BT klik | Szybkie menu (lista sieci, toggle) — bez wchodzenia w ustawienia |
| Blur/frosted glass | Opcjonalny plugin ze Slate Store, suwak przezroczystości, domyślnie solid dark |
| Wirtualne pulpity | Jak macOS Mission Control — swipe gestem, podgląd, drag & drop okien |
| Search | Przeszukuje wszystko na komputerze: aplikacje, pliki, foldery, ustawienia |
| Ustawienia systemu | Wzorowane na macOS — boczny panel z kategoriami |
| Slate Store | Kategorie jak App Store (Polecane, Gry, Narzędzia itp.) |
| Email usera | Opcjonalny w onboardingu — jeśli podany, reset hasła działa; jeśli nie, przycisk ? ukryty |
| Pogoda w górnym pasku | Temperatura na dworze (pogoda), nie CPU |
| Górny pasek | W pełni edytowalny — przeciąganie, usuwanie, dodawanie widgetów |

---

## Implementation Decisions

| Decyzja | Wybór | Uzasadnienie |
|---|---|---|
| GUI stack | Wayland + Hyprland | Płynne animacje out-of-the-box, nowoczesny, duża społeczność |
| Installer | Calamares | Graficzny, sprawdzony, używany przez Manjaro i inne |
| Kompatybilność .exe | Proton (Valve) | Najlepsza kompatybilność z grami i soft Windows |
| Kompatybilność .dmg | Darling (partial) | Jedyna opcja na Linux, z disclaimerem dla usera |
| Package manager | Flatpak + apt + snap za Slate Store | User widzi jeden sklep, nie widzi co działa pod spodem |
| Przeglądarka | Firefox | Open-source, prywatny, bez lock-inu |
| Terminal programista | tmux | Multiplexer pro, standard w dev środowiskach |
| Dev setup | ADM-CLI via curl | Automatyzuje cały dev environment w minuty |
| Menedżer plików | Nautilus | Znajomy, dobrze zintegrowany z GTK |
| Płatne apki w Store | Redirect do strony www | Affinity bezpłatne (Canva), inne → strona producenta |
| Baza systemu | Arch Linux | Najlżejszy, Hyprland w oficjalnych repo, pacman, rolling release |
| Instalacja Hyprland | Auto przez Slate installer | User nie dotyka konfiguracji — gesty, sterowniki, stack w pełni auto |
| Touchpad gesty | Hyprland 0.51+ wbudowane, auto-enabled | Pełna konfigurowalność gestów natywnie |
| Wacom | libwacom + input-wacom kernel module | Obsługa tabletów przez Wayland |
| Telemetria | Zero danych użytkownika | Tylko auto error reports do dewelopera |
| Aktualizacje | W tle, bez wymuszonego restartu, z rollback | Anty-Windows philosophy |
| Model biznesowy | Free → Server paid → max $25 USD | Eliminacja Windowsa jako priorytet |
| Walidacja MVP | QEMU/emulator — GUI działa płynnie | Konkretny, mierzalny milestone |
| Motywy | Ciemny domyślnie, jasny/kontrast/inne ze Slate Store | Personalizacja bez narzucania |
| Szyfrowanie dysku | Opcjonalne podczas instalacji | Jak FileVault / BitLocker |
| Firewall | Wbudowany, domyślnie włączony | Zero konfiguracji przez usera |
| Aktualizacje — zgoda | User potwierdza przed pobraniem, instalacja w tle | Kontrola bez bólu |
| Liczba kont | Max 3 na jednym komputerze | — |
| Konto Dziecka | Zwykły + ograniczenia zarządzane z konta rodzica, bez admina | Jak iOS parental controls |
| Onboarding | W Calamares po instalacji, przed pierwszym pulpitem | Język/region manualnie, klawiatura auto + potwierdzenie |
| Tapety domyślne | Kilka do wyboru podczas onboardingu | — |
| Do Not Disturb | Manualny, wycisza pop-upy i dźwięki, powiadomienia w centrum | Nie włącza się automatycznie |
| Gesty touchpada | 2 palce = scroll, 3 palce = Mission Control, out-of-the-box | — |
| Wirtualne pulpity | Jak macOS Mission Control — swipe, podgląd, drag & drop | — |
| Menedżer haseł | Ze Slate Store, nie wbudowany | — |
| Drukarki | Ze Slate Store, nie wbudowane | — |
| Aktywna apka w pasku | Tylko jedna naraz w górnym pasku | — |
| Screenshot | Jak Ubuntu, zapisuje do Pobranych automatycznie | Cały ekran/okno/obszar |
| Nagrywanie ekranu | Wbudowane, switch audio mikrofon/system | — |
| VPN | Toggle → Slate Store, NordVPN jako pierwsza propozycja | — |
| Oceny w Slate Store | Brak ocen/recenzji | Prosto i czysto |
| Instalacja offline | Niemożliwa — wymaga internetu | — |
| Recovery/Safe mode | Brak | — |
| Touchscreen | Wspierany, wirtualna klawiatura auto na polach tekstowych | Laptopy 2-in-1, tablety |
| Bluetooth audio | Out-of-the-box | — |
| Pobliskie udostępnianie | AirDrop-style przez Bluetooth | — |
| Skróty klawiszowe | Ctrl-based domyślnie, Cmd-based opcjonalnie (klawiatury Mac) | — |
| Pierwsze uruchomienie | Krótki tour/poradnik po onboardingu | — |
| Aplikacja Logs | Czytelna dla wszystkich userów | Nie tylko dla zaawansowanych |
| Dual-boot | Wsparcie + auto-detekcja Windows w Calamares | Jak Ubuntu installer |
| Force Quit | Tylko przez System Monitor | Brak dedykowanego skrótu |
| Night Light | Konfigurowalny harmonogram (w tym auto wschód/zachód) | — |
| Menu kontekstowe pulpitu | Prawy klik — zmiana tapety, nowy folder, ustawienia wyświetlania | Jak Windows/Ubuntu |
| Window snapping | Przeciągnięcie do krawędzi = połówki/ćwiartki ekranu | Jak Windows |
| Accessibility | Skalowanie, czytnik ekranu, kontrast — widoczne w Settings, do pobrania ze Store | — |

---

## Domyślne aplikacje systemowe

Firefox, Transmission, Remmina, Rhythmbox, Totem (Wideo), Shotwell, Document Viewer (Evince), Document Scanner (Simple Scan), Eye of GNOME, Text Editor (Gedit), Calculator, Calendar, System Monitor, Disk Utility, Archive Manager (File Roller), Screenshot, Characters, Font Viewer, Logs, Password & Keys (Seahorse), Startup Applications, Software & Updates, Software Updater, Additional Drivers, Language Support, Nautilus (menedżer plików), Terminal

---

**MVP:** System odpala się w QEMU, GUI działa, animacje są płynne, terminal działa — to jest "faza 1 gotowa".

**Post-MVP:** Każda persona testowana manualnie — instalacja, konfiguracja, działanie kluczowych aplikacji.

---

## Open Questions

*Brak — wszystkie decyzje podjęte.*

---

## References

- Discovery summary: inline (sesja /ask powyżej)
- UI Designs: slate-starting.pdf, slate-login.pdf, slate-main-screen.pdf
- ADM-CLI: https://github.com/CrystalGamesStudio/ADM-CLI
- Loader animation reference: https://cliloaders.com/bars_3