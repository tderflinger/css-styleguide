# Airbnb CSS / Sass Styleguide auf Deutsch

*Ein meist vernünftiger Ansatz für CSS und Sass*

## Inhaltsverzeichnis

1. [Terminologie](#terminologie)
    - [Regeldeklaration](#regeldeklaration)
    - [Selektoren](#selektoren)
    - [Eigenschaften](#eigenschaften)
1. [CSS](#css)
    - [Formatierung](#formatierung)
    - [Kommentare](#kommentare)
    - [OOCSS und BEM](#oocss-und-bem)
    - [ID Selektoren](#id-selektoren)
    - [JavaScript-Haken](#javascript-haken)
    - [Rahmen](#rahmen)
1. [Sass](#sass)
    - [Syntax](#syntax)
    - [Ordnung](#ordnung)
    - [Variablen](#variablen)
    - [Mixins](#mixins)
    - [Extend Anweisung](#extend-anweisung)
    - [Verschachtelte Selektoren](#verschachtelte-selektoren)
1. [Übersetzungen](#übersetzungen)
1. [Lizenz](#lizenz)

## Terminologie

### Regeldeklaration

Eine "Regeldeklaration" ist der Name eines Selektors (oder einer Gruppe von Selektoren) mit einer zugehörigen Gruppe von Eigenschaften. Hier ist ein Beispiel:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### Selektoren

In einer Regeldeklaration sind "Selektoren" die Werte, die bestimmen, welche Elemente im DOM-Baum durch die definierten Eigenschaften gestylt werden. Selektoren können sowohl HTML-Elemente als auch die Klasse, ID oder eines der Attribute eines Elements abgleichen. Hier sind einige Beispiele von Selektoren:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Eigenschaften

Schließlich geben Eigenschaften den ausgewählten Elementen einer Regeldeklaration ihren Stil. Eigenschaften sind Schlüssel-Wert-Paare, und eine Regeldeklaration kann eine oder mehrere Eigenschaftsdeklarationen enthalten. Eigenschaftsdeklarationen sehen so aus:

```css
/* some selector */ {
  background: #f1f1f1;
  color: #333;
}
```

**[⬆ nach oben](#inhaltsverzeichnis)**

## CSS

### Formatierung

* Verwende Soft Tabs (2 Leerzeichen) für die Einrückung.
* Bevorzuge Bindestriche gegenüber camelCasing in Klassennamen.
  - Unterstriche und PascalCasing sind in Ordnung, wenn Sie BEM verwenden (siehe[OOCSS und BEM](#oocss-and-bem) unten).
* Nutze keine ID Selektoren
* Wenn Du mehrere Selektoren in einer Regeldeklaration verwenden, gib jedem Selektor eine eigene Zeile.
* Setze ein Leerzeichen vor die öffnende Klammer `{` in Regeldeklarationen.
* Setze in Eigenschaften ein Leerzeichen nach, aber nicht vor dem Zeichen `:`
* Setze schließende Klammern `}` von Regeldeklarationen auf eine neue Zeile.
* Setze Leerzeilen zwischen Regeldeklarationen.

**Schlecht**

```css
.avatar{
    border-radius:50%;
    border:2px solid white; }
.no, .nope, .not_good {
    // ...
}
#lol-no {
  // ...
}
```

**Gut**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### Kommentare

* Bevorzuge Zeilen-Kommentare (`//` in Sass-Land), vor Blockkommentaren.
* Bevorzuge Kommentare auf einer eigenen Zeile. Vermeide Kommentare am Zeilenende.
* Schreibe detaillierte Kommentare für Code, der nicht selbstdokumentierend ist:
  - Nutzung des z-index
  - Kompatibilität oder browserspezifische Hacks

### OOCSS und BEM

Aus diesen Gründen empfehlen wir eine Kombination von OOCSS und BEM:

  * Es hilft, klare, strenge Beziehungen zwischen CSS und HTML zu schaffen.
  * Es hilft uns, wiederverwendbare, zusammensetzbare Komponenten zu schaffen.
  * Es ermöglicht eine geringere Verschachtelung und eine geringere Spezifizität.
  * Es hilft bei der Erstellung skalierbarer Stylesheets.

**OOCSS**, oder "Object Oriented CSS", ist ein Ansatz zum Schreiben von CSS, der Dich dazu anregt, Deine Stylesheets als eine Sammlung von "Objekten" zu betrachten: wiederverwendbare, wiederholbare Schnipsel, die unabhängig voneinander auf einer Website verwendet werden können.

  * Nicole Sullivan's [OOCSS wiki](https://github.com/stubbornella/oocss/wiki) (Englisch)
  * Smashing Magazine's [Introduction to OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/) (Englisch)

**BEM**, oder "Block-Element-Modifier", ist eine _Namenskonvention_ für Klassen in HTML und CSS. Es wurde ursprünglich von Yandex mit großen Codebasen und Skalierbarkeit im Auge entwickelt und kann als eine solide Reihe von Richtlinien für die Umsetzung von OOCSS dienen.

  * CSS Trick's [BEM 101](https://css-tricks.com/bem-101/)
  * Harry Roberts' [introduction to BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/)

Wir empfehlen eine Variante von BEM mit PascalCased "Blöcken", die in Kombination mit Komponenten (z.B. React) besonders gut funktioniert. Unterstriche und Bindestriche werden weiterhin für Modifikatoren und Kinder verwendet.

**Beispiel**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

  * `.ListingCard` ist der "Block" und stellt die übergeordnete Komponente dar.
  * `.ListingCard__title` ist ein "Element" und repräsentiert einen Nachfahren von `.ListingCard`, der hilft, den Block als Ganzes zu bilden.
  * `.ListingCard--featured` ist ein "Modifikator" und repräsentiert einen anderen Zustand oder eine andere Variante des `.ListingCard` Blocks.

### ID Selektoren

Es ist zwar möglich, Elemente nach ID in CSS auszuwählen, sollte aber generell als Anti-Pattern betrachtet werden. ID-Selektoren führen ein unnötig hohes Maß an [Spezifität](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) in Ihre Regeldeklarationen ein und sind nicht wiederverwendbar.

Weitere Informationen zu diesem Thema findest Du im [Artikel von CSS Wizardry's](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) über den Umgang mit der Spezifität.

### JavaScript-Haken

Vermeide die Bindung an die gleiche Klasse in Ihrem CSS und JavaScript. Das Zusammenführen der beiden führt oft zu einem Minimum an Zeitverschwendung beim Refactoring, wenn ein Entwickler jede Klasse, die er ändert, vergleichen muss. Im schlimmsten Fall haben Entwickler Angst, Änderungen vorzunehmen, aus Sorge, die Funktionalität zu brechen.

Wir empfehlen, JavaScript-spezifische Klassen zu erstellen, die mit dem Präfix `.js-` versehen sind:

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

### Rahmen

Verwenden Sie `0` anstelle von `none`, um anzugeben, dass ein Stil keinen Rahmen hat.

**Schlecht**

```css
.foo {
  border: none;
}
```

**Gut**

```css
.foo {
  border: 0;
}
```
**[⬆ nach oben](#inhaltsverzeichnis)**

## Sass

### Syntax

* Verwende die `.scss` Syntax, niemals die ursprüngliche `.sass` Syntax.
* Ordnen Sie Ihre regulären CSS und `@include` Deklarationen logisch an (siehe unten)

### Ordnung der Eigenschaftsdeklarationen

1. Eigenschaftsdeklarationen

    Listet alle Standard-Eigenschaftsdeklarationen auf, alles, was kein `@include` oder ein geschachtelter Selektor ist.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      // ...
    }
    ```

2. `@include` Deklarationen

    Die Gruppierung von `@include` am Ende erleichtert das Lesen des gesamten Selektors.

    ```scss
    .btn-green {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);
      // ...
    }
    ```

3. Verschachtelte Selektoren

    Verschachtelte Selektoren, _wenn nötig_, gehen zuletzt, und nichts geht ihnen nach. Fügen Sie Leerzeichen zwischen Ihren Regeldeklarationen und verschachtelten Selektoren sowie zwischen benachbarten verschachtelten Selektoren hinzu. Wenden Sie die gleichen Richtlinien wie oben auf Ihre verschachtelten Selektoren an.

    ```scss
    .btn {
      background: green;
      font-weight: bold;
      @include transition(background 0.5s ease);

      .icon {
        margin-right: 10px;
      }
    }
    ```

### Variablen

Bevorzugen Sie Variablennamen mit Bindestrich (z.B. `$my-variable`) gegenüber camelCased oder snake_cased Variablennamen. Es ist zulässig, Variablennamen, die nur innerhalb derselben Datei verwendet werden sollen, einen Unterstrich voranzustellen (z.B. `$_my-variable`).

### Mixins

Mixins sollten verwendet werden, um Ihren Code zu verbessern, Klarheit oder abstrakte Komplexität zu schaffen - ähnlich wie gut benannte Funktionen. Mixins, die keine Argumente akzeptieren, können dafür nützlich sein, aber beachten Sie, dass, wenn Sie Ihre Nutzdaten nicht komprimieren (z.B. gzip), dies zu unnötiger Code-Verdopplung in den resultierenden Stilen beitragen kann.

### Extend Anweisung

`@extend` sollte vermieden werden, da es ein unintuitives und potentiell gefährliches Verhalten hat, besonders wenn es mit verschachtelten Selektoren verwendet wird. Auch das Erweitern von Platzhalter-Selektoren auf oberster Ebene kann zu Problemen führen, wenn sich die Reihenfolge der Selektoren später ändert (z.B. wenn sie sich in anderen Dateien befinden und die Reihenfolge der Dateien verschoben wird). Das Gzipping sollte die meisten Einsparungen verarbeiten, die Sie mit `@extend` erzielt hätten, und Sie können Ihre Stylesheets mit Mixins gut verbessern.

### Verschachtelte Selektoren

**Nicht mehr als drei Ebenen tief schachteln!**

```scss
.page-container {
  .content {
    .profile {
      // STOP!
    }
  }
}
```

Wenn Selektoren so lang werden, schreiben Sie wahrscheinlich CSS, das:

* stark gekoppelt an das HTML (zerbrechlich) ist *-ODER-*
* zu spezifisch (stark) ist *-ODER-*
* nicht wiederverwendbar ist


Nochmals: **Verschachtele niemals ID selectors!**

Wenn Sie zuerst einen ID-Selektor verwenden müssen (und Sie sollten wirklich versuchen, ohne auszukommen), sollten diese niemals verschachtelt werden. Wenn Sie sich dabei erwischen, müssen Sie Ihr Markup erneut überprüfen und herausfinden, warum diese starke Spezifität erforderlich ist. Wenn Sie gut geformtes HTML und CSS schreiben, sollten Sie dies **niemals** tun müssen.

**[⬆ nach oben](#inhaltsverzeichnis)**

## Übersetzungen

  Dieser Styleguide ist auch in anderen Sprachen verfügbar:

  - ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Bahasa Indonesia**: [mazipan/css-style-guide](https://github.com/mazipan/css-style-guide)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [ArvinH/css-style-guide](https://github.com/ArvinH/css-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [Zhangjd/css-style-guide](https://github.com/Zhangjd/css-style-guide)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [mat-u/css-style-guide](https://github.com/mat-u/css-style-guide)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [nao215/css-style-guide](https://github.com/nao215/css-style-guide)
  - ![ko](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [CodeMakeBros/css-style-guide](https://github.com/CodeMakeBros/css-style-guide)
  - ![PT-BR](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Portuguese (Brazil)**: [felipevolpatto/css-style-guide](https://github.com/felipevolpatto/css-style-guide)
  - ![pt-PT](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Portugal.png) **Portuguese (Portugal)**: [SandroMiguel/airbnb-css-style-guide](https://github.com/SandroMiguel/airbnb-css-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [Nekorsis/css-style-guide](https://github.com/Nekorsis/css-style-guide)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [ismamz/guia-de-estilo-css](https://github.com/ismamz/guia-de-estilo-css)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamese**: [trungk18/css-style-guide](https://github.com/trungk18/css-style-guide)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [antoniofull/linee-guida-css](https://github.com/antoniofull/linee-guida-css)

**[⬆ nach oben](#inhaltsverzeichnis)**

## Lizenz

(The MIT License)

Copyright (c) 2015 Airbnb

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ nach oben](#inhaltsverzeichnis)**
