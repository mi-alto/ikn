# Modulo 5 — Carica l’Excel, scarica il report

Un modulo n8n riceve un Excel di fatture e una soglia in euro. Il flusso seleziona le fatture del giorno di riferimento, calcola lo scostamento tra importo fatturato e atteso e restituisce un nuovo Excel con l’esito dei controlli.

Scarica [fatture.xlsx](fatture.xlsx) e tienilo a portata di mano. Per questa prova, la data di riferimento è il **26 novembre 2026**. Il file contiene tre fatture fittizie.

## 1. Crea la pagina di caricamento

1. Entra in [n8n Cloud](https://app.n8n.cloud/), crea un workflow e chiamalo **Controllo fatture**.
2. Aggiungi **n8n Form Trigger**, che può comparire come **On form submission** nel selettore. Inserisci come titolo **Controllo fatture**.
3. In **Form Elements**, aggiungi i due campi qui sotto. Se l’interfaccia mostra **Field Name**, usa i nomi indicati. Se il nome è ricavato dall’etichetta, usa esattamente la stessa etichetta.

   | Etichetta | Nome | Tipo | Obbligatorio |
   |---|---|---|---|
   | Excel | `Excel` | File | Sì |
   | Soglia | `Soglia` | Number | Sì |

4. Se disponibile, limita il campo Excel a un solo file con estensione `.xlsx`. In **Respond When** scegli **Workflow Finishes**.
5. Rinomina il nodo **Carica Excel**. Avvia **Execute Step** sul nodo e apri il **Test URL**. Carica `fatture.xlsx` e inserisci **100**. Nel risultato del nodo controlla che la soglia sia presente e che nella scheda **Binary** compaia il file. Annota la chiave del file mostrata lì, di norma `Excel`.

## 2. Leggi le righe dell’Excel

1. Collega **Extract From File** al modulo e seleziona **Extract From XLSX**.
2. In **Input Binary Field** inserisci la chiave vista nella scheda Binary. Seleziona il foglio **Fatture** e usa la prima riga come intestazione.
3. Esegui il passaggio e controlla che escano **tre righe** con i campi `id_fattura`, `data_registrazione`, `importo_atteso_eur` e `importo_fatturato_eur`.

## 3. Seleziona le fatture del giorno

1. Collega **Filter**. Nella condizione usa il campo `data_registrazione` trascinandolo dall’input, oppure incolla `{{ $json.data_registrazione }}` in modalità **Expression**.
2. Scegli il confronto testuale **is equal to** e inserisci `2026-11-26` come valore fisso. Devono passare solo F02 e F03.

## 4. Calcola lo scostamento e assegna l’esito

1. Aggiungi **Edit Fields (Set)**. Mantieni tutti i campi in ingresso con **Include in Output → All Input Fields** oppure con **Include Other Input Fields** attivo, secondo la versione.
2. Aggiungi `scostamento_eur` di tipo **Number**. Passa a **Expression** e incolla:

   ```text
   {{ Number($json.importo_fatturato_eur) - Number($json.importo_atteso_eur) }}
   ```

3. Aggiungi un secondo **Edit Fields (Set)**, mantieni tutti i campi in ingresso e crea `esito` di tipo **String**. In **Expression** incolla:

   ```text
   {{ Math.abs($json.scostamento_eur) > Number($('Carica Excel').first().json.Soglia) ? 'Da verificare' : 'OK' }}
   ```

   La differenza può essere positiva o negativa. La verifica scatta quando il suo valore assoluto supera la soglia del modulo.

## 5. Crea e restituisci il report

1. Collega **Convert to File → Convert to XLSX**. Imposta **Put Output File in Field** su `report`. Nelle opzioni indica **File Name** `controlli.xlsx`, **Sheet Name** `Controlli` e attiva **Header Row**.
2. Collega un nodo **n8n Form** dopo la conversione. Imposta **Page Type → Form Ending** e **On n8n Form Submission → Return Binary File**.
3. In **Input Data Field Name** scrivi `report`. Come titolo finale puoi usare **Report pronto**.

## 6. Prova il flusso completo

1. Salva e avvia **Execute Workflow**. Apri il **Test URL** del primo nodo, carica lo stesso Excel e inserisci **100**. Apri il report scaricato.
2. Riavvia **Execute Workflow** e ripeti con soglia **40**. Se n8n mostra che il modulo di test è in attesa, invia il file dalla pagina del modulo.

| Fattura | Scostamento | Soglia 100 € | Soglia 40 € |
|---|---:|---|---|
| F02 | +50 € | OK | Da verificare |
| F03 | +150 € | Da verificare | Da verificare |

F01 è registrata il 25 novembre e resta fuori. Se il report manca, apri l’esecuzione e controlla in ordine che il primo nodo abbia ricevuto l’Excel, che il filtro abbia prodotto due righe e che **Convert to File** abbia creato il file nel campo `report`.

## Documentazione ufficiale

- [Form Trigger, campi e modalità di test](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.formtrigger/)
- [Extract From File](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.extractfromfile/)
- [Filter](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.filter/)
- [Edit Fields](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.set/)
- [Convert to File](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.converttofile/)
- [Form Ending e restituzione del file](https://docs.n8n.io/integrations/builtin/core-nodes/n8n-nodes-base.form/)
