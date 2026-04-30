# Test checklist — IVAN_MASTERMIND.html

Lista do **manualnego sprawdzenia** za każdym razem gdy modyfikujemy plik. Jak wszystko `[x]` przechodzi → bezpieczna do wysłania Ivanowi.

**Sposób:** otwórz `IVAN_MASTERMIND.html` w Chrome, wykonaj każdy krok, zaznacz wynik.

## ⚠ ZAWSZE PRZED TESTEM ZROBIĆ

```bash
# 1. JS syntax check (catch literal errors)
sed -n '/^<script>$/,/^<\/script>$/p' IVAN_MASTERMIND.html | sed '1d;$d' > /tmp/ivan.js
node --check /tmp/ivan.js

# 2. Sprawdź duplikaty + wywołania init
grep -c 'function renderTabs' IVAN_MASTERMIND.html  # powinno być 1
grep -c 'function renderContent' IVAN_MASTERMIND.html  # 1
grep -c '^renderTabs();' IVAN_MASTERMIND.html  # 1 (wywołanie init)
grep -c '</script>' IVAN_MASTERMIND.html  # 1

# 3. Otwórz w FRESH tab Chrome (Ctrl+Shift+N — incognito żeby ominąć cache)
open -a "Google Chrome" --args --new-window "file://$(pwd)/IVAN_MASTERMIND.html"

# 4. DevTools → Console: szukaj czerwonych errorów
```

## 🔥 HISTORYCZNE BUGI których uniknąć

- **Init init init** — przy każdej refaktoryzacji JS upewnij się że końcowy blok INIT (`renderTabs(); renderContent(); updateProgress(); loadTestPanelFields();`) jest tam gdzie był. Jeden commit usunął te 4 linie razem z duplikatem THEME_KEY → cała strona pusta.
- **Hardcoded `#fff` w :focus** — zawsze `var(--bg2)` żeby reagowało na dark mode.
- **`window.scrollTo(0)` w switchTab** — usunięto, bo Krystian woli zostać tam gdzie był.

---

## 🌞 LIGHT MODE — wizualka

- [ ] Strona ładuje się bez błędów (DevTools → Console: brak czerwonych)
- [ ] Header gradient (niebieski → fiolet) widoczny
- [ ] Intro tekst czytelny (czarny tekst na białym tle)
- [ ] Toggle dark/light w prawym górnym rogu — widoczny, ikonki ☀ 🌙
- [ ] Sidebar tabs (lewa kolumna) — białe tło, ciemny tekst, niebieski hover
- [ ] Aktywna zakładka — niebieskie tło, biały tekst
- [ ] Right sidebar (sterownik PCB) — ciemny gradient z zieloną płytką
- [ ] Komponenty PCB ledwo widoczne (opacity 0.08) gdy 0% wypełnione
- [ ] Progress card (białe tło) — duży niebieski numer + bar

## 🌙 DARK MODE — wizualka

