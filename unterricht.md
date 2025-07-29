# JavaScript DOM-Interaktion

## Einführung in das Document Object Model (DOM) mit JavaScript

HTML, CSS und JavaScript sind die drei Säulen des Web-Development. Während **HTML** die Struktur einer Webseite festlegt und **CSS** für das Design zuständig ist, sorgt **JavaScript** für Interaktivität und dynamische Inhalte. Um Webseiten wirklich lebendig zu machen, müssen JavaScript-Entwickler in der Lage sein, HTML- und CSS-Komponenten zur Laufzeit zu manipulieren. Hier kommt das **Document Object Model (DOM)** ins Spiel, das diese Aufgabe erheblich vereinfacht.

Das DOM stellt ein HTML-Dokument als eine Baumstruktur von **Knoten** dar. Jeder Teil des Dokuments – sei es ein HTML-Element, ein Attribut oder reiner Text – wird als Knoten im DOM repräsentiert. Jede Änderung, die Sie am DOM vornehmen, spiegelt sich sofort im gerenderten Dokument wider, was es Ihnen ermöglicht, Webseiten dynamisch zu verändern.

## 1. Erste Schritte: Dateien einrichten

Bevor wir ins Detail gehen, richten wir unser Projekt ein.

### 1.1 `index.html` erstellen

Erstellen Sie eine neue HTML-Datei namens `index.html` mit dem folgenden Inhalt. Diese Datei enthält unsere Grundstruktur und die CSS-Stile.

```html
<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="utf-8" />
  <title>HTML-Manipulation mit JavaScript</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 20px;
      background-color: #f4f4f4;
    }
    h1, h2 {
      color: #333;
    }
    .content {
      padding: 15px;
      margin-bottom: 10px;
      border-radius: 5px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      background-color: #ffffff;
      transition: all 0.3s ease;
    }
    .content p {
      margin: 0;
    }
    .content.highlight {
      background-color: #ffe0b2; /* Hellorange für Hervorhebung */
      border: 2px solid #ff9800; /* Orange Rand */
      transform: scale(1.02);
    }
    button {
      padding: 10px 15px;
      margin-right: 10px;
      border: none;
      border-radius: 5px;
      background-color: #4CAF50;
      color: white;
      cursor: pointer;
      font-size: 16px;
      transition: background-color 0.3s ease;
    }
    button:hover {
      background-color: #45a049;
    }
    #message {
        background-color: #e0f7fa;
        padding: 10px;
        border-left: 5px solid #00bcd4;
        margin-top: 20px;
        border-radius: 5px;
    }
    #taskList {
      list-style: none;
      padding: 0;
    }
    #taskList li {
      background-color: #e3f2fd;
      padding: 8px 12px;
      margin-bottom: 5px;
      border-radius: 4px;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }
    #taskList li button {
      background-color: #f44336;
      font-size: 12px;
      padding: 4px 8px;
    }
    #taskInput {
      padding: 10px;
      border: 1px solid #ddd;
      border-radius: 5px;
      width: 250px;
      margin-right: 10px;
    }
  </style>
</head>
<body>

  <h1>DOM-Beispiele und To-Do-Liste</h1>

  <p>
    <button id="btnFirst">Erster Bereich</button>
    <button id="btnSecond">Zweiter Bereich</button>
    <button id="btnThird">Dritter Bereich</button>
    <button id="btnNewMessage">Zufällige Nachricht</button>
  </p>

  <div class="content" id="content_first">
    <p>Dies ist der **erste** Inhaltsbereich. Sein Text wurde beim Laden dynamisch aktualisiert.</p>
  </div>

  <div class="content" id="content_second">
    <p>Dies ist der **zweite** Inhaltsbereich. Sein Text wurde beim Laden dynamisch aktualisiert.</p>
  </div>

  <div class="content" id="content_third">
    <p>Dies ist der **dritte** Inhaltsbereich.</p>
  </div>

  <div id="message">
    <p>Hier erscheinen Nachrichten und dynamische Inhalte.</p>
  </div>

  <hr>
  <h2>Meine To-Do-Liste</h2>
  <input type="text" id="taskInput" placeholder="Neue Aufgabe hinzufügen...">
  <button id="addTaskBtn">Aufgabe hinzufügen</button>
  <ul id="taskList">
    <!-- Aufgaben werden hier dynamisch hinzugefügt -->
  </ul>

  <!-- JavaScript am Ende des Body-Tags einbinden, um sicherzustellen, dass das DOM geladen ist -->
  <script src="script.js"></script>

</body>
</html>

```

### 1.2 `script.js` erstellen

