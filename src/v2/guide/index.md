---
title: Introduction
type: guide
order: 2
---

## What is Vue.js?

Vue (uttalas /vjuː/ såsom **view** i engelskan) är ett **progressivt ramverk** för att bygga användargränssnitt. Till skillnad från andra monolitiska ramverk designas Vue från början så att det kan stegvist adopteras. Kärnbiblioteket fokuserar på bara presentationen (the view layer) och är enkelt att komma igång med och integrerar med andra projekt. Å andra sidan har Vue förmåga att driva sofistikerade enkelsidiga applikationer (härefter SPAs) i samband med [moderna verktyg](single-file-components.html) och [stödjande bibliotek](https://github.com/vuejs/awesome-vue#components--libraries).

Om du skulle vilja lära dig mer om Vue innan vi kommer igång då <a id="modal-player"  href="#">titta på denna video</a> som ska gå igenom grunderna med ett provprojekt.

Om du däremot är erfaren utvecklare och vill se Vue jämföras med andra bibliotek/ramverk kolla då [Jämförelsen med andra ramverk](comparison.html).

<div class="vue-mastery"><a href="https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/" target="_blank" rel="noopener" title="Free Vue.js Course">Titta på en gratis videokurs på Vue Mastery</a></div>

## Att komma igång

<a class="button" href="installation.html">Installation</a>

<p class="tip">Den officiella guiden förmodar en mellanliggande kunskapsnivå på HTML, CSS och Javascript. Om du är helt ny till frontend utveckling då bör du nog inte försöka lära dig ett ramverk förrän du har lärt dig webbutvecklingsgrunderna. Tidigare erfarenheter med andra ramverk är inte nödvändiga men blir troligtvis användbara.</p>

Det enklaste sättet att pröva Vue.js är att använda vårt [JSFiddle Hello World example](https://jsfiddle.net/chrisvfritz/50wL7mdz/). Öppna gärna det i en ny flik och följ med medan vi går igenom några exempel. Eller så kan du <a href="https://gist.githubusercontent.com/chrisvfritz/7f8d7d63000b48493c336e48b3db3e52/raw/ed60c4e5d5c6fec48b0921edaed0cb60be30e87c/index.html" target="_blank" download="index.html" rel="noopener noreferrer">skapa en <code>index.html</code> fil</a> och inkluderar Vue med:

``` html
<!-- utvecklingsversion med hjälpsamma konsolvarningar -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

eller:

``` html
<!-- "production" version, optimerad for storlek och hastighet -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

[Installationssidan](installation.html) ger fler alternativ för att installera Vue. **Obs.** Vi **rekommenderar inte** att nybörjare börjar med `vue-cli`, särskilt om inte man är bekant med Node.js-baserat byggverktyg.

Om du föredrar något lite interaktivare kan du också kolla upp [denna tutorial-serie på Scrimba](https://scrimba.com/playlist/pXKqta), som ger dig en bladning av screencast och kodlekplats där du kan pausa och göra experiment när som helst.

## Deklarativt rendering

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cQ3QVcr" target="_blank" rel="noopener noreferrer">Pröva denna lektion på Scrimba</a></div>

Vid Vues kärna ligger ett system som gör det möjligt att rendera deklarativt data till dokumentobjektmodellen (härefter DOM:n) via en rätt så enkel mallsyntax:

``` html
<div id="app">
  {{ message }}
</div>
```
``` js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hallå Vue!'
  }
})
```
{% raw %}
<div id="app" class="demo">
  {{ message }}
</div>
<script>
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hallå Vue!'
  }
})
</script>
{% endraw %}

Därmed har vi skapat vår första Vue-app! Det liknar alldeles att rendera en strängmall men Vue har gjort mycket arbete i bakgrunden. Datan och DOM:n är kopplade och allt är **reaktivt**. Hur vet man? Öppna webbläsarens webbkonsol (direkt, på denna sida) och sätt `app.message` till en annan värde. Således ser du exemplet uppdateras.

Dessutom "text interpolation" kan vi binda element-attributer så här:

``` html
<div id="app-2">
  <span v-bind:title="message">
    Flytta muspekaren här i några sekunder för att se en dynamiskt bunden titel!
  </span>
</div>
```
``` js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'Du öppnade denna sida på ' + new Date().toLocaleString()
  }
})
```
{% raw %}
<div id="app-2" class="demo">
  <span v-bind:title="message">
    Flytta muspekaren här i några sekunder för att se en dynamiskt bunden titel!
  </span>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'Du öppnade denna sida på ' + new Date().toLocaleString()
  }
})
</script>
{% endraw %}

