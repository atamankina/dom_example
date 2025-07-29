# Dynamischer Rezept-Generator

Dieses Szenario führt Sie durch die Erstellung eines dynamischen Rezept-Generators mithilfe von JavaScript und DOM-Manipulation. Wir lernen, wie man Inhalte aus einem Array dynamisch anzeigt und Stile basierend auf bestimmten Bedingungen anpasst.

## 1. Projekt-Setup von Grund auf

Wir beginnen damit, die notwendigen Dateien zu erstellen und eine saubere Projektstruktur einzurichten.

### 1.1 `index.html` erstellen

Erstellen Sie eine neue Datei namens `index.html` in Ihrem Projektordner. Der Inhalt dieser Datei ist der Grundstein unserer Webseite und verknüpft unsere CSS- und JavaScript-Dateien.

Öffnen Sie diese Datei und fügen Sie den kompletten Code aus dem separaten Dokument **"ha_index.html"** ein. Beachten Sie, dass diese HTML-Datei eine Verknüpfung zu `style.css` im `<head>` und zu `script.js`am Ende des `<body>` enthält.

### 1.2 `style.css` erstellen

Erstellen Sie eine neue Datei namens `style.css` im *selben Ordner* wie Ihre `index.html`. Diese Datei enthält alle visuellen Stile für unsere Webseite.

Öffnen Sie diese Datei und fügen Sie den kompletten Code aus dem separaten Dokument **"ha_style.css"** ein.

### 1.3 `script.js` erstellen

Erstellen Sie eine leere Datei namens `script.js` ebenfalls im *selben Ordner* wie `index.html` und `style.css`. In diese Datei schreiben wir im Folgenden unseren gesamten JavaScript-Code.

## 2. JavaScript-Logik für den Rezept-Generator entwickeln (Schritt-für-Schritt)

Nun beginnen wir mit der Implementierung der Logik in Ihrer `script.js` Datei. Jeder Schritt baut auf dem vorherigen auf.

### 2.1 Schritt 1: DOM-Elemente abrufen

Bevor wir HTML-Elemente in JavaScript manipulieren können, müssen wir eine Referenz zu ihnen herstellen. Wir verwenden `document.getElementById()`, um spezifische Elemente anhand ihrer eindeutigen IDs zu finden.

Fügen Sie diesen Code an den **Anfang** Ihrer `script.js` Datei:

```jsx
// script.js

// 2.1 DOM-Elemente für den Rezept-Generator abrufen
// Wir speichern Referenzen auf unsere HTML-Elemente in JavaScript-Variablen.
// document.getElementById('ID') gibt das Element mit der angegebenen ID zurück.
const generateRecipeBtn = document.getElementById('generateRecipeBtn'); // Der "Rezept generieren" Button
const recipeList = document.getElementById('recipeList');             // Die <ul>-Liste für die Zutaten
const recipeTitle = document.getElementById('recipeTitle');           // Der <h3>-Titel für den Rezeptnamen
const messageDiv = document.getElementById('message');               // Das <div> für Statusmeldungen

console.log("DOM-Elemente erfolgreich abgerufen.");

```

**Erklärung der DOM-Funktion:**

- **`document.getElementById('ID')`**: Diese Funktion ist grundlegend, um ein einzelnes HTML-Element **direkt und effizient** anhand seines `id`Attributs zu finden. Da IDs auf einer Seite eindeutig sein sollten, gibt diese Methode immer nur ein Element (oder `null`, wenn kein Element mit dieser ID gefunden wird) zurück.

### 2.2 Schritt 2: Die Datenquelle – Ein Array von Rezepten

Für unseren Rezept-Generator benötigen wir eine Sammlung von Rezepten und deren Zutaten. JavaScript-Objekte und -Arrays sind perfekt, um solche strukturierten Daten zu speichern.

Fügen Sie dieses Array direkt unterhalb der DOM-Element-Definitionen in Ihrer `script.js` ein:

