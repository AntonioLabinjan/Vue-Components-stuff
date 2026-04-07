# Zadatak za vježbu: Vue Task Tracker

**Cilj:** Izraditi modularnu aplikaciju za upravljanje zadacima koja koristi hijerarhiju komponenti, dvosmjernu komunikaciju (props & emits), validaciju podataka te fleksibilne slotove za prikaz sadržaja.

### Specifikacija:

1.  **`TaskCard.vue` (Pojedinačni prikaz)**:
    * **Props**: Mora primati `naslov` (string, obavezan) i `prioritet` (broj, zadana vrijednost 1) koristeći `defineProps`.
    * **Emits**: Sadrži tipku "Završi" koja klikom šalje signal (`emit`) roditelju da je zadatak gotov.
    * **Slot**: Koristi `<slot>` element za prikaz opcionalnog opisa zadatka, uz definiran "zadani sadržaj" (fallback) ako opis nije poslan.

2.  **`AddTask.vue` (Unos podataka)**:
    * Koristi **reaktivne varijable** (`ref`) i `v-model` za povezivanje polja forme (naslov, opis, prioritet).
    * **Emits**: Prilikom klika na "Dodaj", komponenta mora poslati cijeli **objekt** s podacima novog zadatka roditeljskoj komponenti.

3.  **`TaskList.vue` (Lista i kôordinacija)**:
    * **Props**: Prima niz objekata `tasks` uz obaveznu **validaciju tipa podataka**.
    * Pomoću `v-for` direktive ispisuje `TaskCard` za svaki zadatak u nizu.
    * Prosljeđuje događaj brisanja (zajedno s indeksom zadatka) prema `App.vue`.

4.  **`App.vue` (Glavno stanje)**:
    * Sadrži glavni reaktivni niz zadataka.
    * Implementira metodu za **dodavanje** novih zadataka u niz (koristeći `.push()`).
    * Implementira metodu za **uklanjanje** zadataka (koristeći `.splice()`) na temelju primljenog događaja.

---