Erstellen Sie eine leere Datei namens `script.js` im selben Verzeichnis wie `index.html`. In diese Datei schreiben wir unseren gesamten JavaScript-Code.

## 2. Interaktion mit dem DOM: Erste Schritte

Der `document`-Objekt ist das Tor zum DOM. Es repräsentiert die gesamte HTML-Seite und ist der Ausgangspunkt für alle DOM-Manipulationen.

### 2.1 Das `body`Element auslesen

Fügen Sie den folgenden Code in Ihre `script.js`-Datei ein:

```jsx
// script.js

console.log("DOM-Script geladen!");

// Schritt 1: Zugriff auf das Body-Element
// document.getElementsByTagName("body") gibt eine HTMLCollection (ähnlich einem Array) zurück.
// [0] wählt das erste (und einzige) Body-Element aus.
let bodyElement = document.getElementsByTagName("body")[0];

// Schritt 2: Den inneren HTML-Inhalt des Body-Elements in der Konsole ausgeben.
// innerHTML enthält den gesamten HTML-Code innerhalb des Elements.
console.log("Inhalt des Body-Elements:", bodyElement.innerHTML);

```

**Ausführung:**

1. Öffnen Sie `index.html` in Ihrem Webbrowser.
2. Öffnen Sie die Entwicklerkonsole (meistens mit **F12** oder **Rechtsklick > Untersuchen**).
3. Sie sollten den gesamten HTML-Inhalt des `<body>`Elements in der Konsole sehen.

### 2.2 Hinweise zum Laden des DOM

Das DOM ist erst verfügbar, wenn der HTML-Code vom Browser geladen und geparst wurde. Deshalb ist es Best Practice, JavaScript-Dateien:

- entweder am **Ende des `<body>`Tags** einzubinden (wie in unserer `index.html` mit `<script src="script.js"></script>`).
- oder Ihren JavaScript-Code innerhalb eines `DOMContentLoaded`Eventlisteners auszuführen, der feuert, sobald das HTML geladen ist.

## 3. HTML-Inhalte manipulieren

Sie können den Inhalt von HTML-Elementen auslesen und ändern.

### 3.1 Die `innerHTML`Eigenschaft

Die Eigenschaft `innerHTML` enthält den gesamten HTML-Auszeichnungscode, der innerhalb eines Elements geschrieben wurde. Sie kann sowohl zum Lesen als auch zum Überschreiben von Inhalten verwendet werden.

**Beispiel:** Den Inhalt des Body-Elements überschreiben (Vorsicht!)

```jsx
// script.js (fortgesetzt)

// Beispiel: Den inneren HTML-Inhalt des Body-Elements ändern.
// ACHTUNG: Dies überschreibt den gesamten bestehenden Inhalt des Body-Elements!
// bodyElement.innerHTML = "<p>Dieser Inhalt wurde von JavaScript ersetzt!</p>";
// console.log("Neuer Body-Inhalt nach innerHTML-Änderung:", bodyElement.innerHTML);

```

**Wichtiger Hinweis:** Das direkte Überschreiben von `innerHTML` ist leistungsstark, kann aber auch gefährlich sein, da es alle vorhandenen Elemente und deren Event Listener innerhalb des Ziels löscht und neu rendert. Für feinere Manipulationen gibt es bessere Methoden.

### 3.2 Elemente nach Tag-Namen auswählen: `getElementsByTagName()`

Diese Methode gibt eine **`HTMLCollection`** (eine live-aktualisierende, array-ähnliche Sammlung) aller Elemente mit dem angegebenen Tag-Namen zurück.

```jsx
// script.js (fortgesetzt)

// Alle Elemente auf der Seite finden
let allElements = document.getElementsByTagName("*");
console.log("Anzahl aller Elemente auf der Seite:", allElements.length);

// Ein spezifisches Element nach seinem Tag-Namen und ID finden und ändern
for (let element of allElements) {
  if (element.id === "content_first") {
    // Ändert den Inhalt des ersten Inhaltsbereichs
    element.innerHTML = "<p>Dieser Inhalt wurde mit `getElementsByTagName` gefunden und aktualisiert!</p>";
    break; // Da IDs eindeutig sein sollten, können wir die Schleife abbrechen
  }
}

```

### 3.3 Elemente nach Klassennamen auswählen: `getElementsByClassName()`

Diese Methode gibt eine **`HTMLCollection`** aller Elemente zurück, die den angegebenen Klassennamen besitzen.