```jsx
// script.js (fortgesetzt)

// 2.2 Beispiel-Array von Rezepten
// Jedes Objekt im Array repräsentiert ein Rezept.
// 'name' ist der Name des Rezepts.
// 'ingredients' ist ein Array von Strings, das die Zutatenliste enthält.
const recipes = [
  {
    name: "Sommerlicher Salat",
    ingredients: [
      "200g gemischter Salat",
      "100g Kirschtomaten",
      "1 Gurke",
      "50g Feta-Käse",
      "2 EL Olivenöl",
      "1 EL Balsamico-Essig",
      "Salz, Pfeffer"
    ]
  },
  {
    name: "Pasta Pesto",
    ingredients: [
      "250g Spaghetti",
      "100g Basilikumpesto",
      "50g Parmesan",
      "Knoblauchzehe",
      "Pinienkerne",
      "Olivenöl"
    ]
  },
  {
    name: "Gemüse-Curry",
    ingredients: [
      "1 Zwiebel",
      "2 Karotten",
      "1 Zucchini",
      "200g Kichererbsen",
      "400ml Kokosmilch",
      "2 EL Currypulver",
      "Reis als Beilage"
    ]
  },
  {
    name: "Schoko-Muffins",
    ingredients: [
      "150g Mehl",
      "100g Zucker",
      "2 EL Kakao",
      "1 TL Backpulver",
      "1 Prise Salz",
      "1 Ei",
      "100ml Milch",
      "50g geschmolzene Butter",
      "50g Schokostückchen"
    ]
  },
  {
    name: "Frucht-Smoothie",
    ingredients: [
      "1 Banane",
      "100g Beeren (gefroren)",
      "150ml Mandelmilch",
      "1 EL Chiasamen",
      "Optional: Honig zum Süßen"
    ]
  }
];
console.log("Rezeptdaten geladen. Anzahl der Rezepte:", recipes.length);

```

**Erklärung der JavaScript-Konzepte:**

- **Arrays (`[]`)**: Eine geordnete Sammlung von Werten.
- **Objekte (`{}`)**: Eine ungeordnete Sammlung von Schlüssel-Wert-Paaren.
- **Datenstruktur**: Die Art und Weise, wie wir unsere Daten organisieren. Hier verwenden wir ein Array, das Objekte enthält, was sehr flexibel ist.

### 2.3 Schritt 3: Die Hauptfunktion `generateRandomRecipe()` definieren

Wir erstellen eine Funktion, die die gesamte Logik zum Auswählen und Anzeigen eines Rezepts enthält. Zuerst definieren wir nur den leeren Rahmen dieser Funktion.

Fügen Sie diesen leeren Funktionsblock in Ihre `script.js` ein:

```jsx
// script.js (fortgesetzt)

// 2.3 Hauptfunktion zum Generieren eines zufälligen Rezepts
function generateRandomRecipe() {
  // Hier kommt die gesamte Logik für das Generieren des Rezepts hinein.
  // Wir werden diese Funktion in den nächsten Schritten füllen.
  console.log("generateRandomRecipe Funktion wurde aufgerufen.");
}

```

### 2.4 Schritt 4: Zufälliges Rezept aus dem Array auswählen

Innerhalb unserer `generateRandomRecipe()` Funktion müssen wir nun ein zufälliges Rezept aus unserem `recipes`-Array auswählen.

Erweitern Sie die `generateRandomRecipe()` Funktion in Ihrer `script.js` mit diesem Code:

```jsx
// script.js (fortgesetzt)

function generateRandomRecipe() {
  // 2.4.1 Zufällig einen Index auswählen
  // Math.random() gibt eine Gleitkommazahl zwischen 0 (inklusive) und 1 (exklusive) zurück.
  // Multiplikation mit recipes.length skaliert den Wert auf die Array-Größe.
  // Math.floor() rundet auf die nächste ganze Zahl ab, um einen gültigen Array-Index zu erhalten.
  const randomIndex = Math.floor(Math.random() * recipes.length);

  // 2.4.2 Das Rezept am zufälligen Index auswählen
  const selectedRecipe = recipes[randomIndex];

  console.log("Zufälliges Rezept ausgewählt:", selectedRecipe.name);
}

```

**Erklärung der JavaScript-Konzepte:**

- **`Math.random()`**: Erzeugt eine pseudozufällige Gleitkommazahl zwischen 0 (inklusive) und 1 (exklusive).
- **`Math.floor()`**: Rundet eine Zahl auf die nächste ganze Zahl ab.
- **Array-Indexierung (`recipes[randomIndex]`)**: Greift auf ein Element in einem Array mittels seines numerischen Index zu.

### 2.5 Schritt 5: Bestehende Zutatenliste leeren

