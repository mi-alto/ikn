# Modulo 4 — Leggere documenti e dati

---

## Slide 94 — Dal documento al dato verificabile

- Un PDF è fatto per essere letto come una pagina. Un foglio Excel organizza dati e calcoli in celle.
- Per lavorare con l’AI, scegliamo come leggere il file, quali informazioni estrarre e in che formato conservarle.
- Il percorso è lo stesso per entrambi. Leggiamo la fonte, trasformiamo i dati e controlliamo il risultato.

---

## Slide 95 — Che cosa succede quando alleghiamo un file

- L’applicazione può estrarre il testo, cercare passaggi pertinenti, inviare pagine a un modello con visione o consegnare il file a uno strumento che esegue codice.
- Il metodo dipende dall’applicazione, dal modello e dagli strumenti abilitati.
- Il caricamento del file e la quantità di contenuto che arriva effettivamente al modello sono due aspetti distinti.

---

## Slide 96 — Tre modi di leggere un PDF

- **Estrazione diretta.** Se il PDF contiene testo selezionabile, uno strumento può recuperarlo senza riconoscere i caratteri da un’immagine.
- **OCR.** Se la pagina è una scansione, il software riconosce le lettere e i numeri nei pixel.
- **Visione.** Un modello multimodale può esaminare la pagina come immagine, compresi grafici, colori e disposizione delle tabelle.

---

## Slide 97 — OCR locale con Tesseract