- [ ] Klik toggle → smooth transition do dark mode
- [ ] Body tło ciemne (#0f172a)
- [ ] Tekst jasny (#f1f5f9)
- [ ] Sidebar tabs — ciemne tło, jasny tekst
- [ ] Main panel — ciemny ale nie czarny (#1e293b)
- [ ] Linki w intro — niebieski jasny (#60a5fa)
- [ ] Toggle: biały kursor po lewej (light) → żółty kursor po prawej (dark)
- [ ] Progress card — ciemne tło
- [ ] Right sidebar PCB — bez zmian (zawsze ciemny)
- [ ] Theme persists po reload (localStorage)

## ✏ POLA INPUT — TEKST WIDOCZNY (krytyczny bug który był)

**LIGHT MODE:**
- [ ] Pole TEXT: kliknij, pisz → widać **czarny tekst** od razu (nie kropki!)
- [ ] Pole TEXTAREA: kliknij, pisz → widać tekst od razu
- [ ] Po focus: tło zmienia się na białe, tekst zostaje czarny (czytelny)
- [ ] Placeholder: szary (#9ca3af), znika po wpisaniu

**DARK MODE:**
- [ ] Pole TEXT: kliknij, pisz → widać **jasny tekst** na ciemnym tle (nie biały na białym!)
- [ ] Pole TEXTAREA: kliknij, pisz → widać tekst od razu
- [ ] **Po focus: tło NADAL ciemne** (var(--bg2), nie #fff!) + tekst jasny — czytelny
- [ ] Placeholder: szary jaśniejszy
- [ ] Caret (kursor): niebieski (akcentny)

**SELECT:**
- [ ] Light: tło jasne, tekst ciemny
- [ ] Dark: tło ciemne, tekst jasny
- [ ] Dropdown options: kontrast OK (background, color z theme)

**RADIO buttons:**
- [ ] Klik → zaznaczają się
- [ ] Hover → border zmienia się na niebieski
- [ ] Light/dark mode: tło reaguje na theme

## 📍 NAVIGACJA — SCROLL ZACHOWANIE (krytyczny bug który był)

- [ ] Otwórz długą sekcję (np. „Bezpieczeństwo" — 11 pytań)
- [ ] Przewiń w dół do ostatniego pytania
- [ ] Klik na inną zakładkę w sidebar (np. „Wizytówka")
- [ ] **Scroll page NIE skacze do góry** — zostaje tam gdzie byłeś
- [ ] Aktywna zakładka się zmienia
- [ ] Treść w main się zmienia
- [ ] Sidebar pozostaje sticky widoczny

## 💾 AUTO-SAVE & PERSISTENCE

- [ ] Wpisz cokolwiek w pole TEXT
- [ ] Mały tekst „✓ zapisano" pojawia się na 1.5s w footer
- [ ] Refresh strony (F5)
- [ ] Wpisana wartość ZOSTAJE
- [ ] Wpisz coś, otwórz inną zakładkę, wróć → wartość ZOSTAJE
- [ ] Badge w sidebar `X/Y` aktualizuje się przy każdym wpisaniu

## 🎨 ANIMACJA STEROWNIKA PCB

- [ ] Przy 0% wypełnione: tylko ścieżki na płytce (zielone linie), komponenty prawie niewidoczne
- [ ] Wypełnij 1 pole → 1 komponent „dolatuje" (animacja install — opacity + scale + rotate)
- [ ] Counter „X / 40 komponentów wlutowanych" rośnie
- [ ] Przy 50% wypełnione: ~20 komponentów widocznych
- [ ] Przy 100%: wszystkie 40 komponentów + dioda LED świeci ZIELONO z pulsem
- [ ] Animacja smooth, nie skacze

## 🎉 CONFETTI & MILESTONES

**Test 50%:**
- [ ] Wypełnij dokładnie połowę pytań
- [ ] **Confetti wystrzela** (różne kolory, gravity)
- [ ] Po 700ms otwiera się **modal nagrody**:
  - [ ] Badge „🎁 50% — POŁOWA DROGI"
  - [ ] Tytuł
  - [ ] Współrzędne GPS (placeholder lub realne)
  - [ ] Przycisk „🗺 Otwórz w Google Maps"
  - [ ] Opis miejsca + opis nagrody
- [ ] Modal zamykasz → milestone w sidebar zaznaczony jako unlocked (żółty)
- [ ] Klik na milestone w sidebar → modal otwiera się ponownie

**Test 100%:**
- [ ] Wypełnij wszystkie pytania
- [ ] **Confetti × 2 (więcej particles)**
- [ ] Modal „🏆 100% — META OSIĄGNIĘTA"
- [ ] Przycisk „📤 Prześlij Krystianowi" w footer **zaczyna pulsować** (glow animation)

**Persistence:**
- [ ] Refresh strony — milestone pozostaje unlocked
- [ ] Confetti NIE wystrzeliwa drugi raz (zapamiętane w localStorage)

## 📤 EXPORT & SUBMIT

- [ ] Klik „⬇ Pobierz" → pobiera plik `ivan_brain_dump_YYYY-MM-DD.md`
- [ ] Plik zawiera wszystkie sekcje + wpisane odpowiedzi
- [ ] Puste pytania mają `_(brak odpowiedzi)_`
- [ ] Klik „📤 Prześlij Krystianowi" → modal z gotowym tekstem
- [ ] „📋 Skopiuj do schowka" → Toast „Skopiowano"
- [ ] „📧 Otwórz w mailu" → otwiera default mail z subject + body

## 📱 RESPONSIVE

**Tablet (~900px wide):**
- [ ] Right sidebar (PCB) **znika** lub przesuwa się
- [ ] Sidebar tabs zostaje
- [ ] Form pola pełnej szerokości

**Mobile (~400px wide):**
- [ ] Sidebar tabs znika (lub jest collapsable)
- [ ] Main panel pełnej szerokości
- [ ] Theme toggle wciąż widoczny w prawym górnym rogu
- [ ] Footer się zawija (flex-wrap)

## 🔧 EDGE CASES

- [ ] Działa w **Chrome, Safari, Firefox** (testuj minimum 2)
- [ ] Działa **offline** (nie wymaga internetu — tylko Google Fonts CDN)
- [ ] Działa gdy **localStorage zablokowany** (np. tryb prywatny — pojawi się błąd ale strona nadal się ładuje)
- [ ] Backspace w pole / Ctrl+Z działa
- [ ] Copy-paste w pole działa
- [ ] Tab key → przeskakuje między polami w kolejności

## 🐛 KNOWN BUGS / OGRANICZENIA

- [ ] Modal nagrody — Krystian musi wpisać REALNE współrzędne i opis nagrody w sekcji `const REWARDS` (TODO komentarze w kodzie)
- [ ] Photo upload pól typu `photo` / `file` — nie wysyła plików nigdzie (tylko placeholder, w realnym CRM Iwana będzie inaczej)

---

## Uruchomienie

```bash
open -a "Google Chrome" "file://$(pwd)/IVAN_MASTERMIND.html"
```

Albo dwuklik plik w Finder.

## Co po teście

✅ Wszystko `[x]` → wysyłaj Ivanowi
❌ Cokolwiek `[ ]` → fix + retest

---

**Wersja testu:** 1.0 (2026-04-28)
**Po każdej istotnej zmianie pliku:** zaktualizuj ten plik o nowe testy.
