# mho-pull-tracker · Pull-Rechner für Monster Hunter Outlands

Website zum Berechnen der Spezial-Pulls, mit Sammlung (Zeitleiste aller SSR), Logbuch und Online-Speichern per Spielername + PIN.

## Dateien

| Datei | Wofür |
|---|---|
| `index.html` | Die komplette Website |
| `firestore.rules` | Sicherheitsregeln für die Datenbank (einmal in Firebase einfügen) |
| `README.md` | Diese Anleitung |

---

## Einrichtung (einmalig, ca. 20 Minuten)

### 1. Google Sheet freigeben (Charakter-Liste)

1. Das Google Sheet öffnen → oben rechts **Freigeben**.
2. Unter **Allgemeiner Zugriff** auf **„Jeder mit dem Link“** stellen, Rolle **Betrachter** → **Fertig**.

Die Website liest den Tab **„Banner“**. Neue Charaktere einfach als neue Zeile eintragen:
`Charakter | Typ (Spezial/Standard) | Info | Start | Ende | Ende bestätigt | Version`

### 2. GitHub (die Website veröffentlichen)

1. Auf **github.com** anmelden → oben rechts **+** → **New repository**.
2. Name: `mho-pull-tracker`, **Public** auswählen → **Create repository**.
3. Auf der leeren Repo-Seite **„uploading an existing file“** anklicken → `index.html`, `firestore.rules` und `README.md` hineinziehen → **Commit changes**.
4. Im Repo **Settings** → links **Pages** → bei **Source** „Deploy from a branch“, Branch **main**, Ordner **/ (root)** → **Save**.
5. Nach 1–2 Minuten steht oben die Adresse, z. B. `https://foxinvictus.github.io/mho-pull-tracker/`. Die Seite funktioniert jetzt schon, nur noch ohne Konto.

### 3. Firebase (Online-Speichern)

1. **console.firebase.google.com** öffnen, mit deinem Google-Konto anmelden → **Projekt erstellen**. Name: `mho-pull-tracker`. Google Analytics brauchst du nicht (ausschalten) → **Projekt erstellen**.
2. **Anmeldung einschalten:** links **Authentication** → **Jetzt starten** → Tab **Anmeldemethode** → **E-Mail/Passwort** → den ersten Schalter **aktivieren** → **Speichern**.
   *(Es werden nie E-Mails verschickt. Die Website wandelt den Spielernamen intern in eine Login-Adresse um, die PIN ist das Passwort.)*
3. **Erlaubte Adresse eintragen:** in Authentication → Tab **Einstellungen** → **Autorisierte Domains** → **Domain hinzufügen** → `foxinvictus.github.io` → Hinzufügen.
4. **Datenbank anlegen:** links **Firestore Database** → **Datenbank erstellen** → Standort in Europa wählen (z. B. `europe-west3` Frankfurt) → **Im Produktionsmodus starten** → Erstellen.
5. **Regeln eintragen:** in Firestore → Tab **Regeln** → alles löschen → kompletten Inhalt von `firestore.rules` einfügen → **Veröffentlichen**.
6. **Web-App registrieren:** oben links Zahnrad → **Projekteinstellungen** → ganz unten bei **Meine Apps** das Web-Symbol **`</>`** → App-Name: `mho-pull-tracker` (Firebase Hosting **nicht** ankreuzen) → **App registrieren**.
   Es erscheint ein Block `const firebaseConfig = { apiKey: "...", authDomain: "...", ... };` → diesen Teil von `{` bis `}` kopieren.

### 4. Firebase-Werte in die Website eintragen

1. Im GitHub-Repo auf `index.html` klicken → oben rechts das **Stift-Symbol** (Edit).
2. Mit Strg+F nach `FIREBASE_CONFIG = null` suchen.
3. `null` durch den kopierten Block ersetzen, sodass es so aussieht:
   ```js
   const FIREBASE_CONFIG = {
     apiKey: "AIza...",
     authDomain: "mho-pull-tracker-xxxx.firebaseapp.com",
     projectId: "mho-pull-tracker-xxxx",
     storageBucket: "...",
     messagingSenderId: "...",
     appId: "1:...:web:..."
   };
   ```
4. **Commit changes**. Nach 1–2 Minuten ist die Website mit Konto-Funktion online.

Der `apiKey` darf öffentlich in der Seite stehen, das ist bei Firebase so gedacht. Geschützt werden die Daten durch die Regeln aus Schritt 3.5: Jeder Spieler kann nur seinen eigenen Stand lesen und ändern.

---

## Später aktualisieren

- **Neuer Charakter / Banner:** nur eine Zeile im Google Sheet (Tab „Banner“) eintragen. Alle sehen es beim nächsten Öffnen.
- **Neue Version der Website:** `index.html` im Repo durch die neue Datei ersetzen (*Add file → Upload files*) → Commit. Danach den `FIREBASE_CONFIG`-Block wieder eintragen, falls die neue Datei `null` enthält.

## Gut zu wissen

- **PIN:** 6–8 Ziffern. Firebase blockiert nach zu vielen falschen Versuchen automatisch für eine Weile. Eine vergessene PIN lässt sich nicht zurücksetzen.
  Als Admin kannst du helfen: In Firestore → `players` das Dokument mit dem passenden `name` suchen, die Dokument-ID merken, das Dokument löschen und unter Authentication → Nutzer den Eintrag mit derselben Nutzer-UID löschen. Danach kann sich der Spieler neu registrieren.
- Man bleibt auf dem Gerät angemeldet. Auf fremden Geräten nach dem Spielen **Abmelden**.
- Ohne Internet funktioniert die Seite weiter. Änderungen werden hochgeladen, sobald wieder eine Verbindung da ist.
- Der kostenlose Firebase-Plan („Spark“) reicht für viele Spieler und wird nicht wegen Inaktivität pausiert.
