# TS02 – Vanilla TypeScript + HTML/CSS (Playlist Builder)

I denna workshop bygger du en enkel **Playlist Builder** i webbläsaren.  
Användaren fyller i en låttitel och längd, och listan uppdateras med total speltid.

> **Tid:** ~3–4 timmar  
> **Mål:** öva på DOM-typer, eventhantering, arrays, funktionstyper och enkel rendering.

---

## Steg 1 – Skapa projektet

1. Skapa en ny mapp `ts-playlist` och öppna den i VS Code.
2. Initiera npm:

```bash
npm init -y
```

3. Installera TypeScript:

```bash
npm i -D typescript
```

---

## Steg 2 – Skapa `tsconfig.json`

```bash
npx tsc --init
```

Ändra följande i `tsconfig.json`:

```json
"rootDir": "./src",
"outDir": "./dist",
"strict": true,
"lib": ["ES2020", "DOM"]
```

`lib: ["DOM"]` behövs för att TypeScript ska känna igen alla DOM-typer (`document`, `HTMLElement`, osv).

---

## Steg 3 – HTML & CSS

Skapa en **`index.html`** i projektroten. Lägg in:

```html
<!DOCTYPE html>
<html lang="sv">
  <head>
    <meta charset="utf-8" />
    <title>Playlist Builder</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <h1>Playlist Builder</h1>

    <form id="track-form">
      <input id="title" type="text" placeholder="Titel" required />
      <input id="duration" type="text" placeholder="mm:ss" required />
      <button type="submit">Lägg till</button>
    </form>

    <ul id="list"></ul>
    <p>Total tid: <span id="total">0:00</span></p>

    <script type="module" src="dist/main.js"></script>
  </body>
</html>
```

Skapa en enkel **`styles.css`** för lite styling (valfritt).

---

## Steg 4 – Första TypeScript-filen

1. Skapa mappen `src/` och filen `main.ts`.
2. Testa att skriva:

```ts
console.log("Playlist Builder startar...");
```

Bygg och kör:

```bash
npx tsc
```

Öppna `index.html` i webbläsaren och kontrollera konsolen.

---

## Steg 5 – Hämta element med rätt typer

Hämta DOM-elementen från formuläret:

```ts
const form = document.querySelector("#track-form") as HTMLFormElement;
const titleInput = document.querySelector("#title") as HTMLInputElement;
const durationInput = document.querySelector("#duration") as HTMLInputElement;
const list = document.querySelector("#list") as HTMLUListElement;
const totalEl = document.querySelector("#total") as HTMLSpanElement;
```

---

## Steg 6 – Skapa en typ för en låt

En låt behöver:

- Titel (string)
- Längd i sekunder (number)

Skapa en **type alias** `Track` och en array `tracks: Track[] = []`.

---

## Steg 7 – Hjälpfunktioner

Skriv två funktioner:

1. `parseDuration("3:45"): number | null` → returnerar antal sekunder eller null.
2. `formatDuration(225): string` → returnerar `"3:45"`.

---

## Steg 8 – Hantera submit-event

Lägg till en event-lyssnare på formuläret:

```ts
form.addEventListener("submit", (e) => {
  e.preventDefault();
  // 1. Läs titel och längd
  // 2. Använd parseDuration
  // 3. Skapa ett Track-objekt
  // 4. Lägg till i tracks-arrayen
  // 5. Töm formuläret
  // 6. Anropa render()
});
```

---

## Steg 9 – Rendera listan

Skriv en `render()`-funktion som:

- Tömmer listan
- Loopa igenom `tracks` och skapa `<li>` med titel + längd
- Räkna ut total tid och visa i `#total`

---

## Steg 10 – Extra-utmaningar

- Lägg till genre som en **union type** (`"pop" | "rock" | "other"`)
- Lägg till favorit-checkbox → visa ⭐ i listan om true
- Ta bort låtar (lägg till en 🗑️-knapp per `<li>`)

---

## Steg 11 – Success ✅

När du är klar kan du:

- Kompilera TypeScript till JavaScript och använda det i HTML
- Hämta och typa DOM-element (`HTMLFormElement`, `HTMLInputElement`, …)
- Skriva funktioner med parametrar, returtyper och type aliases
- Hantera events och rendera dynamiskt i DOM
- Arbeta med state i en array och uppdatera gränssnittet

---

## Steg 12 – Extra-utmaning: React-version

Du har nu byggt din Playlist Builder i **vanilla TypeScript**.  
Som extra-utmaning kan du bygga **samma projekt i React med TypeScript** och jämföra skillnaderna.

### 1. Skapa ett nytt React-projekt med Vite

```bash
npm create vite@latest ts-playlist-react -- --template react-ts
cd ts-playlist-react
npm install
npm run dev
```

### 2. Skapa komponenter

- `App.tsx` kan hålla state för dina låtar (`Track[]`).
- En **Form-komponent** för att lägga till en låt.
- En **List-komponent** för att visa alla låtar.

### 3. Använd TypeScript i React

- Skapa en `type Track` med samma struktur som i vanilla-versionen.
- Typa props till dina komponenter (`tracks: Track[]`, `onAdd(track: Track)`, osv).
- Typa eventhandlers:
  - `onSubmit={(e: React.FormEvent<HTMLFormElement>) => ...}`
  - `onChange={(e: React.ChangeEvent<HTMLInputElement>) => ...}`
- Använd useState:
  - const [tracks, setTracks] = useState<Track[]>([]);

### 4. Jämför med vanilla-versionen

- Hur känns det att hantera state i React jämfört med en global array?
- Hur syns typerna i props och state?
- Är det lättare eller svårare att hålla koden organiserad?

---

## Vidare läsning

- [Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)
- [DOM Events (MDN)](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)
- [TypeScript + DOM guide](https://www.typescriptlang.org/docs/handbook/dom-manipulation.html)