Jedes Mal, wenn ein neues Rezept generiert wird, müssen wir die alte Zutatenliste entfernen, bevor die neuen Zutaten hinzugefügt werden. Dies vermeidet, dass sich die Listen überlappen.

Fügen Sie diese Zeile als **erste Zeile** in die `generateRandomRecipe()` Funktion ein:

```jsx
// script.js (fortgesetzt)

function generateRandomRecipe() {
  // 2.5 Bestehende Zutatenliste leeren
  // Das Setzen von innerHTML auf einen leeren String ist eine schnelle Methode,
  // um alle Kindelemente eines HTML-Elements zu entfernen.
  recipeList.innerHTML = '';

  // ... (der Code von 2.4 kommt danach)
  const randomIndex = Math.floor(Math.random() * recipes.length);
  const selectedRecipe = recipes[randomIndex];
  console.log("Zutatenliste geleert und neues Rezept ausgewählt:", selectedRecipe.name);
}

```

**Erklärung der DOM-Funktion:**

- **`element.innerHTML = '';`**: Durch das Zuweisen eines leeren Strings zu `innerHTML` wird der gesamte Inhalt (alle HTML-Tags und Textknoten) innerhalb des Elements `recipeList` entfernt.

### 2.6 Schritt 6: Rezepttitel aktualisieren

Nachdem wir ein Rezept ausgewählt haben, wollen wir den `<h3>`-Titel (`recipeTitle`) aktualisieren, um den Namen des aktuell angezeigten Rezepts widerzuspiegeln.

Fügen Sie diese Zeile in die `generateRandomRecipe()` Funktion ein, **nachdem** `selectedRecipe` definiert wurde:

```jsx
// script.js (fortgesetzt)

function generateRandomRecipe() {
  recipeList.innerHTML = '';
  const randomIndex = Math.floor(Math.random() * recipes.length);
  const selectedRecipe = recipes[randomIndex];

  // 2.6 Rezeptnamen im H3-Tag aktualisieren
  // textContent setzt oder gibt den Textinhalt eines Elements zurück.
  // Im Gegensatz zu innerHTML interpretiert textContent keinen HTML-Code, was es sicherer macht.
  recipeTitle.textContent = `Zutaten für: ${selectedRecipe.name}`;

  console.log(`Titel aktualisiert zu: "Zutaten für: ${selectedRecipe.name}"`);
}

```

**Erklärung der DOM-Funktion:**

- **`element.textContent`**: Diese Eigenschaft wird verwendet, um den Textinhalt eines Elements zu setzen oder zu lesen. Wenn Sie nur Text (kein HTML) in ein Element einfügen möchten, ist `textContent` die **sicherere und oft performantere** Wahl im Vergleich zu `innerHTML`.

### 2.7 Schritt 7: Zutaten dynamisch zur Liste hinzufügen

Dies ist ein zentraler Schritt. Wir müssen für jede Zutat im `selectedRecipe.ingredients`-Array ein neues Listenelement (`<li>`) erstellen und dieses zur `<ul>`-Liste (`recipeList`) hinzufügen.

Erweitern Sie die `generateRandomRecipe()` Funktion mit einer Schleife und den notwendigen DOM-Manipulationen:

```jsx
// script.js (fortgesetzt)

function generateRandomRecipe() {
  recipeList.innerHTML = '';
  const randomIndex = Math.floor(Math.random() * recipes.length);
  const selectedRecipe = recipes[randomIndex];
  recipeTitle.textContent = `Zutaten für: ${selectedRecipe.name}`;

  // 2.7 Zutaten dynamisch zur Liste hinzufügen
  // Die forEach-Methode wird für jedes Element im 'ingredients'-Array einmal ausgeführt.
  selectedRecipe.ingredients.forEach(ingredient => {
    // 2.7.1 Neues Listenelement (<li>) erstellen
    // document.createElement('tagName') erzeugt ein neues HTML-Element im Speicher.
    const listItem = document.createElement('li');

    // 2.7.2 Den Textinhalt des <li> auf die aktuelle Zutat setzen
    listItem.textContent = ingredient;

    // 2.7.3 Das erstellte <li>-Element zur <ul>-Liste hinzufügen
    // parentElement.appendChild(childElement) fügt ein Kindelement als Letztes hinzu.
    recipeList.appendChild(listItem);
    console.log(`Zutat hinzugefügt: ${ingredient}`);
  });
}

```