- Tesseract è un motore OCR che si può eseguire sul proprio computer. Una scansione semplice e leggibile è un buon punto di partenza.
- Tesseract legge immagini. Per una pagina PDF, si esporta prima la pagina come immagine. OCRmyPDF permette di aggiungere un livello di testo a un PDF scansionato.
- Fonte e comandi di riferimento nel [manuale di Tesseract](https://tesseract-ocr.github.io/tessdoc/InputFormats.html).

---

## Slide 98 — Le tabelle richiedono un controllo in più

- Riconoscere correttamente una cifra è solo una parte del lavoro. Bisogna anche collegarla alla riga, alla colonna, all’anno e all’unità giusti.
- Intestazioni su più righe, note e colonne affiancate possono rendere ambiguo il testo estratto.
- Confronta la tabella ricostruita con la pagina originale prima di usare gli importi.

---

## Slide 99 — Lavorare su un PDF lungo

- Usa l’indice per individuare le sezioni pertinenti, poi verifica dove iniziano e finiscono nel visualizzatore.
- Il numero stampato sulla pagina può differire dalla sua posizione nel PDF. Specifica quale numerazione stai usando.
- Per confrontare due bilanci, bastano spesso i prospetti rilevanti e le note che ne spiegano il perimetro.

---

## Slide 100 — Modificare il PDF con Python

- Con una libreria per PDF, Python può selezionare intervalli di pagine, dividere un documento o unire più PDF.
- L’agente può scrivere ed eseguire il programma se dispone di una sandbox con accesso ai file e alla libreria.
- La selezione può mantenere il layout delle pagine. Salva un nuovo file e verifica il conteggio e l’ordine.

---

## Slide 101 — Che cos’è il Markdown

- Markdown è testo semplice con segni che indicano la struttura. Un file `.md` si può leggere direttamente o visualizzare con la formattazione.
- `## Risultati` indica un titolo. Un trattino a inizio riga crea una voce di elenco. Le barre verticali possono delimitare le colonne di una tabella negli editor che le supportano.
- È lo stesso formato usato per i README del corso.

---

## Slide 102 — Dal PDF a una tabella Markdown

- Dopo l’estrazione, possiamo chiedere all’agente di organizzare una tabella in Markdown con intestazioni chiare e riferimenti alle pagine.
- Nei bilanci riportiamo anche anno, unità di misura e nome della voce originale. Segnaliamo quando un importo è ambiguo.
- [Dillinger](https://dillinger.io/) mostra affiancati il testo Markdown e l’anteprima formattata.

---

## Slide 103 — Che cosa c’è dentro un file Excel

- Un file Excel può contenere più fogli, valori, formule e formattazione. Filtri e righe nascoste possono cambiare ciò che si vede a schermo.
- Prima di analizzarlo, identifica il foglio, l’intervallo, le intestazioni e le unità di misura.
- Controlla se nel blocco selezionato sono presenti righe di totale, per evitare di contarle insieme alle righe di dettaglio.

---

## Slide 104 — Leggere e modificare Excel con Python

- L’agente può usare Python per aprire il file, elencare i fogli, leggere celle e intervalli e filtrare le righe.
- Può anche aggiungere una colonna, aggiornare celle o creare un foglio di riepilogo.
- Chiedi di salvare una copia `.xlsx` con un nome distinto. Verifica il foglio e l’intervallo modificati nel file di uscita.

---

## Slide 105 — Calcolare in Python o scrivere formule Excel

- Python può calcolare una variazione e scrivere il risultato come valore. Quel valore resta fisso finché qualcuno lo aggiorna.
- Può anche scrivere una formula Excel nella cella. Un motore di calcolo compatibile la valuta usando le celle a cui fa riferimento.
- La libreria [openpyxl](https://openpyxl.readthedocs.io/en/latest/simple_formulae.html) può scrivere formule. Il ricalcolo spetta a Excel o a un altro motore compatibile.

---

## Slide 106 — Quando conviene esportare in CSV

- Per analizzare una singola tabella, esportare solo il foglio o l’intervallo utile rende i dati più facili da leggere come testo e da elaborare con Python.
- Nel CSV restano i valori esportati. Per esaminare formule, collegamenti tra fogli o formattazione serve il file `.xlsx`.
- Prima di elaborare il CSV, controlla intestazioni, separatore di campo e formato dei decimali.

---

## Slide 107 — Confrontare voci che hanno lo stesso significato

- Registra per ogni dato società, voce originale, anno, unità e pagina di origine.
- Prima del calcolo, verifica che numeratore e denominatore appartengano allo stesso periodo e allo stesso perimetro.
- Nei bilanci, valori consolidati, pro forma e ordinari possono riferirsi a perimetri o definizioni differenti. Rendilo esplicito nel confronto.

---

## Slide 108 — Verificare dati, formule e risultati

- Torna al PDF per controllare che l’importo sia stato letto dalla colonna giusta e che l’unità sia corretta.
- Torna al foglio o al CSV per verificare che righe e intestazioni corrispondano ai dati estratti.
- Rifai un calcolo. La crescita dei ricavi si esprime in percentuale. La differenza tra due margini percentuali si esprime in punti percentuali.

---

## Slide 109 — Esercitazione finale — Dal PDF al Markdown

- Apri gli [estratti Enel e Sorgenia del corso](https://github.com/mi-alto/ikn/tree/main/modulo-2). Chiedi all’agente di estrarre ricavi e risultato operativo 2024–2025 in una tabella Markdown.
- Per ogni valore chiedi denominazione originale, importo, unità e pagina. Segnala eventuali differenze di definizione.
- Incolla la tabella in [Dillinger](https://dillinger.io/) e verifica almeno un dato per società sul PDF.

---

## Slide 110 — Esercitazione finale — Dall’Excel al CSV e al calcolo

- Usa la tabella verificata per creare un foglio Excel. Se la sandbox può generare file, chiedi all’agente di salvarlo come `confronto.xlsx`.
- Chiedi all’agente di riaprire il file con Python, calcolare il margine operativo per anno e salvare una copia del foglio con la nuova colonna. Esporta la tabella in CSV.
- Verifica un calcolo con la formula risultato operativo diviso ricavi. Se la chat non esegue codice, fai gli stessi passaggi nel foglio di calcolo.
