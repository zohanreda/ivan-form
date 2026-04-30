# 📋 Ivan Mastermind — Brain dump form

Standalone HTML form dla **Ivana** (informatyka motron.pl) żeby przekazał wiedzę do AI assistanta.

## Live URL

🌐 **[https://zohanreda.github.io/ivan-form/](https://zohanreda.github.io/ivan-form/)**

## Otwarcie

Po prostu otwórz link powyżej w Chrome — formularz działa offline po wczytaniu (zero backend, dane w localStorage przeglądarki).

Albo dwuklik plik `index.html` lokalnie.

## Funkcje

- ☀ / 🌙 Toggle dzień / noc
- 🧪 Panel testowy (draggable) — edytor nagród + symulatory progress
- 📎 Załączniki per pytanie (Base64 w localStorage, max 500 KB/plik)
- 🚫 „Bez sensu" — Ivan może oznaczyć pytanie jako pomijane
- 🎁 Nagrody przy 50% i 100% (współrzędne GPS w Redzie)
- 🔥 Toasty motywacyjne 25% / 75%
- 🎭 Bonus żarty co 6 odpowiedzi (mix PL / RU / UA)
- 📏 Auto-grow textarea + ręczny resize corner
- ⬇ Pobierz jako Markdown
- Auto-zapis w localStorage

## Statystyki

- **18 sekcji**, **~165 pytań**
- 5 sekcji krytycznych ⭐: Production safety / Backup + współpraca / No-go zones / Data flow / Mental model
- Czas wypełnienia normalnie: **~8-10h** (3-4 wieczory)

## Architektura

- Single HTML file (CSS + JS inline)
- No backend, no dependencies (poza Google Fonts CDN)
- localStorage jako jedyne miejsce zapisu
- Ivan po wypełnieniu klika **„📤 Prześlij Krystianowi"** → kopiuje treść do schowka albo pobiera plik `.md`

## Test workflow

Patrz `TEST.md` — checklist 30+ pozycji do sprawdzenia przy każdej zmianie.

## Source of truth

Główna wersja pliku jest w prywatnym repo `zohanreda/autocrm` w folderze `tools/ivan-form/`. Ten public repo to deploy do GitHub Pages — synchronizowany ręcznie albo przez skrypt deploy.

---

**Maintainer**: Krystian Reda · [zohan.reda@gmail.com](mailto:zohan.reda@gmail.com) · motron.pl
