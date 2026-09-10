# Poster v1 — Entscheidungen & Annahmen

Autonom erstellt am 2026-09-10. Aufgabe: PDF + NotebookLM-Dialog + README lesen, **erste Poster-Version** bauen. Wichtig laut Nutzer: **Grafiken mit echten Kurven**.

## Was ich gelesen habe
- `How The Fast Fourier Transform Actually Works.pdf` (52 S., Medium-Artikel, Kamrun Nahar) — Volltext extrahiert.
- `NotebookLM Dialog.md` — Nutzer-Fragen drehen sich um: das 2/5/9-Hz-Beispiel, den „Multiply-and-Sum"-Test („does it rhyme?"), die drei Regler (Amplitude/Frequenz/Phase), das Zeichnen der Gesamtkurve, und warum Phase den Sinus-only-Test kippt (→ sin+cos-Immunität).
- `README.md` — Poster soll den Fourier erklären und **schrittweise wachsen, wie ein Jupyter-Notebook**.

## Kernentscheidungen

1. **Format: eine eigenständige HTML-Datei (`poster/index.html`), self-contained.**
   Grund: „echte Kurven" heißt für mich *aus der Mathematik berechnete* Kurven, nicht schematische Zeichnungen. HTML+SVG erlaubt, das Signal zur Laufzeit zu sampeln und als echte SVG-Pfade zu rendern. Zusätzlich Artifact-tauglich (kein externer Code außer Google Fonts).

2. **„Wächst wie ein Notebook": vertikale Zellen-Struktur.**
   Jede Erklärstufe = eine „Zelle". Am Ende stehen ausgegraute „coming next"-Platzhalterzellen (Aliasing, Windowing, FFT-Speed, Spektrogramm, Anwendungen), damit das schrittweise Wachsen sichtbar ist. v1 füllt die Zellen, die der Dialog abdeckt.

3. **Inhalt von v1** (bewusst auf das fokussiert, was der Nutzer im Dialog vertieft hat):
   - Die drei Regler an *einer* echten Sinuskurve.
   - Die drei Komponenten `1.0·sin(2π·2t)`, `0.6·sin(2π·5t+1)`, `0.35·sin(2π·9t+2)` als echte Kurven.
   - Die Summe („The Recording" / „scary wave") — echte Überlagerung, N=1000, 1 s.
   - Der Test „Does it rhyme?": Signal × Testwelle, schraffierte Produktfläche, Laufsumme, Score. **Interaktiv** (Frequenz-Slider 1–12 Hz) — bei 2/5/9 Hz großer Score, dazwischen ~0.
   - Das Spektrum: **echte DFT** in JS über die 1000 Samples, Balken bei 2/5/9 Hz mit Höhen 1.0/0.6/0.35.

4. **Phase-Korrektheit im Test.** Der Score-Balken nutzt die *phasen-immune* Magnitude `2/N·√(Σx·cos)²+(Σx·sin)²)` — genau der sin+cos-Trick aus dem Dialog. Die schraffierte Fläche zeigt weiterhin das Sinus-Produkt (anschaulich „Fläche über der Linie"). So ist die Grafik anschaulich UND rechnerisch ehrlich.

5. **Design.** Engineering-/Laborheft-Identität statt Serifen-Creme-Klischee:
   - Typo: IBM Plex Sans (Display) / IBM Plex Serif (Fließtext) / IBM Plex Mono (Mathe, Code, Daten).
   - Kühles Papier-Neutral (leichter Blaustich), Tinte blau-schwarz. Akzent = Signal-Blau.
   - Kurvenfarben (kategorial, validiert mit dataviz-Checker): 2 Hz `#1667b8`, 5 Hz `#c8641c`, 9 Hz `#8a3ca0`, Summe = Tinte. Jede Kurve zusätzlich direkt beschriftet (Sekundärkodierung, nicht nur Farbe).
   - Light- und Dark-Theme über Tokens.

6. **Sprache: Deutsch.** Dialog und Nutzer-Anweisungen sind deutsch.

## Annahmen (mangels Rückfrage-Möglichkeit)
- „Poster-Version" = digitales, druckbares HTML-Poster, kein PDF/Print-Layout in v1. Begründung: README („wächst wie Notebook") + Testbarkeit.
- Beispielsignal exakt aus Artikel/Dialog übernommen (Amplituden 1.0/0.6/0.35, Frequenzen 2/5/9, Phasen 0/1.0/2.0 rad).
- Fokus v1 = die im Dialog vertieften Themen; restliche Artikel-Themen als sichtbare, noch leere Folgezellen.
- Kein Git-Repo → keine Commits.

## Offene Punkte für Review mit Nutzer
- Soll das Poster eher **ein großes Druck-Poster (A1/A0, PDF)** werden oder das wachsende HTML-Notebook bleiben?
- Weitere Zellen priorisieren (Aliasing? Windowing? FFT-Speed? Spektrogramm?).
- Sprache DE vs. EN (Artikel ist EN).
- Ton: mehr erzählerisch (wie Artikel, Münzglas-Metapher) oder knapper/technischer?
