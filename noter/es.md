# JavaScript

## Om JavaScript

Mest populære programmeringssprog

- Populært
  - [developer survey](https://insights.stackoverflow.com/survey/2019#technology)
- Effektivt
- "Simpelt"
- Behæftet med forskellige fejl

Tidligere fortolket

- nu kompileret
  - af bla [V8](https://v8.dev/)

### Selve sproget er...

#### Objektorienteret baseret på prototyper

```javascript
var Person = /** @class */ (function() {
  function Person(navn) {
    this.navn = navn;
  }
  Person.prototype.skriv = function() {
    console.log(`Jeg hedder ${this.navn}`);
  };
  return Person;
})();
var p = new Person("Mathias");
p.skriv();
```

#### Dynamisk

```javascript
let minFunktion = new Function("a", "b", "return a+b;");
console.log(minFunktion(5, 5));
```

#### Typefrit

```javascript
let a = 1;
console.log(typeof a);
a = "1";
console.log(typeof a);
```

#### Funktionsorienteret

```javascript
function findFunktion() {
  if (new Date().getMilliseconds() % 2 == 0) {
    return function(a, b) {
      return a + b;
    };
  } else {
    return function(a, b) {
      return a - b;
    };
  }
}

let f = findFunktion();
console.log(f(4, 4));
```

### Sproget bruges overalt

- Browsere
- Server/desktop
  - [node.js](https://electronjs.org/)
- App- og automatiseringskerner
  - Google Apps
  - Microsoft 365
  - mv
- Desktop
  - [Electron](https://electronjs.org/)
- Mobile
  - [Cordova](https://cordova.apache.org/)
  - [React Native](http://www.reactnative.com/)
- Hardware / IoT
  - [Esprurino](https://www.espruino.com/)

## Historie

Se [ITHistorie](http://ithistorie.cronberg.dk/?maerker=js,det_vi_husker&sortering=stigende)

Skabt af Brendan Eich i 1995 for Netscape

- Først kaldt Mocha, LiveScript

Sproget er inspireret af

- C
  - syntaks
- Scheme/Lisp
  - funktionsorienteret
- Self/Smalltalk
  - objektorienteret

## Moderne JavaScript udvikling er ikke bare lige...

- Transpiler
  - TypeScript, Babeæ
- Linters
  - ESLint
- Libraries
  - [jQuery](http://jquery.com/), [underscore.js](https://underscorejs.org/), [backbone.js](https://backbonejs.org/), [moment.js](https://momentjs.com/), [string.js](https://github.com/jprichardson/string.js)
- Frameworks
  - [React](https://reactjs.org/), [Angular](https://angular.io/), [Ember](https://emberjs.com/), [Vue](https://vuejs.org/)
- Testing
  - Unit test, integration test, continuing integration, UI test
- Module loaders / deployment / workflow
  - Webpack, Broserify, native modules

[How it feels to learn JavaScript in 2016](https://hackernoon.com/how-it-feels-to-learn-javascript-in-2016-d3a717dd577f)

## Udviklingmiljø og process

- Editor
  - [VS Code](https://code.visualstudio.com/)
  - Plugins
    - ESLint / TSLint
    - Chrome debugger
    - Live Server
    - Prettier
    - Auto Rename Tag
    - CSS Formatter
    - HTMLHint
    - HtmlTagWrap
    - Paste JSON as Code
- Package Manager
  - [NPM](https://nodejs.org/en/)
- WebServer
  - Typisk nodejs
    - [LiveServer](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) til VS Code
- Automatisering
  - [NPM Scripts](https://nodejs.org/en/)
- Bundling og minificering
  - [Webpack](https://webpack.js.org/) (eller node-pakker)
- Lintning
  - [ESLint](https://eslint.org/)
  - [TSLint](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-typescript-tslint-plugin)

## Syntaks

- C syntaks
- Instruktion
  - Semicolon (ikke nødvendigt)
- Block
  - {}
- Kommentarer
  - //
  - /\* \*/
- Upper/Lower case
- Brug af (bla) punktumnotationen ved brug af objekter

```javascript
let obj = {};
obj.navn = "Mikkel";
obj.alder = 17;
obj.Alder = 16; // ikke det samme som obj.alder

// Checker alder
if (obj.alder < 17) {
  console.log(`${obj.navn} må ikke køre bil`);
} else {
  console.log(`${obj.navn} må gerne køre bil`);
}
```

## Variabler

### Typefrit

- men internt er der typer
  - string
  - number
  - bool
  - object
  - null
  - undefinded
- værdibaserede
- immutable

### Erklæring

- Brug altid scrict mode (ES5)
  - "use strict";
    - Alt skal erklæres
    - Har ligeledes anden betydning
      - slå flere ting fra eksempelvis
        - eval()
        - delete

Erklæring med

- var
- let (ES6)
  - scope

```javascript
console.log(i); // undefinded
// console.log(j); // ikke defineret
console.log(k); // undefinded
// console.log(l); // ikke defineret

var i = 1;
let j = 2;

if (true) {
  var k = 3;
  let l = 4;
}

console.log(i); // 1
console.log(j); // 2
console.log(k); // 3
// console.log(l); // ikke defineret

const m = 1;
// m = 2;  // fejl

if (true) {
  const n = 4;
  console.log(n);
}

// console.log(n); // ikke defineret

if (true) {
  let o = 5;
  function test() {
    console.log(o); // 5 - closure
  }
  test();
}
```

### Interne typer

Primitive interne datatyper

- Number
- Boolean
- String
- undefined
- null
- object

Brug evt

- typeof
- typeof()
- instanceof

```javascript
let i = 1;
console.log(typeof i); // number
console.log(typeof i); // number

i = true;
console.log(typeof i); // boolean

i = "";
console.log(typeof i); // string

i = {};
console.log(typeof i); // object

i = new Date();
console.log(typeof i); // object
console.log(i instanceof Date); // true
```

### Operatorer

Kendt fra de fleste andre "c" sprog

```javascript
let i = 0;
console.log(i);
i += 4;
console.log(i);
i -= 2;
console.log(i);
i *= 2;
console.log(i);
i /= 2;
console.log(i);
i %= 2;
console.log(i);

/*
0
4
2
4
2
0
*/
```

### Number-typen

- 64 bit floating point tal
- benytter . som literal (100.23)
- et for stort tal bliver til Infinity og en fejl i beregning kan blive til NaN (not a number)
- brug evt
  - toFixed()
  - toString()
  - toLocaleString()
    - kan være forskel på node/browser implementation

```javascript
let a = Math.pow(11, 308);
console.log(a); // infinity
let b = 0 / 0;
console.log(b); // nan
let c = 2342.23342234;
console.log(c);
console.log(c.toFixed(2));
console.log(c.toString());
console.log(c.toLocaleString("da-DK"));
console.log(
  c.toLocaleString("da-DK", {
    maximumFractionDigits: 2
  })
);
```

#### Diverse

- Math-objektet indeholder matematik funktioner
- parseInt og ParseFloat kan bruges til typekonvertering

#### Operatorer

- \+
- \-
- \*
- \/
- \%
- \++
- \--

### Boolean-typen

- Hvem var [George Boole](https://en.wikipedia.org/wiki/George_Boole)? ;)
- Kan være true eller false
  - men false, 0 og "" evalueres til false
  - alt andet til true
  - "truthy and falsy values"
- Brug eventuelt !! operatoren

```javascript
let a = true;
let b = false;

if ("") console.log("false");
else console.log("true"); // true

if (0) console.log("false");
else console.log("true"); // true

if (null) console.log("false");
else console.log("true"); // true

if (1) console.log("false");
else console.log("true"); // false

if ("1") console.log("false");
else console.log("true"); // false

if ("true") console.log("false");
else console.log("true"); // false

console.log(!!0); //false
console.log(!!1); // true
console.log(!!null); //false
console.log(!!""); // false
console.log(!!"xyz"); // true
```

#### Operatorer

Brug altid === eller !== ved sammenligning

- == og != laver evt typekonvering og sammenligner
- === og !== checker først på typen

Andre operatorer

- \<
- \>
- \>=
- \<=
- \!
- \&&
- \||

```javascript
let a = 1;
let b = "1";

if (a == b) console.log("hvad??");

if (a === b) console.log("hvad??");
```

### String-typen

- Indeholder unicode
- Benyt " eller '
- Sammenlæg med +
- Sammenlign med === eller !==
- Escape karakterer
  - \\b (backspace)
  - \\f (formfeed)
  - \\n (newline)
  - \\r (carrige return)
  - \\t (tab)
  - \\"
  - \\'
  - \\\
  - \\uNNNN (unicode)
- String-typen indeholder naturligvis en del metoder men mange benytter diverse biblioteker
  - [Voca](https://vocajs.com/)
  - [stringjs](https://github.com/jprichardson/string.js)

```javascript
let txt = "Marx Brothers";
console.log(txt.length);
console.log(txt.toUpperCase());
console.log(txt.toLowerCase());
console.log(txt.split(" "));
console.log(txt.substring(0, 4));
console.log(txt.slice(0, -5));
console.log(txt.charAt(5));
// Pas på ES version - brug evt polyfill
console.log(txt.startsWith("Ma"));
console.log(txt.endsWith("rs"));
console.log(txt.includes("BRO"));
console.log(txt.repeat(2));
/*
13
MARX BROTHERS
marx brothers
[ 'Marx', 'Brothers' ]
Marx
Marx Bro
B
true
true
false
Marx BrothersMarx Brothers
*/
```

#### Template string

- Nem og effektv måde at danne strenge
- Benyt `..` og \${}

```javascript
let navn = "Mathias";
let beløb = 100;
console.log(navn + " har kr " + beløb);
console.log(navn + " har kr " + beløb + " og næste måned kr " + beløb * 2);
console.log(`${navn} har kr ${beløb}`);
console.log(`${navn} har kr ${beløb} og næste måned kr ${beløb * 2}`);

console.log();
console.log(
  personHTML({
    navn: "Mikkel",
    sport: ["Fodbold", "Fitness"],
    job: "Tømre"
  })
);

function personHTML({ navn, sport, job }) {
  return `<article class="person">
    <h3>${navn}</h3>
    <div>
        <div>Hobbies:</div>
        <ul>
            ${sport.map(sport => `<li>${sport}</li>`).join(" ")}
        </ul>
    </div>
    <p>Current job: ${job}</p>
 </article>`;
}

/*
Mathias har kr 100
Mathias har kr 100 og næste måned kr 200
Mathias har kr 100
Mathias har kr 100 og næste måned kr 200

<article class="person">
    <h3>Mikkel</h3>
    <div>
        <div>Hobbies:</div>
        <ul>
            <li>Fodbold</li> <li>Fitness</li>
        </ul>
    </div>
    <p>Current job: Tømre</p>
 </article>
*/
```

### Date

- Brug Date-typen til dato/tid men de fleste benytter biblioteker som eksempelvis [moment.js](https://momentjs.com/) eller lign.
  - Bemærk at måneder er 0 baseret
- Opret med new

```javascript
let d = new Date(); // nu
console.log(d.toLocaleString());
d = new Date("2019-5-14 9:10");
console.log(d.toLocaleString());
d = new Date(2019, 4, 14, 9, 10);
console.log(d.toLocaleString());

console.log(d.getMonth());
console.log(d.getDate());
console.log(d.getHours());
```

## Flow

### if

```javascript
if (true) {
}

if (true && true) {
}

if ((true && true) || true) {
}

// husk - truthy/falsy
if (!null) {
}

if (!undefined) {
}

if (!0) {
}

if (!"") {
}

// husk ===
let i = 10;
if (i === 10) {
}

if (true) {
} else {
}
```

### switch

```javascript
let y = 1;
var output = "Output: ";
switch (y) {
  case 0:
    output += "0 ";
  case 1:
    output += "1 ";
  case 2:
    output += "2 ";
  case 3:
    output += "3 ";
  case 4:
    output += "4 ";
    break;
  case 5:
    output += "5";
    break;
  default:
    console.log("Kun 1-5");
}
console.log(output); // output: 1 2 3 4
```

### for

```javascript
let s = "";
for (let i = 0; i < 10; i++) {
  s += i + " ";
}
console.log(s); // 0 1 2 3 4 5 6 7 8 9

s = "";
for (let i = 0; i < 10; i += 2) {
  s += i + " ";
}
console.log(s); // 0 2 4 6 8

s = "";
for (let i = 10; i > 0; i--) {
  s += i + " ";
}
console.log(s); // 10 9 8 7 6 5 4 3 2 1

s = "";
for (let i = 0; i < 10; i++) {
  if (i == 4) continue;
  if (i == 7) break;
  s += i + " ";
}
console.log(s); // 0 1 2 3 5 6
```

### while

```javascript
let s = "";
let i = 0;
do {
  i++;
  s += `${i} `;
} while (i < 5);
console.log(s); // 1 2 3 4 5

s = "";
i = 0;
while (i < 5) {
  i++;
  s += `${i} `;
}
console.log(s); // 1 2 3 4 5

s = "";
i = 0;
while (i < 5) {
  i++;
  s += `${i} `;
  if (i == 3) break;
}
console.log(s); // 1 2 3
```

## Funktioner

- Forskellige måder at definere en funktion
  - Frit valg (bare pas på hoisting)

```javascript
function add1(a, b) {
  return a + b;
}

let add2 = function(a, b) {
  return a + b;
};

let add3 = new Function("a", "b", "return a+b;");

let add4 = (a, b) => {
  return a + b;
};

let add5 = (a, b) => a + b;

console.log(add1(1, 1)); // 2
console.log(add2(1, 1)); // 2
console.log(add3(1, 1)); // 2
console.log(add4(1, 1)); // 2
console.log(add5(1, 1)); // 2
```

### Argumenter

- Primitive typer kopierer værdier (by value)
- Objekter kopierer referencer (be reference)

```javascript
function f1(a) {
  a = 200;
}
let b = 100;
console.log(b); // 100
f1(b);
console.log(b); // 100

function f2(dato) {
  dato.setFullYear(2000);
}
let d = new Date();
console.log(d.toLocaleDateString()); // aktuel dato
f2(d);
console.log(d.toLocaleDateString()); // aktuel dato men år = 2000
```

### Intet krav om argumenter

- En funktion er i virkeligheden et objekt (Function) med forskellige medlemmer
  - arguments

```javascript
function f1(a, b, c) {}
// helt ok
f1();
f1(1);
f1(1, 2);
f1(1, 2, 3);
f1(1, 2, 3, 4);
f1(1, 2, 3, 4, 5);
```

- Brug arguments

```javascript
function f1(a, b, c) {
  // arguments er egentlig et object - lav det om til et array
  let ar = Array.from(arguments);
  console.log(ar.join(" "));
  // men kan også bare bruge det som et object (arguments[0], arguments[1] mv)
}
f1();
f1(1); // 1
f1(1, 2); // 1 2
f1(1, 2, 3); // 1 2 3
f1(1, 2, 3, 4); // 1 2 3 4
f1(1, 2, 3, 4, 5); // 1 2 3 4 5
```

### Referencer til funktioner

```javascript
let f1 = (a, b) => a + b;
// kald
let r1 = f1(1, 1);
// reference
let r2 = f1;
let r3 = r2(1, 1);
console.log(r1); // 2
console.log(r2); // function f1
console.log(r3); // 2
```

```javascript
let a = [1, 5, 7, 10, 3, 8];
let s1 = function(a, b) {
  return a - b;
};
let a1 = a.slice(0).sort(s1);
console.log(a1.join(" ")); // 1 3 5 7 8 10

let a2 = a.slice(0).sort(function(a, b) {
  return a - b;
});
console.log(a2.join(" ")); // 1 3 5 7 8 10

let a3 = a.slice(0).sort((a, b) => a - b);
console.log(a3.join(" ")); // 1 3 5 7 8 10
```

```javascript
let add = (a, b) => a + b;
let sub = (a, b) => a - b;
let f = () => {
  let r = Math.floor(Math.random() * 10 + 1); // "tilfældigt" tal mellem 1-10
  if (r < 5) return add;
  else return sub;
};
console.log(f()(3, 2)); // 5 eller 1
```

```javascript
let f = () => {
  let r = Math.floor(Math.random() * 10 + 1); // "tilfældigt" tal mellem 1-10
  if (r < 5) return (a, b) => a + b;
  else return (a, b) => a - b;
};
console.log(f()(3, 2)); // 5 eller 1
```

### Arrow function

- Brug af => operator
- [Alonzo Church](https://en.wikipedia.org/wiki/Alonzo_Church) - lambda calculus

Regler:

- argumenter skal angives i parantes med mindre der kun er en
- hvis der kun er en operation behøves der ikke tuborgklammer eller return
- bedre håndtering af "this"

```javascript
let o1 = new Object();
o1.f1 = function() {
  console.log(this); // function
  let f2 = function() {
    console.log(this); // global/undefinded
  };
  f2();
};
o1.f1();
```

```javascript
let o1 = new Object();
o1.f1 = () => {
  console.log(this); // object
  let f2 = () => {
    console.log(this); // object
  };
  f2();
};
o1.f1();
```

### Immediate function (IIFE)

- Funktion der afvikler sig selv

```javascript
let f1 = (() => {
  console.log("f1"); // f1
})();

let f2 = (function() {
  console.log("f2"); // f2
})();

let f3 = (function(a) {
  console.log("f3 med " + a); // f3 med 1
})(1);

let f4 = (async function() {
  let response = await fetch(
    "http://vejr.cronberg.dk/service/vejr/hent?antal=1"
  );
  let json = await response.json();
  console.log(json); // vejr-data i json
})();
```

### Generators

- Speciel funktion som afventer videre afvikling
  - benyttet i iterators og callbacks

```javascript
function* loop() {
  let i = 0;
  while (i < 2) {
    i++;
    yield i;
  }
}

let r = loop();
console.log(r.next()); // { value: 1, done: false }
console.log(r.next()); // { value: 2, done: false }
console.log(r.next()); // { value: undefined, done: true }

let s = "";
for (const i of loop()) {
  s += i + " ";
}
console.log(s); // 1 2
```

### Closure

- Brugen af closures i ældre JavaScript er meget udbredt
  - indkapsler variabler

```javascript
// Global scope
let marx = ["Chico", "Harpo", "Groucho", "Gummo", "Zeppo"];
let getBrother1 = nr => {
  return marx[nr - 1];
};
console.log(getBrother1(2)); // Harpo

let getBrother2 = nr => {
  // Lokal - men defineret hver gang
  let marx = ["Chico", "Harpo", "Groucho", "Gummo", "Zeppo"];
  return marx[nr - 1];
};
console.log(getBrother2(2)); // Harpo

let getBrother3 = () => {
  // Closure
  let marx = ["Chico", "Harpo", "Groucho", "Gummo", "Zeppo"];
  return nr => marx[nr - 1];
};
console.log(getBrother3()(2)); // Harpo

let getBrother4 = (() => {
  // Closure med bedre syntaks
  let marx = ["Chico", "Harpo", "Groucho", "Gummo", "Zeppo"];
  return nr => marx[nr - 1];
})();
console.log(getBrother4(2)); // Harpo
```

## ASync

Asynkron kode i JavaScript er typisk kodet med callback-funktioner:

```javascript
const setTimeoutPromise = ms => new Promise(resolve => setTimeout(resolve, ms));

console.log("start");
setTimeoutPromise(2000).then(function() {
  console.log("slut");
});
```

Fra ES2017 er async/await dog en del af syntaksen, og det gør koden noget mere logisk og "synkron-agtig". await (som skal placeres i en async funktion) afventer at promise-objektet er afviklet. Yderligere er fejlhåndtering simplificeret til simpel try/catch.

```javascript
const setTimeoutPromise = ms => new Promise(resolve => setTimeout(resolve, ms));

async function test() {
  console.log("start");
  let t = await setTimeoutPromise(2000);
  console.log("slut");
}

test();
```

Flere promise-objekter kan eventuelt await'es med all

```javascript
const setTimeoutPromise = ms => new Promise(resolve => setTimeout(resolve, ms));

async function test() {
  console.log("start");
  const t1 = setTimeoutPromise(2000);
  const t2 = setTimeoutPromise(2000);
  await Promise.all([t1, t2]);
  console.log("slut");
}

test();
```

## Array

- Er egentlig en hash-tabel men man bruger typisk numre som nøgler
- Kan initialieres med new Array eller literals []
- Kan håndtere mange dimensioner
- En masse medlemmer - de vigtige:
  - lenght
  - push
  - pop

```javascript
let a = new Array();
a[0] = 1;
a[1] = 2;
// eller let a = [1, 2];
console.log(a.length); // 2 (sidste index + 1)

a.push(3);
console.log(a.join(" ")); // 1 2 3

let b = a.pop();
console.log(b); // 3
console.log(a.join(" ")); // 1 2
```

- Brug af de mere avancerede metoder er en super god måde at lære funktionsorienteret kode

```javascript
let a = [5, 1, 6, 7, 2, 13, 8];

// Find første
let b = a.find(function(v, i, a) {
  return v > 5;
});
// eller
b = a.find(v => v > 5);
console.log(b); // 6

// Filtrer og returner nyt array
let c = a.filter(v => v < 5);
console.log(c.join(" ")); // 1 2 3

// Manipuler hvert element og returner nyt array
let d = a.map(v => v * 2);
console.log(d.join(" ")); // 10 2 12 14 4 26 16

// Findes element
let e = a.includes(2);
console.log(e); // true

// iterer
a.forEach((v, i) => console.log(i + ": " + v)); // 0: 5, 1: 1, 2: 6 ...

let f = Array.from("mikkel");
console.log(f.join(" ")); // m i k k e l

// sorter
let g = a.slice(0); // kopi
g.sort();
console.log(g.join(" ")); // 1 13 2 5 6 7 8 (hmmm...)

g.sort((a, b) => a - b); // måske bedre med a > b ? 1 : a < b ? -1 : 0
console.log(g.join(" ")); // 1 2 5 6 7 8 13
```

Mange benytter [underscore.js](https://underscorejs.org/)

### Andre samlinger

Der findes nyere array-typer (ES2015-)

- Float32Array
- Float64Array
- Int8Array
- Int16Array
- Int32Array
- UInt16Array
- UInt32Array

Som alternativ til arrays kan du bruge Set (unikke værdier):

```javascript
const set1 = new Set([1, 2, 3, 4, 5]);
set1.add(7);
console.log(set1.size);
console.log(set1.has(2));
console.log(set1.has(6));
set1.clear();
```

eller [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) (nøgle/værdi - som Object men langt flere muligheder)

```javascript
const m = new Map();
m.set("a", 10);
m.set("b", 20);
console.log(m.size); // 2
console.log(m.get("b")); // 20
```

## RegEx

- Brug af regular expresion er indbygget
- literals er /

```javascript
let r = new RegExp("^\\d+$");
console.log(r.test("1")); // true
console.log(r.test("a")); // false

let r2 = /^\d+$/;
console.log(r2.test("1")); // true
console.log(r2.test("a")); // false
```

## Errorhandling

- Brug try/catch/finally
- Men check for undefined og NaN
  - void = undefined
  - undefined + 1 = NaN

```javascript
let o = {}; // new Object();
o.toString(); // ok

/* 
  o.tostring(); // TypeError: o.tostring is not a function
*/

try {
  o.tostring();
} catch (error) {
  console.log(error.message); // o.tostring is not a function
} finally {
  console.log("kører under alle omstændigheder"); // kører under alle omstændigheder
}
```

### Error-objektet

- [Forskellige implementationer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error) men prøv
  - message
  - name
  - stack
- Brug log.trace

```javascript
try {
  o.tostring();
} catch (error) {
  console.log(error.message); // o.tostring is not a function
  console.log(error.name); // TypeError
  console.log(error.stack); // Stack trace
}
```

### Brug throw til at smide fejl

```javascript
function add(a, b) {
  if (arguments.length !== 2) {
    throw new Error("Forkerte argumenter");
  }
}
try {
  add(1, 2); //ok
  add(1); // fejl
} catch (error) {
  console.log(error.message); // Forkerte argumenter
}
```

### Fejl bobler op

```javascript
function f1() {
  f2();
}

function f2() {
  f3();
}

function f3() {
  throw new Error("Fejl");
}

try {
  f1();
} catch (error) {
  console.log(error.message);
}
```

### Log

- Brug et godt log-framework
  - [Papertrail](https://papertrailapp.com/)
  - [trackjs](https://trackjs.com/)
  - Eller det gode gamle imagehack

```javascript
function log(app, tekst) {
  let i = new Image();
  i.src = `https://log.cronberg.dk?app=${app}&tekst=${tekst}`;
}
```

### Test

Forskellige test frameworks, tools og runners

- [Jasmine](https://jasmine.github.io/)
- [Mocha](https://mochajs.org/)
- [PhantomJS](http://phantomjs.org/)
- [Karma](http://karma-runner.github.io/)
- [Protractor](http://www.protractortest.org/)
- [Selenium](http://www.seleniumhq.org/)
- [Puppeteer](https://developers.google.com/web/tools/puppeteer/) - headless Chrome
- [Appveyor](https://www.appveyor.com) - Continuous Integration solution for Windows and Linux

## Objekter

- Objekter er i virkeligheden blot en hashtabel med unikke nøgler og tilhørende værdier
- Der er flere måder at skabe objekterne på

  - Firkantet parentes-notation
  - Punktum-notation
  - Tuborgklamme-notation

- Objekter skabes som udgangspunkt med
  - new Object()
  - {}
- De består allerede af metoder som toString() grundet sin prototype

```javascript
let o1 = new Object();
console.log(o1["toString"]()); // object Object
console.log(o1.toString()); // object Object

let o2 = {};
console.log(o2["toString"]()); // object Object
console.log(o2.toString()); // object Object
```

### Firkantet parentes-notation

```javascript
let p1 = {};
p1["navn"] = "Mathias";
p1["fødselsår"] = 2006;
p1["estimeretAlder"] = function() {
  return new Date().getFullYear() - this["fødselsår"];
};
p1["toString"] = function() {
  console.log(
    `Jeg hedder ${this["navn"]} og er ${this["estimeretAlder"]()} gammel`
  );
};
p1["toString"](); // Jeg hedder Mathias og er 13 gammel
```

### Punktum-notation

```javascript
let p2 = {};
p2.navn = "Mikkel";
p2.fødselsår = 2003;
p2.estimeretAlder = function() {
  return new Date().getFullYear() - this.fødselsår;
};
p2.toString = function() {
  console.log(`Jeg hedder ${this.navn} og er ${this.estimeretAlder()} gammel`);
};
p2.toString(); // Jeg hedder Mikkel og er 16 gammel
```

### Tuborgklamme-notation

```javascript
let p3 = {
  navn: "Michell",
  fødselsår: 1966,
  estimeretAlder: function() {
    return new Date().getFullYear() - this.fødselsår;
  },
  toString: function() {
    console.log(
      `Jeg hedder ${this.navn} og er ${this.estimeretAlder()} gammel`
    );
  }
};
p3.toString(); // Jeg hedder Michell og er 53 gammel
```

### Kombiering af notationer

```javascript
let p4 = {};
p4["navn"] = "Lene";
p4.fødselsår = 1964;
p4["estimeretAlder"] = function() {
  return new Date().getFullYear() - this.fødselsår;
};
p4.toString = function() {
  console.log(
    `Jeg hedder ${this.navn} og er ${this["estimeretAlder"]()} gammel`
  );
};
p4.toString(); // Jeg hedder Lene og er 55 gammel
```

### Tilføj og fjern egenskaber

```javascript
let p5 = {
  navn: "Villads",
  fødselsår: 2017,
  estimeretAlder: function() {
    return new Date().getFullYear() - this.fødselsår;
  },
  toString: function() {
    console.log(
      `Jeg hedder ${this.navn} og er ${this.estimeretAlder()} gammel`
    );
  }
};
p5.toString(); // Jeg hedder Villads og er 2 gammel

p5.årTil18 = function() {
  return 18 - this.fødselsår;
};
delete p5.navn;
p5.toString(); // Jeg hedder undefined og er 2 gammel
```

### Gennemløb af nøgler

```javascript
let p6 = {
  navn: "Villads",
  fødselsår: 2017,
  estimeretAlder: function() {
    return new Date().getFullYear() - this.fødselsår;
  },
  toString: function() {
    console.log(
      `Jeg hedder ${this.navn} og er ${this.estimeretAlder()} gammel`
    );
  }
};
p6.toString(); // Jeg hedder Villads og er 2 gammel

for (const key in p6) {
  console.log(key + " = " + typeof p6[key]);
}
/*
navn = string
fødselsår = number
estimeretAlder = function
toString = function
*/

for (const key in p6) {
  console.log(`${key}: ${p6[key]}`);
}

/*
navn: Villads
fødselsår: 2017
estimeretAlder: function () {
    return new Date().getFullYear() - this.fødselsår;
  }
toString: function () {
    console.log(`Jeg hedder ${this.navn} og er ${this.estimeretAlder()} gammel`);
  }
*/

for (const key in p6) {
  if (typeof p6[key] === "function") {
    p6[key]();
  } else {
    console.log(`${key}: ${p6[key]}`);
  }
}
/*
navn: Villads
fødselsår: 2017
Jeg hedder Villads og er 2 gammel
*/
```

### Array af objekter

```javascript
let toString = function() {
  console.log(`Jeg hedder ${this.navn} og er ${this.estimeretAlder()} gammel`);
};
let estimeretAlder = function() {
  return new Date().getFullYear() - this.fødselsår;
};
let personer = [
  {
    navn: "Michell",
    fødselsår: 1966,
    estimeretAlder: estimeretAlder,
    toString: toString
  },
  {
    navn: "Lene",
    fødselsår: 1964,
    estimeretAlder: estimeretAlder,
    toString: toString
  }
];
personer.push({
  navn: "Mikkel",
  fødselsår: 2003,
  estimeretAlder: estimeretAlder,
  toString: toString
});

let m = {};
m.navn = "Mathias";
m.fødselsår = 2006;
m.estimeretAlder = estimeretAlder;
m.toString = toString;
personer.push(m);

console.log(personer.length); // 4
for (var i = 0; i < personer.length; i++) {
  personer[i].toString();
}
/*
Jeg hedder Michell og er 53 gammel
Jeg hedder Lene og er 55 gammel
Jeg hedder Mikkel og er 16 gammel
Jeg hedder Mathias og er 13 gammel
*/

for (const person of personer) {
  person.toString();
}
/*
Jeg hedder Michell og er 53 gammel
Jeg hedder Lene og er 55 gammel
Jeg hedder Mikkel og er 16 gammel
Jeg hedder Mathias og er 13 gammel
*/
```

### JSON

- Brug JSON objektet til at serialisere (stringify) et objekt til en streng, og deserialisere (parse) fra en string til et objekt.

```javascript
let toString = function() {
  console.log(`Jeg hedder ${this.navn} og er ${this.estimeretAlder()} gammel`);
};
let estimeretAlder = function() {
  return new Date().getFullYear() - this.fødselsår;
};
let personer = [
  {
    navn: "Michell",
    fødselsår: 1966,
    estimeretAlder: estimeretAlder,
    toString: toString
  },
  {
    navn: "Lene",
    fødselsår: 1964,
    estimeretAlder: estimeretAlder,
    toString: toString
  }
];
let json = JSON.stringify(personer);
console.log(json);
// [{"navn":"Michell","fødselsår":1966},{"navn":"Lene","fødselsår":1964}]

let personer2 = JSON.parse(json);
console.log(personer2); // objekt
console.log(personer2.length); // 2
```

## Class

- En klasse i JS er egentlig ikke en klasse men i virkeligheden en "constructor function".
  - Javascript er prototype orienteret fsva OOP

```javascript
class Person {}
let p = new Person();
```

er egentlig

```javascript
let Person = (function() {
  function Person() {}
  return Person;
})();
let p = new Person();
```

Typisk vil man benytte en transpiler som TypeScript, men for en god ordens skyld er syntaksen således:

### constructor og metoder

```javascript
class Person {
  constructor(navn, alder) {
    this._navn = navn;
    this._alder = alder;
  }
  print() {
    console.log(`Jeg hedder ${this._navn} og er ${this._alder} gammel`);
  }
}
let p = new Person("Mikkel", 16);
p.print(); // Jeg hedder Mikkel og er 16 gammel
```

### Statiske metoder

```javascript
class Person {
  constructor(navn, alder) {
    this._navn = navn;
    this._alder = alder;
  }
  print() {
    console.log(`Jeg hedder ${this._navn} og er ${this._alder} gammel`);
  }

  static opretTilfældigPerson() {
    let tal = Math.floor(Math.random() * 25 + 1);
    return new Person(String.fromCharCode(tal + 65), tal);
  }
}
let p = Person.opretTilfældigPerson();
p.print();
```

### Egenskaber

```javascript
class Person {
  constructor(navn, alder) {
    this._navn = navn;
    this._alder = alder;
  }
  print() {
    console.log(`Jeg hedder ${this._navn} og er ${this._alder} gammel`);
  }
  get navn() {
    // sikkerhed, log, validering
    return _navn;
  }
  set navn(value) {
    // sikkerhed, log, validering
    this._navn = value;
  }
}
let p = new Person("Mat", 13);
p.print(); // Jeg hedder Mat og er 13 gammel
p.navn = "Mathias";
p.print(); // Jeg hedder Mathias og er 13 gammel
```

### Nedarvning

```javascript
class Person {
  constructor(navn, alder) {
    this._navn = navn;
    this._alder = alder;
  }
  print() {
    console.log(`Jeg hedder ${this._navn} og er ${this._alder} gammel`);
  }
}

class Elev extends Person {
  constructor(navn, alder, elevId) {
    super(navn, alder);
    this._elevId = elevId;
  }
  print() {
    console.log(
      `Jeg hedder ${this._navn} og er ${this._alder} gammel med elevid ${this._elevId}`
    );
  }
}

let e = new Elev("Villads", 2, "xyz"); // Jeg hedder Villads og er 2 gammel med elevid xyz
e.print();
```