**Erklärung der DOM-Funktionen:**

- **`document.createElement('tagName')`**: Diese Funktion ist grundlegend für das dynamische Erstellen von HTML-Elementen mit JavaScript. Sie gibt ein neues, noch nicht im Dokument vorhandenes Element-Objekt zurück.
- **`parentNode.appendChild(childNode)`**: Diese Methode fügt einen Knoten (das `childNode`) als das letzte Kind eines anderen Knotens (des `parentNode`) hinzu. Hier fügen wir jedes neu erstellte `<li>` zur `<ul>` (`recipeList`) hinzu.

### 2.8 Schritt 8: Bedingte Style-Manipulation (Zutaten hervorheben)

Wir wollen bestimmte Zutaten (z.B. die, die "Öl", "Butter" oder "Milch" enthalten) visuell hervorheben. Dafür verwenden wir die `classList`-Eigenschaft eines Elements, um eine vordefinierte CSS-Klasse hinzuzufügen.

Erweitern Sie die `forEach`-Schleife in Ihrer `generateRandomRecipe()` Funktion:

```jsx
// script.js (fortgesetzt)

function generateRandomRecipe() {
  // ... (vorheriger Code) ...

  selectedRecipe.ingredients.forEach(ingredient => {
    const listItem = document.createElement('li');
    listItem.textContent = ingredient;

    // 2.8 Bedingte Style-Manipulation: Bestimmte Zutaten hervorheben
    // Wir prüfen, ob die Zutat bestimmte Schlüsselwörter enthält (case-insensitive).
    if (ingredient.toLowerCase().includes("öl") ||
        ingredient.toLowerCase().includes("butter") ||
        ingredient.toLowerCase().includes("milch")) {
      // Wenn die Bedingung erfüllt ist, fügen wir dem <li> die CSS-Klasse 'highlight-ingredient' hinzu.
      // Die eigentlichen Stile sind im CSS-Block der style.css definiert.
      // element.classList.add('className') fügt dem Element eine Klasse hinzu.
      listItem.classList.add('highlight-ingredient');
      console.log(`Zutat hervorgehoben: ${ingredient}`);
    }

    recipeList.appendChild(listItem);
  });
}

```

**Erklärung der DOM-Funktion:**

- **`element.classList.add('className')`**: Diese Methode fügt dem `class`Attribut eines Elements eine oder mehrere CSS-Klassen hinzu. Es ist die bevorzugte Methode, um Stile dynamisch anzuwenden, da sie die Trennung von Struktur (HTML), Stil (CSS) und Verhalten (JavaScript) aufrechterhält.
- **`String.prototype.toLowerCase()`**: Eine JavaScript-String-Methode, die den String in Kleinbuchstaben umwandelt. Nützlich für Vergleiche, die nicht auf Groß-/Kleinschreibung achten sollen.
- **`String.prototype.includes('substring')`**: Eine JavaScript-String-Methode, die prüft, ob ein String einen bestimmten Substring enthält (gibt `true` oder `false` zurück).

### 2.9 Schritt 9: Statusmeldung anzeigen

Es ist immer gut, dem Benutzer Rückmeldung zu geben. Wir aktualisieren das `messageDiv`, um anzuzeigen, welches Rezept generiert wurde, und ändern dynamisch dessen Hintergrundfarbe und Rahmen.

Fügen Sie diesen Codeblock am **Ende** der `generateRandomRecipe()` Funktion ein:

```jsx
// script.js (fortgesetzt)

function generateRandomRecipe() {
  // ... (vorheriger Code) ...

  // 2.9 Nachricht anzeigen, dass ein neues Rezept generiert wurde
  // Wir prüfen, ob das Nachrichtendiv existiert, bevor wir es manipulieren.
  if (messageDiv) {
    messageDiv.innerHTML = `<p>Neues Rezept "<b>${selectedRecipe.name}</b>" generiert!</p>`;
    // Direkte Style-Manipulation über die style-Eigenschaft.
    // Dies ist nützlich für einmalige oder spezifische Stiländerungen.
    messageDiv.style.backgroundColor = '#e1f5fe'; // Hellblau
    messageDiv.style.borderColor = '#42a5f5'; // Blau
    console.log(`Statusmeldung: Rezept "${selectedRecipe.name}" generiert.`);
  }
}

```