Här har vi stött på något nytt. `v-bind`-attributen som du ser ovan heter ett **direktiv** (directive). Direktiv börjar med `v-` för att tyda på att de är speciella attributer som ges av Vue och som du kanske har gissat tillämpar de särskilt reaktivt beteende till den renderade DOM:n. Det uppger helt enkelt att titel-attributen ska uppdateras när `message`-egenskapen än ändras på Vue-instansen.

Om du öppnar webbkonsolen igen och anger `app2.message = 'nåt nytt meddelande', kommer du lägga märke till att den bundna HTML:n har ändrats - i detta fall så har titel-attributen uppdaterats.

## Villkor och slingar

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cEQe4SJ" target="_blank" rel="noopener noreferrer">Pröva denna lektion på Scrimba</a></div>

Det är lätt att ändra en elements närvaro också:


``` html
<div id="app-3">
  <span v-if="seen">Nu ser du mig</span>
</div>
```

``` js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

{% raw %}
<div id="app-3" class="demo">
  <span v-if="seen">Nu ser du mig</span>
</div>
<script>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
</script>
{% endraw %}

Varsågod ange `app3.seen = false` i webbkonsolen. Du ska se att meddelandet försvinner.

Det här exemplet bevisar att vi kan binda data till inte bara text och attributer utan även själva strukturen av DOM:n. Dessutom ger Vue ett kraftfull transition-system som kan automatiskt applicera [transitionseffekter](transitions.html) när element läggs till/upddateras/tas bort av Vue.

Det är ganska många andra direktiv med var sin särskilda funktionalitet. Till exempel kan v-for`-direktiven användas för att visa en lista över artiklar med datan från ett fält:

``` html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
``` js
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Lär mig JavaScript' },
      { text: 'Lär mig Vue' },
      { text: 'Bygger nåt fantastiskt' }
    ]
  }
})
```
{% raw %}
<div id="app-4" class="demo">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
<script>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Lär mig JavaScript' },
      { text: 'Lär mig Vue' },
      { text: 'Bygger nåt fantastiskt' }
    ]
  }
})
</script>
{% endraw %}

I webbkonsolen ange `app4.todos.push({ text: 'Ny artikel' })`. Du borde se ett nytt element läggs till i listan.

## Att hantera användinmatning

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/czPNaUr" target="_blank" rel="noopener noreferrer">Pröva denna lektion på Scrimba</a></div>

I avsikt att låta användare interagerar med din app kan vi använda `v-on`-direktivet för att attach event listeners (TRANSLATE!) som anropar metoder på våra Vue-instanser:


``` html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Vänd meddelandet</button>
</div>
```
``` js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hallå Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
{% raw %}
<div id="app-5" class="demo">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Vänd meddelandet</button>
</div>
<script>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hallå Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
{% endraw %}

Obs. I den här metoden uppdaterar vi appens tillstånd utan att röra DOM:n - alla DOM-manipulationer hanteras av Vue, vilket ger dig (och koden som du skriver) möjlighet att fokusera på den bakomliggande logiken.

Vue ger också `v-model`-direktivet som gör det lätt som en plätt att få tvåvägsbindning (TRANSLATE?) mellan formulärsinmatningen (TRANSLATE?) och appen.

``` html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
``` js
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hallå Vue!'
  }
})
```
{% raw %}
<div id="app-6" class="demo">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
<script>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hallå Vue!'
  }
})
</script>
{% endraw %}

## Att sammansätta (TRANSLATE?) komponenter

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cEQVkA3" target="_blank" rel="noopener noreferrer">Pröva denna lektion på Scrimba</a></div>

Komponentssystemet är ett till viktigt begrepp i Vue därför att det är an abstraktion som låter oss bygga storskaliga applikationer som sammansätts (TRANSLATE?) av små, fristående och oftast återanvändbara komponenter. Om vi tänker på det så kan vilket applikationsgränssnitt som helst abstraheras till ett komponentsträd (TRANSLATE?).

![Komponentsträdet](/images/components.png)

Med Vue är en komponent i grund och botten en Vue-instans med fördefinerade alternativ. Att registrera en komponent i Vue är lätt:

``` js
// Definiera en ny komponent som heter todo-item
Vue.component('todo-item', {
  template: '<li>Detta är a todo (TRANSLATE!)</li>'
})
```

Nu kan den används i en annan komponents mall:


``` html
<ol>
  <!-- Skapa en instans av todo-item-komponenten -->
  <todo-item></todo-item>
</ol>
```