```jsx
// script.js (fortgesetzt)

// Alle Elemente mit der Klasse "content" finden
let contentElements = document.getElementsByClassName("content");
console.log("Anzahl der Elemente mit Klasse 'content':", contentElements.length);

// Den Inhalt des zweiten Inhaltsbereichs ändern
for (let element of contentElements) {
  if (element.id === "content_second") {
    element.innerHTML = "<p>Der Inhalt des zweiten Bereichs wurde mit `getElementsByClassName` aktualisiert!</p>";
    break;
  }
}

```

## 4. Spezifische Elemente auswählen: Optimierte Methoden

Das Iterieren über viele Elemente (wie mit Schleifen) ist ineffizient, wenn Sie ein ganz bestimmtes Element ändern möchten. JavaScript bietet optimierte Methoden.

### 4.1 Auswahl nach ID: `document.getElementById()`

Dies ist die performanteste und am meisten empfohlene Methode, um ein einzelnes Element anhand seiner eindeutigen ID zu finden. Da IDs eindeutig sein müssen, gibt diese Methode direkt das Element (oder `null`, wenn es nicht gefunden wird) zurück.

```jsx
// script.js (fortgesetzt)

// Das Element mit der ID "message" direkt auswählen
let messageDiv = document.getElementById("message");

// Den Inhalt des Nachrichtendivs ändern
if (messageDiv) { // Immer prüfen, ob das Element existiert, bevor darauf zugegriffen wird
  messageDiv.innerHTML = "<p>Nachrichtendiv-Inhalt wurde mit `getElementById` aktualisiert.</p>";
}

```

**Methoden verketten:** Da `getElementById()` ein einzelnes Element zurückgibt, können Sie Methoden und Eigenschaften direkt verketten:

```jsx
// document.getElementById("message").innerHTML = "<p>Nochmal aktualisiert direkt!</p>";

```

### 4.2 Auswahl mit CSS-Selektoren: `querySelector()` und `querySelectorAll()`

Diese Methoden ermöglichen es Ihnen, Elemente mit CSS-Selektor-Syntax zu finden, was sehr flexibel ist.

- **`document.querySelector(selector)`**: Gibt das **erste** Element zurück, das dem angegebenen CSS-Selektor entspricht.
- **`document.querySelectorAll(selector)`**: Gibt eine **`NodeList`** (eine statische Sammlung, die nicht live-aktualisiert wird) aller Elemente zurück, die dem angegebenen CSS-Selektor entsprechen.

```jsx
// script.js (fortgesetzt)

// Das erste Element mit der ID "content_first" und einem Kind-p-Element finden
// Selektoren für IDs beginnen mit '#'
let firstContentParagraph = document.querySelector("#content_first p");
if (firstContentParagraph) {
  firstContentParagraph.textContent = "Der erste Absatz des ersten Bereichs, mit `querySelector` geändert!";
}

// Alle Elemente mit der Klasse "content" finden
// Selektoren für Klassen beginnen mit '.'
let allContentDivs = document.querySelectorAll(".content");
console.log("Alle Content-Divs (via querySelectorAll):", allContentDivs.length);

// Ein spezifisches Kind-Element mit einer Pseudoklasse finden (z.B. den zweiten Absatz)
// Beispiel: Angenommen, 'content_third' hätte mehrere Paragraphen
// document.querySelector("#content_third p:nth-child(2)").textContent = "Dies ist der zweite Paragraph im dritten Bereich.";

```

**Wichtiger Unterschied zu `getElementsBy...`:**

- `getElementsByTagName` und `getElementsByClassName` geben **`HTMLCollection`** zurück, die "live" sind (Änderungen im DOM spiegeln sich automatisch wider).
- `querySelector` und `querySelectorAll` geben **`Element`** bzw. **`NodeList`** zurück, die "statisch" sind (eine Momentaufnahme zum Zeitpunkt des Aufrufs).

## 5. Mit Attributen arbeiten

Die Manipulation von HTML-Attributen ist eine Kernfunktion des DOM.

### 5.1 Attribute setzen und entfernen: `setAttribute()` und `removeAttribute()`

- **`element.setAttribute(name, value)`**: Fügt ein neues Attribut hinzu oder ändert den Wert eines bestehenden Attributs.
- **`element.removeAttribute(name)`**: Entfernt ein Attribut vom Element.

**Beispiel:** Sichtbarkeit von Elementen steuern.

