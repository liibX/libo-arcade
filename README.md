# 🐰 LiboArcade

Un endless runner in stile Chrome Dino, ma con un coniglio al posto del dinosauro. Pensato per l’iPhone, funziona in un unico file HTML, senza librerie e senza installazione.

**Autore:** Libo

## Come si gioca

Il coniglio corre da solo: tu devi evitare gli ostacoli. Più vai avanti, più la velocità aumenta.

| Azione | Touch (iPhone) | Tastiera |
|---|---|---|
| Saltare | Tocca la parte destra dello schermo | `Spazio`, `↑` o `W` |
| Abbassarsi | Tieni premuto a sinistra | `↓` |
| Cadere più in fretta (in aria) | Tieni premuto a sinistra durante il salto | `↓` durante il salto |
| Iniziare / ripartire | Tocca ovunque | `Spazio` |

Il pulsante 🔊 in alto a destra attiva o disattiva l’audio.

## Caratteristiche

- Coniglio disegnato in codice, con orecchie animate e sciarpa rossa
- Ciclo giorno/notte con sole, luna e stelle
- Colline in parallasse e nuvole
- Ostacoli: sassi, cespugli e corvi (i corvi compaiono dopo i primi 250 punti)
- Musica chiptune in loop e effetti sonori, generati con la Web Audio API
- Record personale salvato sul dispositivo (`localStorage`)
- Layout adattivo: funziona in verticale e in orizzontale

## Giocare su iPhone

1. Apri la pagina in **Safari**.
2. Tocca **Condividi** e poi **Aggiungi a Home**.
3. Avvia il gioco dall’icona: si apre a schermo intero, come un’app.

> L’audio parte solo dopo il primo tocco (regola di iOS). Se non senti nulla, controlla che l’interruttore silenzioso dell’iPhone non sia attivo.

## File

```
liboarcade.html   # tutto il gioco: HTML, CSS e JavaScript in un unico file
README.md
```

Per usarlo in locale basta aprire `liboarcade.html` in un browser. Per metterlo online va bene qualsiasi hosting statico, per esempio GitHub Pages.

## Personalizzazione

Tutto sta nello script di `liboarcade.html`. Alcuni punti utili:

- **Velocità:** in `update()`, la riga `speed=300+Math.min(score,1500)*.25`
- **Salto:** `r.vy=780` (forza) e `2400` (gravità), sempre in `press()` e `update()`
- **Frequenza ostacoli:** `spawnIn=speed*.75+150+Math.random()*300`
- **Comparsa dei corvi:** la condizione `score>250` in `spawn()`
- **Musica:** l’array `L` contiene la melodia in note MIDI e `B` il basso; `E` è la durata di ogni nota
- **Colori del cielo:** funzione `bg()`

## Dettagli tecnici

- Rendering su `<canvas>` 2D con coordinate logiche a larghezza fissa (640) e scala automatica, anche per gli schermi Retina
- Loop di gioco con `requestAnimationFrame` e passo temporale limitato per evitare salti
- Collisioni con riquadri leggermente ridotti, per un gioco più tollerante
- Audio sospeso automaticamente quando la pagina va in background
