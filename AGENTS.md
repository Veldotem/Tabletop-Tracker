# Expo HAS CHANGED

Read the exact versioned docs at https://docs.expo.dev/versions/v54.0.0/ before writing any code.

---

# Tabletop Tracker (Warhammer 40K)

Eine mobile App zum Tracken von Ressourcen und Runden in Warhammer-40K-Tabletop-Spielen.

## Überblick

- Zweck: Während einer 40K-Partie den eigenen Spielstand tracken (Runde, Command Points, Victory Points).
- Plattform: iOS/Android über React Native + Expo (SDK 54).
- Kontext: persönliches Lernprojekt; der Entwickler lernt React Native/Expo beim Bauen.

## Aktuelle Version: V1 (in Entwicklung)

Einzelspieler-Sicht – es werden nur die eigenen Ressourcen getrackt.

Features:
- Spiel starten und auswählen, ob man Startspieler ist.
- Runden-Tracking über 5 Battle Rounds; pro Runde ziehen beide Spieler abwechselnd.
- „Zug beenden"-Button, der einen Halbzug weiterschaltet und am Rundenende automatisch die nächste Runde beginnt. Nach dem zweiten Zug von Runde 5 ist das Spiel vorbei (10 Halbzüge insgesamt).
- CP-Counter mit +/–.
- VP-Counter mit +/–.
- „Neues Spiel"-Button, der alles zurücksetzt.
- Kein Speichern: beim erneuten Öffnen der App startet immer ein frisches Spiel.

Der aktive Zug ergibt sich aus der Startspieler-Wahl und dem aktuellen Halbzug der Runde. Die Counter bleiben auch während gegnerischer Züge aktiv (in 40K können auch dann CP für Stratageme ausgegeben werden).

## Tech-Stack

- React Native mit Expo, SDK 54 (Start via `npx expo start`, Test in Expo Go).
- TypeScript (`.tsx`/`.ts`), Expo Router als Navigations-/Dateistruktur (`app/`-Verzeichnis).
- State: lokales `useState` mit State-Lifting, bewusst ohne externe State-Library.
- Keine Persistenz in V1.

## Testen in Expo Go

- Die App muss jederzeit in Expo Go (SDK 54) lauffähig bleiben: keine Libraries oder nativen Module verwenden, die einen eigenen Dev-Build erfordern – nur was Expo Go direkt unterstützt.
- Zum Prüfen `npx expo start` ausführen und per QR-Code in Expo Go auf dem Gerät öffnen.
- Jede neue Komponente muss vom App-Einstiegspunkt aus gerendert und erreichbar sein, damit sie in Expo Go sichtbar ist – kein Code, der nirgends eingebunden ist.
- Nach jeder Änderung kurz in Expo Go manuell prüfen, dass das neue Verhalten funktioniert, bevor committet wird.

## Komponenten (Ziel für V1)

- Einstiegs-Screen (`app/index.tsx`) – hält den Spiel-State und schaltet je nach Bildschirm die Ansicht um.
- `StartScreen` – Startbildschirm mit „neues Spiel starten".
- `OrderChoice` – Wahl, ob der Spieler Startspieler ist.
- `GameView` – zeigt Runde und aktiven Zug, die Counter und die Buttons.
- `Counter` – wiederverwendbarer +/–-Baustein für CP und VP.

## Domänen-Glossar

- CP (Command Points): Ressource für Stratageme; in V1 ein manueller Counter.
- VP (Victory Points): Siegpunkte; in V1 ein manueller Counter.
- Battle Round: eine von 5 Spielrunden; beide Spieler ziehen je einmal darin.
- Halbzug: der Zug eines einzelnen Spielers innerhalb einer Battle Round.
- Startspieler: der Spieler, der in jeder Runde zuerst zieht.

## Bewusst NICHT in V1

Absichtlich ausgeklammert; nicht mitbauen, bis explizit dran:
- Ressourcen des Gegners tracken.
- Speichern/Fortsetzen von Spielen (AsyncStorage o. Ä.).
- Automatische CP-Vergabe zu Beginn der eigenen Command-Phase.
- Detailliertes Phasen-Tracking (Command/Movement/Shooting/Charge/Fight).
- Stratagem-System, Secondary Objectives, Fraktionsauswahl.
- Online-/Mehrspieler-Funktionen.

## Arbeitsweise

- Lernen-durch-Bauen: neue Konzepte kurz erklären statt nur fertigen Code liefern.
- In kleinen, testbaren Schritten arbeiten; einfacher, lesbarer Code vor cleveren Abkürzungen.
- Keine zusätzlichen Libraries ohne kurze Begründung.
- Antworten und Kommentare auf Deutsch, Code-Bezeichner auf Englisch.
- Git-Workflow über zwei Rechner (Windows-PC und MacBook); kleine Commits mit klaren Messages.