**Erklärung der DOM-Funktionen:**

- **`element.style.propertyName = 'value'`**: Ermöglicht die direkte Zuweisung von CSS-Eigenschaften zu einem Element. Der Eigenschaftsname wird in JavaScript als CamelCase geschrieben (z.B. `backgroundColor` statt `background-color`). Während `classList` für das Anwenden vordefinierter Stile bevorzugt wird, ist `element.style` nützlich für dynamische, einmalige Stiländerungen.

### 2.10 Schritt 10: Event Listener verknüpfen

Jetzt müssen wir die `generateRandomRecipe()` Funktion mit unserem Button verbinden, sodass sie ausgeführt wird, wenn der Benutzer auf den Button klickt.

Fügen Sie diese Zeile **nach der Definition der `generateRandomRecipe()` Funktion** in Ihre `script.js` ein:

```jsx
// script.js (fortgesetzt)

// 2.10 Event Listener für den "Rezept generieren"-Button
// addEventListener ist die moderne und empfohlene Methode,
// um Event-Handler zuzuweisen. Sie nimmt das Ereignis ('click')
// und die Funktion (generateRandomRecipe), die bei diesem Ereignis ausgeführt werden soll.
generateRecipeBtn.addEventListener('click', generateRandomRecipe);
console.log("Event Listener für Button hinzugefügt.");

```

**Erklärung der DOM-Funktion:**

- **`element.addEventListener('event', function)`**: Dies ist die Standardmethode, um auf Benutzerinteraktionen zu reagieren. Sie "lauscht" auf ein bestimmtes Ereignis (`'click'`) auf einem Element und führt eine angegebene Funktion aus, wenn dieses Ereignis eintritt.

### 2.11 Schritt 11: Initiales Laden des Rezepts

Damit die Seite nicht leer ist, wenn sie zum ersten Mal geladen wird, rufen wir unsere `generateRandomRecipe()`Funktion einmal direkt beim Laden des Skripts auf.

Fügen Sie diese Zeile am **Ende** Ihrer `script.js` Datei hinzu:

```jsx
// script.js (fortgesetzt)

// 2.11 Initiales Rezept beim Laden der Seite generieren
// Ruft die Funktion einmal auf, damit beim ersten Laden der Seite bereits ein Rezept angezeigt wird.
generateRandomRecipe();
console.log("Initiales Rezept generiert beim Laden der Seite.");

```

### 2.12 Kompletter `script.js`Code (Zusammenfassung)

Nachdem Sie alle oben genannten Schritte durchgeführt haben, sollte Ihre `script.js`-Datei wie folgt aussehen:

```jsx
// script.js

// 2.1 DOM-Elemente für den Rezept-Generator abrufen
const generateRecipeBtn = document.getElementById('generateRecipeBtn');
const recipeList = document.getElementById('recipeList');
const recipeTitle = document.getElementById('recipeTitle');
const messageDiv = document.getElementById('message');

console.log("DOM-Elemente erfolgreich abgerufen.");

// 2.2 Beispiel-Array von Rezepten
const recipes = [
  {
    name: "Sommerlicher Salat",
    ingredients: [
      "200g gemischter Salat",
      "100g Kirschtomaten",
      "1 Gurke",
      "50g Feta-Käse",
      "2 EL Olivenöl",
      "1 EL Balsamico-Essig",
      "Salz, Pfeffer"
    ]
  },
  {
    name: "Pasta Pesto",
    ingredients: [
      "250g Spaghetti",
      "100g Basilikumpesto",
      "50g Parmesan",
      "Knoblauchzehe",
      "Pinienkerne",
      "Olivenöl"
    ]
  },
  {
    name: "Gemüse-Curry",
    ingredients: [
      "1 Zwiebel",
      "2 Karotten",
      "1 Zucchini",
      "200g Kichererbsen",
      "400ml Kokosmilch",
      "2 EL Currypulver",
      "Reis als Beilage"
    ]
  },
  {
    name: "Schoko-Muffins",
    ingredients: [
      "150g Mehl",
      "100g Zucker",
      "2 EL Kakao",
      "1 TL Backpulver",
      "1 Prise Salz",
      "1 Ei",
      "100ml Milch",
      "50g geschmolzene Butter",
      "50g Schokostückchen"
    ]
  },
  {
    name: "Frucht-Smoothie",
    ingredients: [
      "1 Banane",
      "100g Beeren (gefroren)",
      "150ml Mandelmilch",
      "1 EL Chiasamen",
      "Optional: Honig zum Süßen"
    ]
  }
];
console.log("Rezeptdaten geladen. Anzahl der Rezepte:", recipes.length);

// 2.3 Hauptfunktion zum Generieren eines zufälligen Rezepts
function generateRandomRecipe() {
  // 2.5 Bestehende Zutatenliste leeren
  recipeList.innerHTML = '';

  // 2.4.1 Zufällig einen Index auswählen
  const randomIndex = Math.floor(Math.random() * recipes.length);

  // 2.4.2 Das Rezept am zufälligen Index auswählen
  const selectedRecipe = recipes[randomIndex];

  console.log("Zufälliges Rezept ausgewählt:", selectedRecipe.name);

  // 2.6 Rezeptnamen im H3-Tag aktualisieren
  recipeTitle.textContent = `Zutaten für: ${selectedRecipe.name}`;
  console.log(`Titel aktualisiert zu: "Zutaten für: ${selectedRecipe.name}"`);

  // 2.7 Zutaten dynamisch zur Liste hinzufügen
  selectedRecipe.ingredients.forEach(ingredient => {
    const listItem = document.createElement('li');
    listItem.textContent = ingredient;

    // 2.8 Bedingte Style-Manipulation: Bestimmte Zutaten hervorheben
    if (ingredient.toLowerCase().includes("öl") ||
        ingredient.toLowerCase().includes("butter") ||
        ingredient.toLowerCase().includes("milch")) {
      listItem.classList.add('highlight-ingredient');
      console.log(`Zutat hervorgehoben: ${ingredient}`);
    }

    recipeList.appendChild(listItem);
    console.log(`Zutat hinzugefügt: ${ingredient}`);
  });

  // 2.9 Nachricht anzeigen, dass ein neues Rezept generiert wurde
  if (messageDiv) {
    messageDiv.innerHTML = `<p>Neues Rezept "<b>${selectedRecipe.name}</b>" generiert!</p>`;
    messageDiv.style.backgroundColor = '#e1f5fe'; // Hellblau
    messageDiv.style.borderColor = '#42a5f5'; // Blau
    console.log(`Statusmeldung: Rezept "${selectedRecipe.name}" generiert.`);
  }
}

// 2.10 Event Listener für den "Rezept generieren"-Button
generateRecipeBtn.addEventListener('click', generateRandomRecipe);
console.log("Event Listener für Button hinzugefügt.");

// 2.11 Initiales Rezept beim Laden der Seite generieren
generateRandomRecipe();
console.log("Initiales Rezept generiert beim Laden der Seite.");

```

## 3. Projekt ausführen und testen

Nachdem Sie alle Schritte durchgeführt und den Code in Ihren jeweiligen Dateien gespeichert haben, können Sie Ihre Anwendung im Browser testen:

1. **Speichern Sie alle Dateien:** Stellen Sie sicher, dass Sie alle Änderungen in `index.html`, `style.css` und `script.js` gespeichert haben.
2. **Browser öffnen/neu laden:** Öffnen Sie Ihre `index.html` in einem Webbrowser (oder laden Sie die Seite neu, falls sie bereits geöffnet ist).
3. **Erstes Rezept:** Beim Laden der Seite sollte automatisch ein erstes zufälliges Rezept angezeigt werden.
4. **Button klicken:** Klicken Sie auf den Button **"Rezept generieren"**.
    - Sie sollten sehen, wie der Rezeptname unter der Überschrift "Zutaten für:" aktualisiert wird.
    - Die Liste der Zutaten sollte sich ändern und die neuen Zutaten anzeigen.
    - Zutaten, die "Öl", "Butter" oder "Milch" enthalten, sollten farblich hervorgehoben sein (basierend auf den CSS-Regeln).
    - Eine Statusmeldung sollte im "Statusmeldungen"-Bereich am unteren Rand erscheinen.
5. **Entwicklerkonsole prüfen:** Öffnen Sie die Entwicklerkonsole (meistens mit F12), um die `console.log`Ausgaben zu sehen, die Ihnen den Ausführungsfluss anzeigen.

