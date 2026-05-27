# Lekcija 2 — addEventListener

## Što je event?

Do sada se tvoj JS izvršavao odmah kad se stranica učitala — jednom, od vrha prema dnu, gotovo.

**Event** je nešto što se dogodi:
- Korisnik klikne gumb → `click`
- Korisnik upiše tekst → `input`
- Korisnik pošalje formu → `submit`

`addEventListener` kaže JS-u: **"čekaj na ovaj event, a kad se dogodi — izvrši ovu funkciju."**

---

## Osnovna sintaksa

```javascript
const gumb = document.querySelector("#mojGumb");

gumb.addEventListener("click", () => {
    console.log("Kliknut!");
});
```

Format je uvijek isti:
```
element.addEventListener("vrstaEventa", () => { /* tvoj kod */ });
```

---

## Click event

```javascript
const gumb = document.querySelector("#gumb");
const prikaz = document.querySelector("#prikaz");
let brojKlikova = 0;

gumb.addEventListener("click", () => {
    brojKlikova++;
    prikaz.textContent = `Kliknuo si ${brojKlikova} puta.`;
});
```

**Varijabla `brojKlikova` je IZVAN event listenera** — tako pamti vrijednost između klikova.

---

## Input event — čita što korisnik tipka

```javascript
const input = document.querySelector("#imeInput");
const prikaz = document.querySelector("#prikaz");

input.addEventListener("input", () => {
    prikaz.textContent = `Zdravo, ${input.value}!`;
});
```

- `input.value` = što je trenutno upisano u polju
- `input` event se okida **svaki put** kad korisnik upiše ili obriše znak

---

## Submit event — forma bez reloada

```javascript
const forma = document.querySelector("#forma");

forma.addEventListener("submit", (event) => {
    event.preventDefault(); // ← OBAVEZNO! Spriječi reload stranice
    console.log("Poslano!");
});
```

### Zašto `event.preventDefault()`?

Bez njega — browser osvježi stranicu i izgubi sve.  
S njim — stranica ostaje, ti obradiš podatke u JS-u.

---

## Čitanje inputa — pazi na tip!

`input.value` je uvijek **string**, čak i za `type="number"`:

```javascript
const a = document.querySelector("#broj1").value; // "10" — string!
const b = document.querySelector("#broj2").value; // "20" — string!

console.log(a + b);              // "1020" ← POGREŠNO!
console.log(parseFloat(a) + parseFloat(b)); // 30 ← ISPRAVNO
```

**`parseFloat()`** pretvara string u decimalni broj.  
**`parseInt()`** pretvara string u cijeli broj.

---

## Rezime

```javascript
// Click
el.addEventListener("click", () => { });

// Input — svako tipkanje
input.addEventListener("input", () => {
    const vrijednost = input.value;
});

// Submit forme
forma.addEventListener("submit", (e) => {
    e.preventDefault(); // obavezno!
});

// Pretvaranje u broj
parseFloat(input.value)  // decimalni broj (npr. 3.14)
parseInt(input.value)    // cijeli broj (npr. 3)
```

---

## ✏️ Otvori vjezba.html i riješi zadatke

---

## Zaglavljen si?

**Event listener ne reagira na klik**
→ Provjeri je li `<script>` na dnu `<body>` taga, a ne u `<head>`
→ Provjeri konzolu — ima li null ili grešku?

**Forma osvježava stranicu**
→ Zaboravio si `event.preventDefault()` — mora biti prva linija u submit listeneru.

**Zbrajanje daje "1020" umjesto 30**
→ Zaboravio si `parseFloat()`. `input.value` je uvijek string!
