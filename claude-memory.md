# SLATE OS — Pełny Kontekst dla Claude Code

> Ten plik zawiera wszystko co Claude Code musi wiedzieć o projekcie Slate OS.
> Przeczytaj go w całości przed wykonaniem jakiegokolwiek zadania.

---

## Czym jest Slate?

Slate to lekki, płynny system operacyjny oparty na Linuxie (Arch Linux), zaprojektowany jako bezpośrednia alternatywa dla Windows 11. Nie kolejna dystrybucja Linuxa — to system który ma wyglądać i działać inaczej niż cokolwiek wcześniej, być przyjazny dla wszystkich i eliminować wszystko co irytuje w Windowsie: reklamy, telemetrię, bloatware, planowe postarzanie sprzętu, lock-in do ekosystemu.

**Cel nadrzędny:** Pokonać Windowsa 11 wśród młodych dorosłych do 30 lat.

---

## Stack techniczny

| Warstwa | Technologia |
|---|---|
| Baza systemu | **Arch Linux** |
| Compositor / GUI | **Wayland + Hyprland** |
| Installer / Onboarding | **Calamares** |
| Menedżer plików | **Nautilus** |
| Przeglądarka | **Firefox** |
| Dev setup | **ADM-CLI** (https://github.com/CrystalGamesStudio/ADM-CLI) via curl |
| Terminal (dev persona) | **tmux** |
| Sklep z aplikacjami | **Slate Store** (frontend nad Flatpak + apt + snap) |
| Kompatybilność .exe | **Proton** (Valve) |
| Kompatybilność .dmg | **Darling** (partial, z disclaimerem) |
| Kompatybilność .deb | **dpkg** (natywny) |
| Kompatybilność .tar.gz | Auto-detekcja przez Slate |
| Kompatybilność .AppImage | Natywne (auto chmod+x) |
| Touchpad | Hyprland 0.51+ wbudowane gesty |
| Wacom | libwacom + input-wacom kernel module |

---

## Repo i pliki

- **Repo:** `github.com/[owner]/slate-os`
- **Pliki planów:** `/plans/`
  - `slate-os-prd.md` — pełny PRD (wszystkie funkcje)
  - `prd-mvp.md` — okrojony PRD tylko dla MVP
  - `SLATE_MEMORY.md` — ten plik (kontekst dla Claude Code)

---

## Aktualny status

**Faza: PRD gotowy → następny krok: `/carve` (podział na fazy implementacji)**

MVP jest zdefiniowany i okrojony do absolutnego minimum. Celem jest zbudowanie działającego GUI w QEMU — to był blocker poprzedniego projektu i musi być pierwszy milestone.

---

## Co to jest MVP

MVP = dowód że Slate odpala się z działającym GUI. Poprzednia próba budowy systemu przez Adama zatrzymała się na tym etapie (terminal działał, GUI nie). MVP to potwierdzenie że ten problem jest rozwiązany.

### MVP zawiera:
- Arch Linux jako baza
- Wayland + Hyprland (auto-konfigurowany przez instalator)
- **Boot screen:** logo Slate (PNG/JPG) + animowany loader bars-style (przesuwa się i znika jak https://cliloaders.com/bars_3) — BEZ etykiety `_Starting_`
- **Login screen:** tylko input hasła + Enter (bez profilu, bez WiFi/BT, bez power buttons)
- **Pulpit:**
  - Górny pasek z live zegarem
  - Tapeta — obrazek PNG/JPG z logo Slate (dostarczy Adam)
  - Dolny pasek — klikalne ikony + launchpad (ikona apps otwiera widok wszystkich aplikacji z blur transition)
- Terminal (domyślny, np. Foot lub Kitty)
- Przycisk okna **●** (zamknij) — tylko zamknij, bez fill i minimalizuj

### MVP NIE zawiera:
Persona onboarding, Slate Store, kompatybilność plików (.exe/.dmg/.deb), auto-wykrywanie sprzętu, centrum powiadomień, WiFi/BT menu, `_AppName_` switcher, zaokrąglone rogi okien, window snapping, wielu użytkowników, szyfrowanie, firewall, search, animowane okna (domyślny Hyprland wystarczy), touchpad gesty, power buttons na loginie i wszystko inne z listy "out of scope" w prd-mvp.md.

### Definicja "MVP gotowe":
> System bootuje się w QEMU → boot screen z animowanym logo → ekran logowania (hasło + Enter) → pulpit z tapetą, górnym paskiem (live zegar) i działającym dolnym paskiem (klikalne ikony + launchpad) → terminal odpala się i działa → przycisk ● zamyka okno.

---

## Design Systemu — UI

### Ekran startowy (boot)
- Czarne tło
- Logo Slate wyśrodkowane
- Pod logo: animowany loader bars-style (przesuwa się i znika, NIE tradycyjny progress bar)
- Referencja animacji: https://cliloaders.com/bars_3
- BEZ etykiety `_Starting_` (była w projekcie ale usunięta z MVP)

### Ekran logowania
- Czarne tło
- Wyśrodkowany input hasła w stylu pill-shape
- Logowanie przez Enter
- BEZ: zdjęcia profilowego, przycisku submit, ikon WiFi/BT/power
- (W pełnej wersji post-MVP: animowana tapeta, powiadomienia, profil, WiFi/BT, power buttons, reset hasła przez ? → email)

### Górny pasek (Top Bar)
- Po lewej: ikony WiFi i Bluetooth (szybkie menu przy kliknięciu)
- Na środku: **`_AppName_`** — nazwa aktywnej aplikacji (interaktywny element)
- Po prawej: zegar live, pogoda (temperatura na dworze), bateria
- W pełni edytowalny: przeciąganie, usuwanie, dodawanie widgetów
- Opcjonalny auto-hide

### `_AppName_` — kluczowy element UI
Kliknięcie `_AppName_` otwiera **dropdown z animacją** zawierający:
1. **Input bez obramowania** — wpisz nazwę apki żeby ją zmienić
2. **Duże kwadratowe przyciski:** Force Quit, Zamknij, Minimalizuj, Maksymalizuj
3. **Opcje aplikacji:** File, Edit, View itp. (menu apki)
- Dostępny zarówno w górnym pasku jak i w oknie aplikacji
- Dotyczy też .dmg apps (macOS apps via Darling)
- Force Quit wymaga potwierdzenia

### Dolny pasek (Bottom Bar)
- Zawsze widoczny domyślnie (opcjonalny auto-hide)
- **Lewa strona:** Slate Store (domyślny, usuwalny) + open-at-login apps
- **Separator:** pionowa kreska `|`
- **Prawa strona:** ikona Apps → otwiera Launchpad
- **Wskaźniki apek:**
  - Długa kreska pod ikoną = aplikacja aktywna (używasz jej teraz)
  - Kropka pod ikoną = aplikacja widoczna/zminimalizowana ale nieaktywna

### Launchpad
- Otwiera się z blur transition (efekt rozmycia przy wejściu)
- Siatka ikon auto-dopasowuje się do rozdzielczości
- Jak macOS Sequoia

### Okna aplikacji
- Domyślnie zaokrąglone rogi
- Ostre rogi gdy zmaksymalizowane (fill)
- **Przyciski okna:** ● (oktagon) = zamknij, □ (kwadrat) = fill/unfill, ▽ (odwrócony trójkąt) = minimalizuj
- Window snapping: przeciągnięcie do krawędzi = połówki/ćwiartki ekranu

### Powiadomienia
- Pop-up powiadomienia: wyskakują na górze ekranu NA ŚRODKU
- Centrum powiadomień: wysuwa się z boku (jak Windows 10 Action Center)
- Do Not Disturb: manualny, wycisza pop-upy i dźwięk — powiadomienia trafiają do centrum bez sygnału

### Szybkie toggles w centrum powiadomień (domyślne, edytowalne):
Sieć, Wszystkie ustawienia, Bluetooth, Tryb nocny, Lokalizacja, Oszczędzanie baterii, VPN, Wycinanie ekranu, Tryb samolotowy, Pobliskie udostępnianie, Apps manager

---

## Personalizacja i wygląd

- **Motyw:** ciemny domyślnie
- **Inne motywy** (jasny, kontrast, blur/frosted glass): do pobrania ze Slate Store
- **Blur/frosted glass:** opcjonalny, konfigurowalny suwakiem przezroczystości
- **Tapety:** kilka domyślnych do wyboru w onboardingu, PNG/JPG
- **Ustawienia:** wzorowane na macOS (boczny panel z kategoriami)

---

## Persony onboardingowe (13 person, post-MVP)

Podczas onboardingu w Calamares user wybiera personę. Slate instaluje odpowiednie aplikacje i optymalizuje system.

| Persona | Kluczowe apki | Optymalizacja |
|---|---|---|
| **Zwykły** | Firefox, terminal, Nautilus | As-fast-as-possible |
| **Gamer** | Game Center (Steam/Heroic/Lutris — user wybiera), Discord, MangoHud, Proton-GE | CPU governor performance, GPU drivers, GameMode |
| **Programista** | ADM-CLI via curl → IDE (user wybiera osobno), tmux | Swap pod kompilację, Docker |
| **Grafik** | Krita, GIMP, Inkscape, Darktable, Blender; Affinity via Proton (user wybiera) | GPU accel, HiDPI, ICC color profiles |
| **Pisarz** | LibreOffice Writer, Obsidian, Typora, FocusWriter, Zotero, Notion | Focus mode, Night Light, auto-backup |
| **Streamer/Twórca** | OBS, DaVinci Resolve / Kdenlive, webcam setup | GPU encoding, niskie latency |
| **Muzyk/Producent** | LMMS, Ardour, Carla | JACK audio, niskie latency |
| **Student** | Okular, Anki, Zotero, Teams/Zoom | Balans wydajności |
| **Biznes** | LibreOffice Suite, Thunderbird, Teams, Calendar | Stabilność |
| **Fotograf** | Darktable, RawTherapee, import z aparatu | RAM pod RAW, HiDPI |
| **Rozrywka** | Spotify, VLC, Firefox | Maksymalnie prosto |
| **Digital Nomad** | VPN, Notion, komunikatory | Lekki, bateria |
| **Dziecko** | Zwykły + filtry treści + limity czasowe | Brak dostępu do ustawień |

**Ważne o Programista:** ADM-CLI instaluje środowisko deweloperskie (Node.js, npm/pnpm, git, gh CLI, SSH, dotfiles). IDE i dodatkowe narzędzia Slate pyta osobno po ADM-CLI.

---

## Domyślne aplikacje systemowe (wszystkie persony)

Firefox, Transmission, Remmina, Rhythmbox, Totem (Wideo), Shotwell, Document Viewer (Evince), Document Scanner (Simple Scan), Eye of GNOME, Text Editor (Gedit), Calculator, Calendar, System Monitor, Disk Utility, Archive Manager (File Roller), Screenshot, Characters, Font Viewer, Logs, Password & Keys (Seahorse), Startup Applications, Software & Updates, Software Updater, Additional Drivers, Language Support, Nautilus, Terminal

---

## Kluczowe decyzje produktowe

| Temat | Decyzja |
|---|---|
| Telemetria | Zero danych użytkownika — tylko auto error reports do dewelopera |
| Aktualizacje | User potwierdza przed pobraniem, instalacja w tle, możliwość rollback |
| Konta | Max 3 konta na komputerze |
| Konto Dziecka | Zarządzane z konta rodzica bez admina |
| Onboarding | Po instalacji w Calamares, przed pierwszym pulpitem; język/region manualnie, klawiatura auto+potwierdzenie |
| Dual-boot | Automatyczna detekcja Windows w Calamares |
| Instalacja | Wymaga internetu (offline niemożliwe) |
| Szyfrowanie dysku | Opcjonalne podczas instalacji |
| Firewall | Wbudowany, domyślnie włączony |
| Skróty | Ctrl-based domyślnie, Cmd-based opcjonalnie |
| Screenshot | Jak Ubuntu, zapisuje do Pobranych automatycznie |
| Nagrywanie ekranu | Wbudowane, switch audio (mikrofon/system) |
| VPN | Toggle → Slate Store, NordVPN jako pierwsza propozycja |
| Menedżer haseł | Ze Slate Store (nie wbudowany) |
| Drukarki | Ze Slate Store (nie wbudowane) |
| Accessibility | Widoczne w Settings, do pobrania ze Store |
| Night Light | Konfigurowalny harmonogram (auto wschód/zachód słońca) |
| Pobliskie udostępnianie | AirDrop-style przez Bluetooth |
| Bluetooth audio | Out-of-the-box |
| Touchscreen | Wspierany, wirtualna klawiatura auto |
| Gesty touchpada | 2 palce = scroll, 3 palce = Mission Control |
| Wirtualne pulpity | Jak macOS Mission Control — swipe, podgląd, drag & drop |
| Prawy klik pulpitu | Menu kontekstowe (zmiana tapety, nowy folder, ustawienia) |
| Model biznesowy | Darmowy (consumer) → płatny Server (firmy) → docelowo max $25 USD |

---

## Slate Store

- Frontend nad Flatpak + apt + snap — user widzi jeden sklep
- Kategorie jak App Store (Polecane, Gry, Narzędzia, itp.)
- Brak ocen i recenzji
- Affinity: bezpłatne (Canva); inne płatne apki → redirect do strony producenta

---

## Pliki designu (referencje UI)

W repo znajdują się 3 pliki PDF z projektami ekranów:
- `slate-starting.pdf` — boot screen (logo + loader)
- `slate-login.pdf` — ekran logowania
- `slate-main-screen.pdf` — główny pulpit

Kluczowe szczegóły z projektów:
- Styl nazw w `_podkreśleniu_` (np. `_Terminal_`, `_Login_`, `_Starting_`) to identyfikatory UI, nie zwykłe etykiety
- Górny pasek ma strukturę: [WiFi][BT] ... [AppName] ... [zegar][temp][bateria]
- Dolny pasek ma separator `|` oddzielający apki od systemowych ikon
- Wskaźniki apek pod ikonami: kreska = aktywna, kropka = nieaktywna

---

## Historia projektu

- Adam wcześniej próbował zbudować podobny system (BETA), ale projekt upadł gdy GUI nie chciało wystartować — terminal działał, compositor/GUI nie
- Slate jest planowanym, dopracowanym sukcesorem tamtego projektu
- Dlatego MVP koncentruje się NA GUI — to jest pierwsza rzecz do udowodnienia

---

## Workflow pracy

1. Planowanie: Claude.ai (chat) — `/ask` → `/blueprint` → `/carve` → `/dispatch`
2. Implementacja: **Claude Code** — na podstawie planów z `/plans/`
3. Testowanie: QEMU jako główny emulator

---

## Linki

- ADM-CLI: https://github.com/CrystalGamesStudio/ADM-CLI
- Loader animation reference: https://cliloaders.com/bars_3
- Repo: github.com/[owner]/slate-os