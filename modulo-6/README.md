# Modulo 6 — Riconciliare fatture e ordini

Scarica i due Excel con dati fittizi: [fatture.xlsx](fatture.xlsx) e [ordini.xlsx](ordini.xlsx). Tutti gli importi sono imponibili in euro. Le fatture hanno un identificativo proprio. Per associarle agli ordini bisogna confrontare fornitore, causale, sito o impianto e importo.

## Consegna

1. Dai i due file all’agente e chiedi di proporre abbinamenti motivati tra fatture e ordini. Una fattura può coprire l’intero ordine o solo una parte. Più fatture possono riferirsi allo stesso ordine.
2. Chiedi una tabella con ID ordine, ID fatture candidate, totale fatturato, imponibile dell’ordine, differenza, esito e breve motivazione. La differenza è **totale fatturato meno imponibile ordinato**. Calcola il totale quando l’abbinamento è sufficientemente sostenuto.
3. Segnala gli abbinamenti ambigui, le fatture senza ordine identificato e gli ordini senza fattura identificata. Per ogni caso ambiguo, indica quale informazione permetterebbe di decidere.
4. Controlla che nessuna fattura venga conteggiata due volte. Verifica a mano una somma e spiega perché un caso dubbio va lasciato aperto.

Il risultato è una proposta di riconciliazione per il controller. L’esercizio riguarda ordini e fatture, quindi non richiede movimenti bancari.
