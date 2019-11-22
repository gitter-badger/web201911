# NodeJS

JavaScript runtime bygget på Googles V8 motor, der giver mulighed for at afvikle JavaScript filer på både server og desktop - på de fleste platforme.

NodeJS er skabt af [Ryan Dahl](https://en.wikipedia.org/wiki/Ryan_Dahl) i 2009. Se [ithistorie.cronberg.dk](http://ithistorie.cronberg.dk/?maerker=node,js) for at få et overblik.

https://nodejs.org/

## EventLoop

Node benytter et indbygget eventloop der asynkront kalder eksterne ressourcer (IO, DB, HTTP mv)

<img src='https://miro.medium.com/max/1829/1*fBOm10njasRdooZsSHXkGw.png' height='600' />

[ref](https://miro.medium.com/max/1829)

Node (og JS) er enkelttrådet men afvikler IO/HTTP mv asynkront ved at lade operativsystemet foretage kald.

## Indbyggede APIer

Node har et hav af indbyggede APier som giver mulighed for at benytte

- console
- kryptering
- http, dns, tcp mv
- moduler
- fil systemet
- operativsystemet
- streams
- timers

og meget mere.

## Brug af node

Flere store virksomheder benytter node til at skabe serverside webapplikationer med voldsomt mange brugere

  - Paypal
  - Netflix
  - Uber
  - LinkedIn
  - mv

og mange benytter node scripts som en del af udviklingsprocessen til alle typer af applikationer

  - kompilering/transpilering
  - linting
  - minificering
  - tranformering af billeder
  - kopi/backup
  - deployment
  - kryptering
  - komprimering
  - mv

Argumenterne for at benytte Node er mange

  - Javascript
  - Hastighed
  - Async / non blocking
  - Mange muligheder for at skabe apps (serverside/clientside)
  - NPM med et hav af pakker (+50.000)
  - Meget udbredt

## NPM

Der findes et hav af 3. parts pakker som kan kombineres på alle måde

https://www.npmjs.com/

Pakker som

  - Express (kæmpe framework til at skabe serverside web apps)
  - Async (hjælp til async kode)
  - Request (hjælp til http)
  - Browserify / WebPack (hjælp til modul baseret udvikling og meget mere)
  - Grunt (task runner)
  - Socket.io (socket kommunikation)
  - Commander (console)
  - Mocha (test)
  - UnderscoreJS (arrays mv)
  - Passport (authentication)
  - NodeMailer (mail)
  - React / Angular / Vue (SPA apps)
  - Karma (test)
  - MySql/Mongo (DB)
  - LESS (kompilering CSS)
  - JSHint/TSHint (linter)

NPM er en del af NodeJS installationen.

## En Node-applikation

Består typisk af en mappe med følgende filer

- package.json
  - fil med info om applikationen, source control, hvilke pakker der benyttes samt eventuelle scripts
- .gitignore (eller anden source control ignore file)
  - de filer som ignoreres af source control
- jslint.json eller tslint.json
  - konfiguration af lintere
- jsconfig.json, tsconfig.json eller lign.
  - opsætning til kompiler/transpiler

## Start en node-applikation (uden git)

I en tom mappe (typisk med navngivet efter applikationen

```
npm init 
```

og besvar diverse spørgsmål.

## Start en node-applikation (med git)

I en tom mappe (typisk med navngivet efter applikationen)

```
git init
npm init 
```

og besvar diverse spørgsmål.

Hent tekst fra https://raw.githubusercontent.com/github/gitignore/master/Node.gitignore og gem som .gitignore i mappen

## Eksempel på en simpel node-applikation

Denne applikation benytter axios til at hente json over HTTP og underscore til at hjælpe med lidt array manipulation. 

```
npm install axios --save
npm install underscore --save
```

Bemærk, at package.json nu ser sålede ud:

```json
{
  "name": "nodetest",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "axios": "^0.19.0",    
    "underscore": "^1.9.1"
  }
}

```

Skab filen kommuner.js

```javascript
const _ = require("underscore");
const axios = require("axios").default;

exports.hentKommuner = function() {
  return new Promise(async function(resolve, reject) {
    try {
      let response = await axios.get("https://dawa.aws.dk/kommuner/");
      let kommuner = response.data;
      // skab et array af objekter med navn og kode (skærer resten fra)
      let navne = _.map(kommuner, o => ({
        navn: o.navn,
        kode: o.kode
      }));
      resolve(navne);
    } catch (error) {
      reject(error);
    }
  });
};
```

Skab filen app.js

```javascript
const modul = require("./kommuner.js");

(async function() {
  const kommuner = await modul.hentKommuner();
  kommuner.forEach(v => console.log(`${v.kode}: ${v.navn}`));
})();
```

Prøv applikation fra kommandoprompt

```
node app.js
```

Nu skulle alle kommuner gerne blive vist.

Ret package.json således, at der oprettes et script

```json
{
  "name": "nodetest",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node app.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "axios": "^0.19.0",    
    "underscore": "^1.9.1"
  },
  "devDependencies": {
    "regenerator-runtime": "^0.13.3"
  }
}
```

og kør script fra konsol med 

```
npm start
```

### Skab en browser applikation med brug af jQuery

Den nemmeste måde at skabe HTML er at benytte jQuery. Samtidigt skal vi bruge pakken regenerator-runtime, som er en pakke for at kunne benytte async/awit i flere runtime miljøer og module loadere (se senere). Sidstnævnte gemmes som devDependencies (bruges kun i udvikling).

```
npm install jquery --save
npm install regenerator-runtime --save-dev
```
Opret et html-dokument

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Kommuner i DK</title>
  </head>
  <body>
    <h1>Kommuner i DK</h1>
    <ul id="lst" />
    <script src="index.js"></script>
  </body>
</html>
```

Dan filen index.js:

```javascript
// nødvendig for at kunne håndtere promise i Parcel
const regeneratorRuntime = require("regenerator-runtime");
const $ = require("jquery");
const modul = require("./kommuner.js");

(async function() {
  const kommuner = await modul.hentKommuner();
  const ul = $("#lst");
  kommuner.forEach(v => {
    let li = $("<li/>").html(`${v.kode}: ${v.navn}`);
    ul.append(li);
  });
})();
```

Node forstår require til import at moduler, men det gør browsere ikke (vi kan dog "snart" skifte til ES6 moduler og benytte import/export). Derfor er du nødt til at benytte en module-loader (WebPack, Browserify, Parcel mv). Parcel er den nemmeste - prøv

```
npm install parcel-bundler --save-dev
```

Tilføj nu et par script til package.json

```json
{
  "name": "nodetest",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node app.js",
    "dev": "parcel dev index.html",
    "build": "parcel build index.html"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "axios": "^0.19.0",    
    "underscore": "^1.9.1"
  },
  "devDependencies": {
    "parcel-bundler": "^1.12.4",
    "regenerator-runtime": "^0.13.3"
  }
}
```

Og prøv fra konsol nu at skrive

```
node run dev
```

Nu burde HTML-siden kunne ses gennem http://localhost:1234.

prøv også 

```
node run build
```

og check dist-mappen.