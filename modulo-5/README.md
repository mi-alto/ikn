# Modulo 5 — Controllo giornaliero delle fatture con n8n

L’obiettivo è leggere un foglio Excel, selezionare le fatture registrate nel giorno di riferimento, calcolare lo scostamento e produrre un secondo Excel con i controlli.

## Materiale

- [Scarica fatture.xlsx](fatture.xlsx). Il foglio **Fatture** contiene tre righe fittizie. Le date sono stringhe nel formato AAAA-MM-GG e gli importi sono espressi in euro.
- [Tutorial introduttivo ufficiale di n8n](https://docs.n8n.io/build-your-first-workflow) per orientarsi nel canvas e leggere input e output dei nodi.

## Costruisci il flusso

1. Accedi a [n8n Cloud](https://app.n8n.cloud/), crea un workflow e aggiungi **Manual Trigger**.
2. Aggiungi **HTTP Request**, metodo GET. Usa l’[URL diretto dell’Excel](https://raw.githubusercontent.com/mi-alto/ikn/main/modulo-5/fatture.xlsx). Imposta **Response Format → File** e indica `data` come campo di uscita.
3. Collega **Extract From File → Extract From XLSX**. Usa il campo binario `data` e leggi il foglio **Fatture** con la prima riga come intestazione.
4. Aggiungi **Filter**. Mantieni le righe in cui `data_registrazione` è uguale a `2026-11-26`. La data fissa permette di ripetere la prova in qualsiasi giorno.
5. In **Edit Fields**, mantieni i campi in ingresso e aggiungi il campo numerico `scostamento_eur` con l’espressione `{{ Number($json.importo_fatturato_eur) - Number($json.importo_atteso_eur) }}`.
6. In un secondo **Edit Fields**, mantieni i campi in ingresso e aggiungi `esito` con `{{ Math.abs($json.scostamento_eur) > 100 ? 'Da verificare' : 'OK' }}`.
7. Chiudi con **Convert to File → Convert to XLSX**. Imposta il nome `controlli.xlsx` e il foglio **Controlli**. Esegui il flusso e scarica il file dall’output del nodo.

## Risultato atteso

| Fattura | Scostamento | Esito |
|---|---:|---|
| F02 | +50 € | OK |
| F03 | +150 € | Da verificare |

F01 è del giorno precedente e resta fuori. Con la soglia impostata a 150 €, F03 passa a OK, perché la condizione è strettamente maggiore della soglia.

Per usare il flusso ogni giorno, sostituisci l’avvio manuale con **Schedule Trigger**, imposta il fuso orario **Europe/Rome** e usa la data corrente nel filtro. La fonte dovrà essere un Excel aggiornato. In questa prova ogni esecuzione genera un nuovo foglio di output.
