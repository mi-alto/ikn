# Modulo 6 — Riconciliare fatture e ordini

I dati sono fittizi e tutti gli importi sono imponibili in euro.

- [fatture.csv](fatture.csv)
- [ordini.csv](ordini.csv)

Per usare Airtable, importa ciascun CSV come tabella separata nella stessa base. Usa la prima riga come intestazione e controlla che `Imponibile EUR` sia numerico. Per la prova in n8n puoi partire direttamente dai due blocchi di testo qui sotto.

## Imposta l’agente in n8n

Nel **System Message** inserisci le istruzioni stabili:

> Sei l’assistente del controller. Proponi abbinamenti usando solo i dati ricevuti. Valuta fornitore, causale, sito o impianto e importi. Considera più fatture per un ordine. Se le evidenze non bastano, mantieni il caso aperto e indica il dato da chiedere. Evita di conteggiare la stessa fattura più di una volta.

Nel **Prompt** dell’agente incolla la richiesta e i due CSV qui sotto. I dati entrano come testo nel contesto del modello.

```text
Proponi la riconciliazione delle fatture con gli ordini.
Restituisci ID ordine, ID fatture, totale fatturato, totale ordinato,
differenza (fatturato meno ordinato), esito e motivazione.
Indica anche ordini e fatture rimasti senza abbinamento.

<FATTURE>
ID fattura,Data fattura,Fornitore,Causale fattura,Imponibile EUR
F-311,2026-11-18,Reti e Misure,"Collaudo e taratura misuratori, rif. novembre",900
F-312,2026-11-12,TERMO SERVIZI,Prima quota intervento su gruppo ricircolo P17,1000
F-313,2026-11-15,Cavi Lombardi,"Materiale MT dep. N, lotto A + trasporto urgente",1570
F-314,2026-11-19,Elettro Nord,Test relè quadro LC,1200
F-315,2026-11-21,Sensori Italia,Acconto sonde pressione imp. Sud,600
F-316,2026-11-24,Termoservizi,Saldo ripristino gruppo ricircolo P17,1400
F-317,2026-11-20,ELETTRO NORD SRL,Tagliando cabina bassa tensione MB,1200
F-318,2026-11-25,Idro Pronto S.r.l.,Uscita urgente per allagamento locale tecnico,420
</FATTURE>

<ORDINI>
ID ordine,Data ordine,Fornitore,Descrizione ordine,Imponibile EUR
O-101,2026-11-02,ElettroNord S.r.l.,Manutenzione programmata cabina BT del sito Monza,1200
O-102,2026-11-03,Termoservizi S.p.A.,Revisione pompa di circolazione P-17,2400
O-103,2026-11-03,Reti & Misure S.r.l.,Taratura contatori presso sito Est,900
O-104,2026-11-04,Reti & Misure S.r.l.,Taratura contatori presso sito Ovest,900
O-105,2026-11-05,Cavi Lombardi S.r.l.,"Fornitura cavo MT lotto A, deposito Nord",1450
O-106,2026-11-06,Acqua Service S.r.l.,Ispezione perdite tratta Vallone,760
O-107,2026-11-07,ElettroNord S.r.l.,Verifica protezioni quadro sito Lecco,1200
O-108,2026-11-07,Sensori Italia S.r.l.,Fornitura sensori pressione per impianto Sud,1800
</ORDINI>
```

## Consegna

1. Esegui il prompt con i due CSV nel contesto e chiedi di proporre abbinamenti motivati tra fatture e ordini. Una fattura può coprire l’intero ordine o solo una parte. Più fatture possono riferirsi allo stesso ordine.
2. Chiedi una tabella con ID ordine, ID fatture candidate, totale fatturato, imponibile dell’ordine, differenza, esito e breve motivazione. La differenza è **totale fatturato meno imponibile ordinato**. Calcola il totale quando l’abbinamento è sufficientemente sostenuto.
3. Segnala gli abbinamenti ambigui, le fatture senza ordine identificato e gli ordini senza fattura identificata. Per ogni caso ambiguo, indica quale informazione permetterebbe di decidere.
4. Controlla che nessuna fattura venga conteggiata due volte. Verifica a mano una somma e spiega perché un caso dubbio va lasciato aperto.

Il risultato è una proposta di riconciliazione per il controller. L’esercizio riguarda ordini e fatture, quindi non richiede movimenti bancari.