```jsx
// script.js (fortgesetzt)

// Funktion zum Zufälligen Anzeigen eines Inhaltsbereichs beim Laden
function showRandomContentSection() {
  const contentSections = document.querySelectorAll(".content");

  // Zuerst alle Bereiche ausblenden (CSS display: none ist in index.html definiert)
  contentSections.forEach(section => {
    section.style.display = "none";
  });

  // Zufällig einen Index auswählen (0, 1 oder 2)
  const randomIndex = Math.floor(Math.random() * contentSections.length);

  // Den zufällig ausgewählten Bereich anzeigen
  if (contentSections[randomIndex]) {
    contentSections[randomIndex].style.display = "block";
    console.log(`Zufällig angezeigt: ${contentSections[randomIndex].id}`);
  }
}

// Funktion beim Laden der Seite aufrufen
showRandomContentSection();

// Beispiel für setAttribute und removeAttribute (hier nicht im Hauptfluss verwendet, da CSS besser ist)
// Let's modify the message div's custom attribute and then remove it
if (messageDiv) {
    messageDiv.setAttribute("data-status", "active");
    console.log("Data-Status von messageDiv:", messageDiv.getAttribute("data-status"));
    // setTimeout(() => {
    //     messageDiv.removeAttribute("data-status");
    //     console.log("Data-Status von messageDiv nach Entfernung:", messageDiv.getAttribute("data-status"));
    // }, 2000);
}

```

**Hinweis zur Sichtbarkeit:** Statt das `hidden`-Attribut direkt zu manipulieren, ist es oft sauberer und flexibler, die Sichtbarkeit über CSS-Eigenschaften (`display`, `visibility`, `opacity`) oder durch das Hinzufügen/Entfernen von CSS-Klassen zu steuern. Dies hält die Styling-Logik von der JavaScript-Logik getrennt.

## 6. Mit Klassen arbeiten: `classList`

Die `classList`-Eigenschaft ist der bevorzugte Weg, um CSS-Klassen eines Elements zu verwalten. Sie ermöglicht es Ihnen, mehrere Stile gleichzeitig anzuwenden oder zu entfernen, ohne die `style`-Eigenschaft direkt zu manipulieren.

### 6.1 Die `classList`Methoden

- **`element.classList.add(className)`**: Fügt eine Klasse hinzu.
- **`element.classList.remove(className)`**: Entfernt eine Klasse.
- **`element.classList.toggle(className)`**: Fügt die Klasse hinzu, wenn sie nicht vorhanden ist, und entfernt sie, wenn sie vorhanden ist.
- **`element.classList.contains(className)`**: Prüft, ob die Klasse vorhanden ist (gibt `true`/`false` zurück).

**Beispiel:** Elemente hervorheben.

```jsx
// script.js (fortgesetzt)

// Funktion zum Hervorheben eines Inhaltsbereichs
function highlightContent(idToHighlight) {
  // 1. Alle vorhandenen Hervorhebungen entfernen
  document.querySelectorAll(".content").forEach(element => {
    element.classList.remove('highlight');
  });

  // 2. Die "highlight"-Klasse zum ausgewählten Element hinzufügen
  const selectedElement = document.getElementById(idToHighlight);
  if (selectedElement) {
    selectedElement.classList.add('highlight');
  }
}

// Beim Laden der Seite einen zufälligen Bereich hervorheben
const highlightIndex = Math.floor(Math.random() * 3);
const highlightIds = ["content_first", "content_second", "content_third"];
highlightContent(highlightIds[highlightIndex]);

```

## Zusammenfassung

In dieser Lektion haben Sie tiefgreifende Einblicke in die Interaktion von JavaScript mit dem HTML-Dokument über das **Document Object Model (DOM)** erhalten. Sie haben gelernt, wie Sie HTML-Inhalte und deren CSS-Eigenschaften dynamisch ändern können. Diese Änderungen können durch Benutzerereignisse ausgelöst werden, was essenziell für die Erstellung moderner, dynamischer Webanwendungen ist.

Die wichtigsten Konzepte und Verfahren, die wir behandelt haben:

- **Untersuchung der Dokumentstruktur** mit Methoden wie `document.getElementById()`, `document.getElementsByClassName()`, `document.getElementsByTagName()`, `document.querySelector()`und `document.querySelectorAll()`.
- **Änderung des Inhalts des Dokuments** mit der Eigenschaft `innerHTML` und, als sicherere Alternative für reinen Text, mit `textContent`.
- Das **dynamische Erstellen und Hinzufügen neuer Elemente** zum DOM mit `document.createElement()`, `appendChild()`, `createTextNode()` und das Entfernen von Elementen mit `removeChild()`.
- **Hinzufügen und Ändern von Attributen** von Seitenelementen mit den Methoden `setAttribute()` und `removeAttribute()`.
- Die **korrekte Manipulation von Elementklassen** mit der Eigenschaft `classList` (mit `add()`, `remove()`, `toggle()`) und ihre Verbindung zu CSS-Stilen.
- **Binden von Funktionen an Ereignisse** (wie Klicks, Mausbewegungen oder Tastatureingaben) in bestimmten Elementen mit `addEventListener()`.