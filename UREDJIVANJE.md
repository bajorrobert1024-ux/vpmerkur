# Dodavanje fotografija i uređivanje kataloga

Otvorite `js/catalog.js` u editoru teksta. Stranica koristi ovaj fajl direktno, bez buildovanja. `catalog.json` je početna kopija podataka za uvoz u druge sisteme; njegovo samostalno menjanje ne menja sajt. Ako ga koristite za uvoz, držite ga usklađenim sa JavaScript katalogom.

## Fotografije

U folder `assets/proizvodi/` dodajte svoje JPG, PNG, WebP ili AVIF fajlove. Nisu uključene niti generisane fotografije ili ilustracije proizvoda. `image: ""` u svakoj stavci ostavlja potpuno prazan prostor.

Pronađite proizvod po `id` ili `name` i promenite samo polje `image`, na primer:

```js
"image": "assets/proizvodi/knjaz-milos.jpg"
```

Putanja je relativna u odnosu na `index.html`, ne na `js/catalog.js`. Imena fajlova treba da se poklapaju, uključujući velika i mala slova. Preporučuje se kadar sa svetlom ili transparentnom pozadinom; `object-fit: contain` čuva ceo proizvod bez odsecanja. Isti resurs automatski se prikazuje na kartici, detaljima, u korpi i u pregledu upita.

Prostori za fotografije na početnom promotivnom baneru i kategorijama takođe su prazni. Oni se uređuju odvojeno u funkciji `home()` u `js/app.js`; nisu povezani sa jednom stavkom kataloga.

## Cene

Cene unosite kao brojeve u dinarima, sa tačkom kao decimalnim separatorom. Ovo je primer formata, a ne preporučena cena:

```js
"price": 149.99,
"oldPrice": null,
"stock": true
```

- `price: null`: „Cena na upit”. Nemojte koristiti nulu za nepoznatu cenu.
- `oldPrice: 179.99`: stara cena, prikazuje se samo ako je veća od nove.
- `stock: null`: „Dostupnost na upit”; `true`: „Na stanju”; `false`: „Po porudžbini”.
- Unesite potrošačke cene sa PDV-om; prikaz to navodi uz objavljenu cenu.

Korpa sabira poznate cene. Ako neki artikal nema cenu, ukupno ostaje „Po potvrdi ponude”. Dostava se ne izmišlja i ostaje „Po dogovoru”.

## Pakovanja i artikli

Izmenite `volume` (npr. `"0,5 l"`) i `pack` (npr. `"Limenka"`) kada potvrdite tačnu deklaraciju. Za različita pakovanja napravite zasebne objekte sa različitim `id` vrednostima.

Svaki proizvod ima sledeća polja:

```js
{
  "id": "jedinstveni-id-proizvoda",
  "name": "Naziv proizvoda",
  "brand": "Brend",
  "category": "voda",
  "subcategory": "id-postojece-potkategorije",
  "volume": "",
  "pack": "",
  "price": null,
  "oldPrice": null,
  "image": "",
  "adult": false,
  "alcohol": false,
  "description": "Opis prema potvrđenoj deklaraciji.",
  "stock": null
}
```

`category` i `subcategory` moraju odgovarati postojećim ID vrednostima u odeljku `categories` istog fajla. `id` mora biti jedinstven i stabilan jer ga koriste sačuvana korpa, favoriti i linkovi.

Za alkoholna pića koristite `adult: true, alcohol: true`. Za energetska pića sa preporukom punoletstva koristite `adult: true, alcohol: false`. Za izričito bezalkoholne varijante unosite podatke prema deklaraciji. Ne menjajte oznake uzrasta samo da biste uklonili upozorenje.

## Nazivi i podaci koje treba potvrditi

Lista je prepisana iz dostavljenog asortimana. Kod generičkih stavki (sorte vina, vrste nektara, velika pakovanja) nisu izmišljeni proizvođači i zapremine. Zanatske kombinacije i sporni nazivi imaju opis da je potrebna potvrda. Pre objavljivanja zamenite takve stavke stvarnim SKU proizvodima i njihovim deklaracijama.

## Logotip, boje i kontakti

- Zamenite `assets/logo.svg` i `assets/logo-dark.svg` originalnim vektorskim logotipima, uz zadržavanje imena fajlova, ili promenite putanju u funkciji `logo()`.
- Osnovne boje su u `:root` na početku `css/styles.css`: `--green`, `--green-dark`, `--lime`, `--orange`.
- Kontakti, dostava i uslovi nalaze se u funkciji `infoModal()` u `js/app.js`; trenutno nema izmišljenih telefona ili adresa.
- Tekstovi početne stranice su u funkciji `home()`, a footer u funkciji `footer()`.

## Provera nakon uređivanja

Ponovo otvorite ili osvežite `index.html`. Proverite karticu proizvoda, detalje i korpu, desktop i mobilni prikaz. Preporučuje se provera u novoj privatnoj sesiji zbog prethodno sačuvane korpe i potvrde punoletstva. Ako menjate ID vrednosti artikala, stare stavke koje više ne postoje automatski se uklanjaju iz sačuvane korpe pri učitavanju.
