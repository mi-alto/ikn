# Modulo 5 — Principi di automazione con n8n

---

## Slide 111 — Che cosa automatizziamo

- Un’automazione esegue operazioni definite quando si verifica un evento. Può acquisire dati, trasformarli, applicare regole e salvare il risultato.
- Nel modulo 5 costruiamo workflow governati da regole esplicite. Nel modulo 6 vedremo come un agente può scegliere quali azioni intraprendere per raggiungere un obiettivo.

---

## Slide 112 — Quando ha senso automatizzare

- Cerca attività ricorrenti con input riconoscibili, regole stabili e un risultato controllabile.
- Definisci chi usa il risultato e quali eccezioni richiedono una decisione umana. Una regola ambigua va chiarita prima di tradurla in un flusso.

---

## Slide 113 — Trigger e modalità di avvio

- Il trigger stabilisce quando parte il flusso. Può essere un avvio manuale, un orario o un evento in un altro sistema.
- L’avvio manuale permette di osservare una singola esecuzione. Quando il flusso è pronto, si può valutare un avvio periodico o legato a un evento.

---

## Slide 114 — Nodi e passaggio dei dati

- In n8n un nodo rappresenta un passaggio. Riceve dei dati, esegue un’operazione e produce un risultato.
- Per una tabella, ogni riga può diventare un elemento elaborato dal flusso. Il collegamento tra nodi permette a quello successivo di usare i risultati del precedente.

---

## Slide 115 — Mappare e trasformare i campi

- Mappare significa associare un campo in uscita al valore da cui deriva. Puoi scegliere un campo esistente, assegnare un valore fisso o usare un’espressione.
- Prima di applicare una regola numerica controlla i tipi. Una data, un importo e un codice possono richiedere trattamenti diversi.

---

## Slide 116 — Condizioni e percorsi

- Un filtro lascia proseguire gli elementi che soddisfano una regola. Una condizione può indirizzare esiti diversi verso percorsi distinti.
- Decidi come trattare valori assenti o non validi. Se un dato manca, può essere utile mandarlo a verifica prima di applicare una soglia.

---

## Slide 117 — Collegare i dati tabellari

- Una tabella può essere nativa di n8n, arrivare da un file Excel o essere letta da un servizio come Airtable.
- Per leggere un file occorre renderlo disponibile al flusso e interpretarne le colonne. Per leggere o scrivere in un servizio esterno occorre configurare l’accesso.

---

## Slide 118 — Risultati, errori e riesecuzioni

- Definisci dove deve finire il risultato del flusso e come verificare che sia completo.
- Usa la cronologia per risalire al passaggio che ha ricevuto dati inattesi. Prima di rilanciare una scrittura, verifica se la prima esecuzione ha già creato dei record.

---

## Slide 119 — Dimostrazione — Il primo workflow n8n

- Seguiamo [Build your first workflow](https://docs.n8n.io/build-your-first-workflow), il tutorial ufficiale di n8n. Il flusso recupera il meteo, prepara un riepilogo con passaggi configurati e lo salva in una tabella.
- Nel canvas osserviamo trigger, input e output dei nodi e la scrittura finale. Lo stesso schema si applica a dati tabellari di finanza.

---

## Slide 120 — Esercitazione — Carica l’Excel e scarica il report

- Dal [modulo 5](../modulo-5/README.md) scarica `fatture.xlsx` e segui la guida per costruire il flusso in n8n.
- Apri il modulo di test, carica l’Excel e imposta la soglia a 100 €. Il flusso filtra le fatture del 26 novembre 2026, calcola lo scostamento e restituisce `controlli.xlsx`.

---

## Slide 121 — Esercitazione — Verifica la soglia

- Nel primo report devono comparire due fatture. Solo F03, con uno scostamento di 150 €, è da verificare.
- Ripeti con soglia 40 €. Ora sono da verificare sia F02 (+50 €) sia F03 (+150 €). La regola usa lo scostamento in valore assoluto.