Men detta skulle rendera samma text för varje todo (TRANSLATE?) vilket inte är särskilt intresserande. Vi skulle kunna skicka data från the parent scope (TRANSLATE!) in i child components (TRANSLATE!). Låt oss modifiera komponentsdefinitionen så att den ska ta en [egenskap](components.html#Props) (TRANSLATE!).

``` js
Vue.component('todo-item', {
  // todo-item-komponenten tar nu en egenskap ("prop"),
  // betrakta den som en custom (TRANSLATE!) HTML-attribut.
  // Denna attribut heter todo.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

Nu kan vi skicka (TRANSLATE?) todo-artikeln till varje upprepade komponent via `v-bind`:

``` html
<div id="app-7">
  <ol>
    <!--
      Varje todo-item motsvarar en artikel i groceryList-
      -objekten. Vi bindar då varje todo-items todo-egenskap 
      till den motsvarande  artikeln med `v-bind:todo="item`. 
      Varje komponent behövs också en nyckel (TRANSLATE?) som
      ska förklaras senare.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>
```
``` js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Grönsaker' },
      { id: 1, text: 'Ost' },
      { id: 2, text: 'Vad som helst annat människor borde äta' }
    ]
  }
})
```
{% raw %}
<div id="app-7" class="demo">
  <ol>
    <todo-item v-for="item in groceryList" v-bind:todo="item" :key="item.id"></todo-item>
  </ol>
</div>
<script>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Grönsaker' },
      { id: 1, text: 'Ost' },
      { id: 2, text: 'Vad som helst annat människor borde äta' }
    ]
  }
})
</script>
{% endraw %}

Detta är ett konstlat exempel men vi har lyckats skilja vår app in i två mindre enheter och barnet (TRANSLATE?) är relativt decoupled (TRANSLATE!) från föräldern via egemskapsgränssnittet (TRANSLATE?). Detta innebär att ytterligare förbättringar till `<todo-item>`-komponenten kan göras utan att påverkar föräldoappen (TRANSLATE?).

I en stor applikation är det nödvändigt att dela hela appen in i komponenter för att göra utvecklingen hanterligt. Vi pratar mer om komponenter [senare i guiden](components.html) men här är ett inbillat exempel på hur en apps mall kan se ut med komponenter:

``` html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### Förhållande till Custom Elements (TRANSLATE!)

Du kanske lagt märke till att Vue-komponenter liknar mycket **Custom Elements**, som tillhör [Web Components Spec](https://www.w3.org/wiki/WebComponents/). Det är på grund av att Vues komponentsyntax (TRANSLATE?) baserats löst på specifikationen. T.ex genomför Vue-komponenter [Slot API:t](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md) och den speciella `is`-attributen. Dock finns det en del viktiga skillnader:

1. The Web Components Spec (TRANSLATE!) har slutföras men är inte natively implemented (TRANSLATE!) i varje webbläsare. Safari 10.1+, Chrome 54+ och Firefox 63+ natively (TRANSLATE!) stödjer webbkomponenter. I jämförelse kräver Vue-komponenter ej några polyfills (TRANSLATE!) och fungerar konsekvent i alla stödda webbläsare (IE9 och över). När det behövs kan Vue-komponenter slås in en native custom element (TRANSLATE!).

2. Vue-komponenter ger viktiga fuktioner som inte är tillgängliga med enkla custom (TRANSLATE!) element. Sådana som tvärskomponent dataflöde, custom (TRANSLATE!) händelsekommunikation och byggverktygsintegrering (TRANSLATE?).

Fastän Vue använder ej custom (TRANSLATE!) element internt har det [great interoperability](https://custom-elements-everywhere.com/#vue) (TRANSLATE!) när det gäller att förbruka eller fördela som custom (TRANSLATE) element. Vue CLI stödjer också att bygga Vue-komponenter som registrerar sig som native custom (TRANSLATE!) elements.

## Redo för mer?

Vi har presenterat kortfattat Vues grundfunktioner - resten av den här guiden ska beskriva dem och andra avancerade funktioner in i minsta detalj, så se till att du läsa igenom den!

<div id="video-modal" class="modal"><div class="video-space" style="padding: 56.25% 0 0 0; position: relative;"><iframe src="https://player.vimeo.com/video/247494684" style="height: 100%; left: 0; position: absolute; top: 0; width: 100%; margin: 0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div><script src="https://player.vimeo.com/api/player.js"></script><p class="modal-text">Video av <a href="https://www.vuemastery.com" target="_blank" rel="noopener" title="Vue.js kurser på Vue Mastery">Vue Mastery</a>. Titta på Vue Mastery's gratis <a href="https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/" target="_blank" rel="noopener" title="Vue.js kurser på Vue Mastery">Intro till Vue kurs</a>.</div>