## 4. Git-Repository erstellen und verwalten

Um Ihr Projekt versioniert zu halten und es später einfach teilen zu können, ist es ratsam, es in einem Git-Repository zu speichern.

### 4.1 Voraussetzungen

- **Git installiert:** Stellen Sie sicher, dass Git auf Ihrem System installiert ist. Sie können dies überprüfen, indem Sie `git --version` in Ihrem Terminal ausführen. Falls nicht, laden Sie es von der [offiziellen Git-Website](https://git-scm.com/downloads) herunter und installieren Sie es.
- **GitHub/GitLab/Bitbucket-Konto (optional, aber empfohlen):** Für das Hosting Ihres Remote-Repositories.

### 4.2 Schritt-für-Schritt-Anleitung

### Schritt 1: Projektverzeichnis initialisieren

Öffnen Sie Ihr Terminal (oder Ihre Befehlszeile) und navigieren Sie in das Verzeichnis, in dem sich Ihre `index.html`, `style.css` und `script.js` befinden.

```bash
cd /pfad/zu/ihrem/projektordner

```

Initialisieren Sie ein neues Git-Repository in diesem Ordner:

```bash
git init

```

Sie sollten die Meldung `Initialized empty Git repository in .../.git/` sehen.

### Schritt 2: Dateien zum Staging-Bereich hinzufügen

Fügen Sie alle relevanten Dateien (`index.html`, `style.css`, `script.js`) zum Staging-Bereich hinzu. Dies ist der Bereich, in dem Git verfolgt, welche Änderungen Sie in den nächsten Commit aufnehmen möchten.

```bash
git add index.html style.css script.js
# Oder, um alle neuen/geänderten Dateien im aktuellen Verzeichnis hinzuzufügen:
# git add .

```

### Schritt 3: Erster Commit erstellen

Erstellen Sie Ihren ersten Commit, der die hinzugefügten Dateien als Momentaufnahme speichert. Jeder Commit sollte eine aussagekräftige Nachricht haben, die beschreibt, was in diesem Commit geändert wurde.

```bash
git commit -m "Initiales Setup: Rezept-Generator mit HTML, CSS und JavaScript"

```

### Schritt 4: Remote-Repository erstellen und verbinden (optional)

Wenn Sie Ihr Projekt auf GitHub, GitLab oder Bitbucket hosten möchten:

1. Melden Sie sich bei Ihrem bevorzugten Dienst an.
2. Erstellen Sie ein neues Repository (z.B. `rezept-generator`). **Initialisieren Sie es NICHT mit einer README-Datei oder .gitignore**, da Sie dies bereits lokal getan haben.
3. Nach der Erstellung erhalten Sie Anweisungen, wie Sie Ihr lokales Repository mit dem Remote-Repository verbinden können. Das sieht in der Regel so aus:
    
    ```bash
    git remote add origin https://github.com/IhrBenutzername/rezept-generator.git
    git branch -M main
    git push -u origin main
    
    ```
    
    *(Ersetzen Sie `https://github.com/IhrBenutzername/rezept-generator.git` durch die tatsächliche URL Ihres Remote-Repositories und `main` durch den Standard-Branch-Namen, falls dieser anders ist, z.B. `master`).*
    

### Schritt 5: Änderungen verfolgen und weitere Commits erstellen

Wenn Sie weitere Änderungen an Ihren Dateien vornehmen (z.B. neue Funktionen hinzufügen, Fehler beheben):

1. Nehmen Sie die Änderungen an den Dateien vor.
2. Überprüfen Sie den Status Ihrer Änderungen (zeigt geänderte, aber nicht gestagte Dateien):
    
    ```bash
    git status
    
    ```
    
3. Fügen Sie die geänderten Dateien erneut zum Staging-Bereich hinzu:
    
    ```bash
    git add .
    
    ```
    
4. Erstellen Sie einen neuen Commit mit einer passenden Nachricht:
    
    ```bash
    git commit -m "Funktionalität hinzugefügt: Zutaten dynamisch anzeigen und hervorheben"
    
    ```
    
5. Synchronisieren Sie Ihre lokalen Commits mit dem Remote-Repository (falls vorhanden):
    
    ```bash
    git push
    
    ```
    

Herzlichen Glückwunsch! Ihr Rezept-Generator-Projekt ist nun in einem Git-Repository versioniert.