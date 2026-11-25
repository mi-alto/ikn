# Modulo 1: Fondamenti e primi passi

---

## Slide 7: Fondamenti e primi passi

Tre domande a cui rispondiamo in questo modulo:

1. Cosa c'è dentro questi strumenti?
2. Quale scelgo, e cosa posso caricarci?
3. Dove mi fanno risparmiare tempo?

---

## Slide 8: Cos'è un modello di linguaggio

Un sistema che, dato un testo, calcola quale parola viene più probabilmente dopo.

- Ha letto una quantità enorme di testi
- Ha imparato come si scrive, e molte cose che in quei testi erano scritte
- Non è un archivio e non è un motore di ricerca

**Approfondimento**

- Il paragone più semplice è il suggerimento automatico della tastiera del telefono, ma enormemente più potente.
- Il modello non va a cercare la risposta da qualche parte: la compone, parola dopo parola.
- Per questo scrive benissimo anche quando il contenuto è sbagliato.

---

## Slide 9: I token

Il modello non legge parole intere. Legge pezzi di parola, chiamati token.

- Una parola comune è spesso un solo token
- Una parola lunga o rara viene divisa in più pezzi
- Anche i numeri vengono spezzati

| Testo | Come può essere diviso (esempio indicativo) |
|---|---|
| bilancio | bilancio |
| riconciliazione | ricon · cili · azione |
| 445.653.538 | 445 · . · 653 · . · 538 |

---

## Slide 10: Perché i token contano

- **I limiti si misurano in token.** Quanto testo regge una conversazione, quante richieste si possono fare al minuto.
- **Il costo si misura in token.** Si paga per il testo che entra e per quello che esce.
- **I numeri spezzati spiegano gli errori di calcolo.** Il modello non vede 445.653.538 come una quantità, ma come una fila di pezzi.

**Ordini di grandezza**

- Una pagina di testo: alcune centinaia di token
- Un bilancio annuale completo: centinaia di migliaia di token

---

## Slide 11: Contiamo i token

Esistono strumenti gratuiti in rete che mostrano come un testo viene diviso e quanti token occupa:

- **Tokenizer di OpenAI** (ufficiale, per i modelli GPT): https://platform.openai.com/tokenizer
- **Tiktokenizer** (per i modelli OpenAI, mostra anche il formato della conversazione)
- **The Tokenizer Playground** su Hugging Face (per i modelli aperti: Llama, Mistral, Gemma e altri)

**Prova**

1. Incollate una frase in italiano e la stessa frase in inglese
2. Incollate un numero lungo, per esempio 445.653.538
3. Incollate una riga di contabilità con data, descrizione e importo

**Cosa osservare**

- Lo stesso contenuto in italiano occupa più token che in inglese
- I numeri vengono spezzati in più pezzi
- Ogni modello conta in modo diverso: lo stesso testo dà numeri diversi

**Attenzione**

Sono strumenti pubblici: si incolla solo testo non riservato.

---

## Slide 12: Come lavora, il ciclo

1. Riceve una fila di token in ingresso
2. Calcola quale token è più probabile dopo, e lo scrive
3. Aggiunge quel token in fondo all'ingresso
4. Ricomincia dal punto 1

A ogni giro sceglie tra i token più probabili, con un po' di caso.

**Provate: la stessa domanda, due volte**

> Spiega in tre righe cos'è un rateo passivo.

Le due risposte dicono la stessa cosa con parole diverse.

**Approfondimento**

La variabilità non è un difetto: è il modo in cui il modello funziona. Quando serve un risultato sempre uguale bisogna dare un formato preciso. È il tema del modulo 2.

---

## Slide 13: I token speciali

Alcuni token non sono parole. Servono a dare ordine al testo: dove comincia un messaggio, chi sta parlando, dove finisce la risposta.

Sono scritti in modo che non si possano confondere con il testo normale. Qualche esempio reale:

- GPT-2 e GPT-3 (OpenAI), fine del testo: `<|endoftext|>`
- Formato di conversazione di OpenAI, inizio e fine di un messaggio: `<|im_start|>` e `<|im_end|>`
- Llama 3 (Meta), fine del turno: `<|eot_id|>`
- Mistral, inizio e fine del testo: `<s>` e `</s>`
- Mistral, richiesta dell'utente: `[INST]` e `[/INST]`
- Gemma (Google), inizio e fine del turno: `<start_of_turn>` e `<end_of_turn>`

**Il token di fine**

Significa "ho finito". Il modello lo prevede come prevede tutti gli altri token. Quando lo scrive, il ciclo si ferma.

---

## Slide 14: Una conversazione vista dal modello

Noi vediamo una conversazione ordinata. Il modello riceve un'unica fila di testo, con i token speciali che separano i ruoli:

```
<|im_start|>system
Sei un assistente per l'area finanza.<|im_end|>
<|im_start|>user
Cos'è un rateo passivo?<|im_end|>
<|im_start|>assistant
```

Da qui il modello comincia a scrivere, un token alla volta:

```
Un rateo passivo è un costo di competenza del periodo
che verrà pagato in un periodo successivo.<|im_end|>
```

L'ultimo token è quello di fine. Il programma che gestisce la conversazione lo riconosce, ferma il ciclo e mostra solo il testo.

---

## Slide 15: Quando il ciclo si interrompe

| Motivo | Cosa succede |
|---|---|
| Token di fine | Il modello ha previsto che la risposta è completa |
| Limite di lunghezza | Raggiunto il numero massimo di token in uscita, la risposta viene tagliata, anche a metà frase |
| Chiamata a uno strumento | Il modello scrive un token speciale che chiede un calcolo o una ricerca. Il ciclo si sospende, lo strumento lavora, il risultato entra nell'ingresso e il modello riparte |
| Interruzione | La persona preme il pulsante di arresto |

**Approfondimento**

- Una risposta troncata a metà non è un errore: è il limite di lunghezza. Basta chiedere di continuare.
- Il modello può prevedere la fine troppo presto. Su elenchi lunghi o tabelle va sempre controllato che il risultato sia completo.
- La sospensione per chiamare uno strumento è il meccanismo che sta sotto agli agenti. È il tema del modulo 3.

---

## Slide 16: I token di ragionamento

Alcuni modelli, prima di rispondere, scrivono una brutta copia: analizzano la domanda, provano una strada, si correggono. Sono i token di ragionamento (in inglese thinking o reasoning).

Non sono un meccanismo diverso. Sono token normali, prodotti dallo stesso ciclo, racchiusi tra due token speciali. Nei modelli aperti si vedono così:

```
<think>
La domanda chiede lo scostamento rispetto al budget.
Prima calcolo la differenza in valore, poi in percentuale.
Controllo che il segno sia coerente con la natura della voce.
</think>
Lo scostamento è di 1,2 milioni, pari al 4,8%.
```

Il programma che gestisce la conversazione nasconde la parte tra i due segni, oppure ne mostra un riassunto.

**Cosa comporta**

- **Migliorano i compiti in più passi.** Confronti, verifiche di coerenza, problemi con più condizioni.
- **Si pagano.** Contano come token in uscita, anche se non si vedono.
- **Occupano spazio e tempo.** La risposta arriva più lentamente.
- **Non sostituiscono il calcolo.** Un modello che ragiona sbaglia meno, ma i conti veri vanno comunque fatti da un programma.

**Approfondimento**

- Quasi tutti gli strumenti permettono di scegliere quanto far ragionare il modello: poco, medio, molto.
- Il ragionamento mostrato a schermo è spesso un riassunto, non la traccia completa.

---

## Slide 17: Come nasce un modello, primo passaggio

**Il pre-addestramento**

Il modello legge una quantità enorme di testi e si esercita su un solo compito: indovinare il token successivo. Sbaglia, viene corretto, riprova. Miliardi di volte.

**La ricetta è nota dal 2017**

L'architettura si chiama Transformer ed è stata descritta nell'articolo "Attention Is All You Need". Da allora la ricetta di base è rimasta quella. Sono cambiate le dosi.

**Tre ingredienti, tutti in crescita**

| Ingrediente | Cosa vuol dire |
|---|---|
| Dimensione del modello | Sempre più parametri, cioè più "manopole" da regolare |
| Potenza di calcolo | Sempre più processori specializzati ed energia |
| Dati | Una parte sempre più grande dei testi disponibili |

**Approfondimento**

- Addestrare un modello di punta oggi richiede investimenti alla portata di pochissime aziende al mondo.
- Per questo i fornitori sono pochi, e per questo conta sapere dove hanno sede e dove tengono i dati.

---

## Slide 18: Il modello del mondo

Per indovinare bene la parola successiva non basta la grammatica. Bisogna avere un'idea di come funzionano le cose.

Leggendo, il modello si costruisce una rappresentazione interna del mondo: in inglese world model.

- Sa che dopo un aumento dei tassi il costo del debito sale
- Sa come è fatto un bilancio e cosa segue cosa
- Sa come ragiona un revisore, un giurista, un analista

---

## Slide 19: Non è un'enciclopedia

- Un'enciclopedia conserva i fatti e li restituisce uguali
- Il modello conserva schemi e relazioni, e ricostruisce i fatti ogni volta

Quando la ricostruzione non ha appigli, il modello riempie il vuoto con qualcosa di plausibile. Si chiama confabulazione.

**Approfondimento**

- La confabulazione non è una bugia: il modello non sa di non sapere.
- È più probabile su nomi, date, numeri precisi, citazioni e riferimenti normativi. Proprio i dettagli che in finanza contano di più.

---

## Slide 20: Come nasce un modello, secondo passaggio

Dopo il pre-addestramento il modello sa continuare un testo. Non sa ancora fare l'assistente.

**L'apprendimento per rinforzo**

Il modello prova a svolgere un compito, riceve un voto, e viene spinto verso i comportamenti che ottengono i voti migliori.

| Cosa impara in questa fase | Esempio |
|---|---|
| A rispondere a una domanda, non solo a proseguire un testo | Dare una risposta e fermarsi |
| A ragionare per passi prima di rispondere | Scomporre un problema |
| A usare strumenti | Lanciare un calcolo, cercare in rete |
| A rispettare regole di comportamento | Rifiutare richieste pericolose |

**Approfondimento**

- I voti arrivano in parte da persone, in parte da controlli automatici (il programma funziona, il risultato è giusto).
- Due modelli con lo stesso pre-addestramento possono comportarsi in modo molto diverso dopo questo secondo passaggio.

---

## Slide 21: Misurare il progresso, la perplessità

La perplessità misura quanto il modello resta sorpreso dal token che viene davvero dopo, su testi che non ha mai visto.

Meno sorpresa, previsioni migliori. Più basso è il numero, più forte è il modello di base.

**I dati pubblicati da OpenAI**

Il 22 novembre 2026 il capo scienziato di OpenAI, Jakub Pachocki, ha pubblicato per la prima volta i valori interni dell'azienda (logaritmo della perplessità):

| Modello | Valore | Cosa compare a quel livello |
|---|---|---|
| GPT-3.5 | 0,986 | Conversazione scorrevole |
| GPT-4 | 0,913 | Ragionamento per passi che funziona |
| GPT-6.2 Astra | 0,761 | Primi risultati originali in matematica |
| Modello interno non pubblicato | 0,732 | |

Il grafico completo è nell'articolo "Perplexity and Intelligence":
https://openai.com/index/perplexity-and-intelligence/

---

## Slide 22: Come leggere la perplessità

- Le capacità nuove non arrivano in modo graduale: compaiono quando il valore scende sotto certe soglie.
- La differenza tra 0,99 e 0,76 sembra piccola. In pratica separa un modello che chiacchiera da uno che fa scoperte.

**I limiti della misura, dichiarati dall'autore**

- Non misura quanto un modello è utile in un lavoro concreto
- Non vede i miglioramenti ottenuti dopo il pre-addestramento, come il ragionamento per passi
- Ogni laboratorio usa testi di prova diversi, quindi i valori non sono confrontabili tra aziende

**Approfondimento**

L'articolo propone di adottare questa misura in tutto il settore, anche per fissare limiti comuni allo sviluppo. È una proposta in discussione, non uno standard.

---

## Slide 23: Le classifiche indipendenti

La perplessità è una misura interna dei laboratori. Per confrontare i modelli dall'esterno esistono siti indipendenti che li provano tutti con lo stesso metodo.

Il più usato è Artificial Analysis: https://artificialanalysis.ai

**Cosa misura**

| Famiglia | Cosa dice | Come si legge |
|---|---|---|
| Qualità | Un indice da 0 a 100 che riassume più prove: lavoro d'ufficio, programmazione, scienze, cultura generale | Più alto è meglio |
| Velocità | Quanti token al secondo scrive il modello, e quanto aspetta prima di cominciare | Più veloce è meglio |
| Prezzo | Quanto costa un milione di token in ingresso e in uscita, e quanto costa in media un compito | Più basso è meglio |

**Perché è utile**

- Le prove sono fatte da un terzo, non da chi vende il modello
- Lo stesso modello viene misurato presso fornitori diversi: stessa qualità, velocità e prezzi differenti
- I grafici mettono insieme qualità e prezzo, e fanno vedere subito chi offre di più a parità di spesa

---

## Slide 24: Come leggere una classifica

**Cosa una classifica non dice**

- **Non misura il vostro lavoro.** Le prove riguardano compiti generali, non una riconciliazione o la lettura di un contratto di fornitura.
- **È in inglese e quasi tutta su testo.** Dice poco su come un modello se la cava in italiano o con tabelle scansionate.
- **Un numero solo nasconde le differenze.** Due modelli con lo stesso indice possono essere uno forte nella programmazione e uno nell'analisi di documenti.
- **Invecchia in fretta.** La classifica cambia ogni poche settimane, e ogni tanto cambia anche il metodo di calcolo.

**Come usarla**

1. Guardare la classifica per restringere la scelta a due o tre modelli
2. Controllare velocità e prezzo, non solo la qualità
3. Provare i candidati sui propri documenti, con le proprie domande

**Approfondimento**

La prova migliore è sempre la propria: dieci domande tipiche del proprio lavoro, con la risposta giusta già nota. È quello che facciamo nell'esercizio di questo modulo, in piccolo.

---

## Slide 25: Modelli piccoli, medi e grandi

Ogni fornitore offre lo stesso modello in più taglie.

| Taglia | Caratteristiche | Adatto a |
|---|---|---|
| Piccola | Veloce ed economica, meno precisa | Compiti semplici e ripetuti in grande quantità: classificare, estrarre un dato, smistare |
| Media | Buon equilibrio | La maggior parte del lavoro quotidiano |
| Grande | Più capace, più lenta, più costosa | Analisi complesse, documenti lunghi, problemi in più passi |

---

## Slide 26: I nomi delle taglie, per fornitore

| Fornitore | Piccola | Media | Grande |
|---|---|---|---|
| OpenAI | nano, mini | versione base | versioni "pro" |
| Anthropic | Haiku | Sonnet | Opus |
| Google | Flash-Lite | Flash | Pro |
| Mistral | Small | Medium | Large |

**Approfondimento**

- La differenza di costo tra la taglia piccola e la grande può essere di decine di volte.
- Regola pratica: partire dalla media, scendere alla piccola per i compiti ripetitivi, salire alla grande quando la risposta non convince.
- I modelli gratuiti sono in genere taglie piccole o medie.

---

## Slide 27: Modelli multimodali

Un modello multimodale non lavora solo sul testo.

| In ingresso | Esempi in finanza |
|---|---|
| Immagini | Fattura scansionata, fotografia di un documento, grafico di una relazione |
| Documenti impaginati | PDF con tabelle, intestazioni, note a piè di pagina |
| Audio | Registrazione di una riunione o di una presentazione dei risultati |
| Video | Registrazione di un incontro con schermo condiviso |

In uscita può produrre testo, immagini, voce.

**Come funziona**

Anche un'immagine viene trasformata in token. Il modello li riceve nella stessa fila di quelli del testo.

**Approfondimento**

- Leggere un numero da un'immagine è più soggetto a errori che leggerlo da un testo. Una virgola spostata o una cifra scambiata sono gli errori tipici.
- Un'immagine occupa molti token: un documento scansionato pesa più dello stesso documento in formato testo.
- L'estrazione di dati dai documenti è il tema del modulo 4.

---

## Slide 28: Tre limiti da ricordare

1. **Può inventare (confabulazione).** E lo fa con tono sicuro.
2. **Non fa i conti a mente.** Scrive numeri che sembrano giusti.
3. **Sa le cose fino a una certa data.** Dopo, non sa o inventa.

**Approfondimento**

- Questi tre limiti si riducono con i modelli migliori, ma non spariscono.
- La soluzione è dare al modello il documento e far fare i conti a un programma. Sono i temi dei moduli 3 e 4.

---

## Slide 29: Due prove dal vivo

**Il calcolo**

> Quanto fa 48.367 per 9.214? Rispondi solo con il numero.

Risultato corretto: 445.653.538.

**Il fatto recente**

> Qual è stato l'utile netto di un grande gruppo quotato dell'energia nell'ultimo trimestre?

Senza un documento allegato, il modello o dichiara di non saperlo, o propone un numero da confrontare con quello vero.

---

## Slide 30: L'ancoraggio alle fonti

In inglese grounding. Vuol dire dare al modello una fonte su cui appoggiare la risposta, invece di lasciarlo rispondere a memoria.

| | Senza ancoraggio | Con ancoraggio |
|---|---|---|
| Da dove viene la risposta | Da quello che il modello ha imparato in addestramento | Da un documento o da una ricerca fatta in quel momento |
| Fatti recenti | Non li conosce, o li inventa | Li trova |
| Numeri e date | Ricostruiti, quindi a rischio | Copiati dalla fonte |
| Verifica | Impossibile: non c'è una fonte | Possibile: la fonte è indicata |

**Tre modi per ancorare**

1. Allegare il documento alla conversazione
2. Collegare una ricerca in rete, per esempio con un collegamento MCP
3. Collegare un archivio aziendale

**Approfondimento**

- Con l'ancoraggio il modello smette di essere la fonte e diventa chi legge la fonte.
- L'ancoraggio riduce le invenzioni, non le elimina. La fonte indicata va aperta e controllata.
- Una ricerca in rete trova anche pagine sbagliate o di parte. La qualità della risposta dipende dalla qualità della fonte.

---

## Slide 31: Il modello non ha memoria

Il modello vede solo quello che gli arriva in ingresso, in quel momento.

- Non ha memoria tra una richiesta e l'altra
- Non ricorda la domanda di un minuto fa
- Non conosce i file, la posta, i sistemi aziendali

Ogni richiesta, per il modello, è la prima.

**Approfondimento**

Se una conversazione sembra continua, è perché qualcuno gliela ripresenta ogni volta. Quel qualcuno è il programma costruito intorno al modello.

---

## Slide 32: L'imbracatura intorno al modello

Il programma che sta intorno al modello si chiama imbracatura (in inglese harness). È quello che usiamo quando apriamo ChatGPT, Copilot, Gemini o Claude.

**Cosa fa a ogni richiesta**

1. Prende la nuova domanda
2. Ci aggiunge le istruzioni di fondo
3. Ci aggiunge tutta la conversazione precedente
4. Ci aggiunge il contenuto dei file caricati
5. Manda tutto insieme al modello
6. Riceve la risposta e la mostra

---

## Slide 33: Cosa aggiunge l'imbracatura

| Il modello da solo | L'imbracatura |
|---|---|
| Riceve token, restituisce token | Ripropone conversazione e file a ogni richiesta |
| | Cerca in rete |
| | Esegue calcoli con un programma |
| | Conserva preferenze e ricordi |
| | Si collega ad altri programmi |

Il modello è il motore. L'imbracatura è l'automobile.

**Approfondimento**

- Lo stesso modello si comporta in modo molto diverso a seconda dell'imbracatura.
- Un'imbracatura si può configurare: istruzioni, skill, collegamenti. È il tema del modulo 3.

---

## Slide 34: La finestra di contesto

La finestra di contesto è la quantità massima di token che il modello può ricevere in una volta.

Dentro ci deve stare tutto: istruzioni, conversazione, file, e la risposta da scrivere.

**Cosa succede quando si riempie**

L'imbracatura deve scegliere cosa lasciare fuori:

- taglia i messaggi più vecchi
- oppure li sostituisce con un riassunto
- oppure passa solo alcune parti dei file

In tutti i casi il modello non vede più una parte del materiale, e non lo dice.

---

## Slide 35: Il degrado del contesto

In inglese context rot. Più la conversazione si allunga, più la qualità delle risposte scende. Succede molto prima di arrivare al limite della finestra.

**Perché succede**

- **L'attenzione si diluisce.** Con molto materiale, il modello dà meno peso a ogni singola parte.
- **Il centro si perde.** Ricorda meglio l'inizio e la fine. Quello che sta in mezzo viene trascurato.
- **Gli errori restano dentro.** Tentativi sbagliati e versioni superate continuano a essere riletti a ogni richiesta, e influenzano le risposte successive.
- **Le istruzioni si contraddicono.** Una correzione data a metà convive con l'istruzione originale.

**Come si riconosce**

- Il modello dimentica un'istruzione data all'inizio
- Ripete un errore già corretto
- Confonde i numeri di un documento con quelli di un altro
- Le risposte diventano più vaghe

**Cosa fare**

- Aprire una conversazione nuova, portando solo un riassunto di quello che serve
- Togliere il materiale che non serve più
- Ripetere l'istruzione importante vicino alla domanda

**Approfondimento**

Una conversazione lunga non è una conversazione più informata. Oltre una certa soglia, aggiungere materiale peggiora il risultato.

---

## Slide 36: Tre abitudini

- Argomento nuovo, conversazione nuova
- Estratti mirati, non documenti di 300 pagine
- Le informazioni importanti si ripetono, non si danno per ricordate

**Approfondimento**

- Ogni richiesta rimanda al modello tutta la conversazione: più è lunga, più costa e più è lenta.
- Su un bilancio intero il modello può non ricevere una nota a pagina 180. Per questo conviene lavorare su estratti.

---

## Slide 37: Due tipi di memoria

Quando uno strumento "ricorda", sta facendo una di queste due cose.

| | Memoria della conversazione | Memoria tra conversazioni |
|---|---|---|
| Cos'è | I messaggi precedenti, rimandati al modello a ogni richiesta | Appunti che lo strumento salva e reinserisce nelle conversazioni future |
| Quanto dura | Finché resta aperta quella conversazione | Finché non viene cancellata |
| Limite | La finestra di contesto | Uno spazio massimo fissato dallo strumento |
| Chi decide cosa entra | Tutto, fino al limite | Lo strumento, che sceglie cosa annotare |

In entrambi i casi il modello non ricorda nulla. È l'imbracatura che rimette il testo in ingresso.

**Cosa si può regolare**

- Accendere o spegnere la memoria tra conversazioni
- Vedere, correggere e cancellare gli appunti salvati
- Fissare quanta parte della conversazione viene rimandata al modello

**Approfondimento**

- La memoria tra conversazioni è comoda, ma porta informazioni di un lavoro dentro un altro. Su temi riservati conviene spegnerla.
- Quello che finisce in memoria è un dato conservato dal fornitore: valgono le stesse domande su durata e accessi.

---

## Slide 38: Gli strumenti

| Strumento | Chi lo fa | Dove vive |
|---|---|---|
| ChatGPT | OpenAI | Sito e applicazione propri |
| Copilot | Microsoft | Dentro Word, Excel, Outlook, Teams |
| Gemini | Google | Dentro Gmail, Documenti, Fogli |
| Claude | Anthropic | Sito e applicazione propri |

**Quattro cose da guardare**

1. Qualità delle risposte
2. Capacità di analisi su file e numeri
3. Quanta documentazione regge in una conversazione
4. Tutela dei dati

**Approfondimento**

- Le differenze di qualità cambiano ogni pochi mesi.
- La differenza che resta è dove vive lo strumento: Copilot e Gemini lavorano sui documenti e sulla posta dell'ufficio, gli altri due partono da una pagina vuota.

---

## Slide 39: America, Europa, Cina

| Area | Esempi |
|---|---|
| America | OpenAI, Anthropic, Google |
| Europa | Mistral |
| Cina | Z.ai, DeepSeek, Alibaba |

Due domande diverse:

- **Dove è nato il modello?** Dice chi l'ha addestrato e con quali regole.
- **Dove gira?** Dice dove vanno i dati.

**Approfondimento**

- Un modello cinese può girare su un server americano o europeo. Un modello aperto può girare sul proprio computer, e i dati non vanno a nessuno.
- Negli esercizi di oggi usiamo un modello per area, a scopo di confronto: Gemini, Mistral e GLM.

---

## Slide 40: Modelli chiusi e modelli aperti

| | Modello chiuso | Modello aperto |
|---|---|---|
| Cosa vuol dire | Il modello resta presso chi lo ha creato. Si usa solo attraverso il suo servizio | Il modello si può scaricare e far girare dove si vuole |
| Esempi | GPT (OpenAI), Claude (Anthropic), Gemini (Google) | Llama (Meta), Gemma (Google), Qwen (Alibaba), DeepSeek, alcuni modelli Mistral e GLM |
| Punto di forza | Di solito sono i più capaci | Controllo completo su dove vanno i dati |
| Punto debole | Dipendenza dal fornitore e dalle sue regole | Servono competenze e macchine per farli girare |

**Approfondimento**

- "Aperto" riguarda il modello, non i dati su cui è stato addestrato, che restano quasi sempre non pubblici.
- Aperto non vuol dire senza regole: ogni modello ha una licenza che dice cosa se ne può fare.
- Lo stesso fornitore può avere modelli chiusi e modelli aperti.

---

## Slide 41: Modelli remoti e modelli locali

| | Remoto | Locale |
|---|---|---|
| Dove gira | Sui server del fornitore, raggiunti via rete | Su un computer o un server dell'azienda |
| Dati | Escono dall'azienda | Restano in azienda |
| Qualità | Accesso ai modelli più capaci | Limitata dalla potenza delle proprie macchine |
| Costo | A consumo o in abbonamento | Acquisto e gestione delle macchine |
| Avvio | Immediato | Richiede installazione e manutenzione |

**Le combinazioni possibili**

- **Chiuso e remoto:** il caso più comune. ChatGPT, Claude, Gemini, Copilot.
- **Aperto e locale:** il massimo controllo sui dati.
- **Aperto e remoto:** un modello aperto fatto girare da un fornitore terzo, per non gestire le macchine.

**Una via di mezzo**

Molti fornitori offrono il servizio remoto in una regione europea, con impegni scritti su dove i dati vengono trattati.

---

## Slide 42: Come scegliere

Tre domande, in quest'ordine:

1. Cosa permette l'azienda?
2. Che dati devo usare?
3. Che lavoro devo fare?

**Approfondimento**

La prima domanda chiude quasi sempre la questione: lo strumento giusto è quello autorizzato.

---

## Slide 43: Sicurezza dei dati, tre livelli

| Livello | Cosa succede ai dati | Esempio |
|---|---|---|
| Servizi gratuiti per il pubblico | Possono servire a migliorare il servizio | Versioni gratuite |
| Piani aziendali con contratto | Restano riservati, con regole scritte | Copilot aziendale, piani per le imprese |
| Modelli installati in casa | Non escono dall'azienda | Modelli aperti su server propri |

**Approfondimento**

- Gratis non vuol dire senza costo: spesso si paga con i dati.
- La differenza la fa il contratto, non la marca.
- Negli esercizi di oggi usiamo servizi gratuiti, quindi solo dati pubblici o inventati.

---

## Slide 44: Cosa non si carica mai

Su uno strumento non autorizzato dall'azienda:

- Contratti e condizioni commerciali
- Prezzi e margini non pubblici
- Dati personali di dipendenti, clienti, fornitori
- Numeri di bilancio prima della pubblicazione

**Approfondimento**

- In una società quotata i risultati non ancora pubblicati sono informazioni riservate, con regole precise su chi può conoscerle.
- Regola pratica: quello che non si manderebbe per posta a un estraneo, non si carica.
- Nei casi dubbi decide la funzione aziendale che si occupa di sicurezza o di conformità.

---

## Slide 45: Come leggere le regole di un fornitore

Prima di usare uno strumento con dati aziendali, sette domande:

1. **I miei dati servono ad addestrare i modelli?** Qual è l'impostazione di partenza, e come si cambia?
2. **Per quanto tempo vengono conservati, e perché?**
3. **Chi può leggerli?** Personale del fornitore, società esterne, in quali casi?
4. **Dove vengono trattati?** In quale paese o regione?
5. **A quali altri fornitori vengono passati?**
6. **Quali certificazioni di sicurezza ha il fornitore?**
7. **C'è un contratto per il trattamento dei dati?**

**Dove si trovano le risposte**

- Condizioni d'uso e informativa sulla riservatezza
- Accordo sul trattamento dei dati (in inglese DPA)
- La pagina del fornitore dedicata a sicurezza e conformità

**Approfondimento**

- Lo stesso prodotto ha regole diverse nella versione per il pubblico e in quella per le aziende.
- Se un dipendente usa un abbonamento personale, ai dati aziendali si applicano le regole per il pubblico.

---

## Slide 46: Conservazione zero dei dati (ZDR)

**L'impostazione di partenza**

Quasi tutti i fornitori conservano richieste e risposte per un certo periodo, in genere intorno a 30 giorni, per controllare gli abusi. In alcuni casi il personale può leggerle.

**Cos'è la conservazione zero**

In inglese Zero Data Retention, in sigla ZDR. Il fornitore elabora la richiesta, restituisce la risposta e non conserva nulla.

**Cosa sapere**

- Di norma non è attiva: va richiesta, e spesso serve un'approvazione
- Non copre tutte le funzioni: file caricati, memoria e conversazioni salvate restano fuori
- Non è disponibile per tutti i modelli: nel 2026 alcuni fornitori hanno imposto un periodo di conservazione per i loro modelli più avanzati

**La regola**

Chiedere sempre la conservazione zero. Se non è disponibile, farsi mettere per iscritto durata, scopo e chi ha accesso.

---

## Slide 47: Il GDPR

Il regolamento europeo sulla protezione dei dati si applica ogni volta che nei dati ci sono persone: nomi su una fattura, dipendenti, referenti di clienti e fornitori.

**I punti che contano quando si usa l'AI**

| Tema | Cosa vuol dire in pratica |
|---|---|
| Ruoli | L'azienda decide perché e come usare i dati. Il fornitore li tratta per suo conto, e serve un accordo scritto |
| Minimizzazione | Si caricano solo i dati necessari. Se i nomi non servono, si tolgono |
| Finalità | I dati raccolti per uno scopo non si usano per un altro senza una base |
| Valutazione d'impatto | Per i trattamenti più rischiosi va fatta prima di cominciare |
| Diritti delle persone | Accesso, rettifica, cancellazione valgono anche qui |

**Approfondimento**

Un'abitudine utile: prima di caricare un documento, chiedersi se i dati personali servono davvero all'analisi. Spesso basta sostituire i nomi con un codice.

---

## Slide 48: Trasferire dati fuori dall'Europa

Il GDPR non vieta di portare dati personali fuori dall'Europa. Lo permette a certe condizioni.

| Strada | Come funziona |
|---|---|
| Decisione di adeguatezza | La Commissione europea riconosce che un paese protegge i dati in modo equivalente. Vale per esempio per Regno Unito, Svizzera, Giappone |
| Stati Uniti | Adeguatezza limitata alle aziende certificate nel Data Privacy Framework |
| Clausole contrattuali tipo | Contratto con testo fissato dalla Commissione, più una valutazione del paese di destinazione |
| Regole vincolanti d'impresa | Per i trasferimenti dentro uno stesso gruppo |
| Deroghe | Solo per casi specifici e occasionali |

**Lo stato delle cose**

- L'accordo con gli Stati Uniti è in vigore. Il Tribunale dell'Unione lo ha confermato nel settembre 2025. È pendente un ricorso alla Corte di giustizia.
- Per la Cina non esiste una decisione di adeguatezza: servono clausole contrattuali e una valutazione approfondita.

**Approfondimento**

- Molti fornitori permettono di scegliere una regione europea per il trattamento. Semplifica, ma va verificato cosa resta davvero in Europa.
- Nei settori regolati si aggiungono le regole di settore e quelle interne del gruppo.

---

## Slide 49: L'AI Act, i livelli di rischio

Il regolamento europeo sull'intelligenza artificiale classifica gli usi per livello di rischio.

| Livello | Esempi | Cosa comporta |
|---|---|---|
| Vietato | Manipolazione, punteggio sociale | Non si può fare |
| Alto rischio | Selezione del personale, valutazione del credito delle persone | Obblighi stringenti |
| Trasparenza | Assistenti che conversano, contenuti generati | Dichiarare che si tratta di AI |
| Rischio minimo | Sintesi, analisi, supporto alla scrittura | Nessun obbligo specifico |

---

## Slide 50: L'AI Act, le date

| Da quando | Cosa si applica |
|---|---|
| 2 febbraio 2025 | Divieti e alfabetizzazione del personale |
| 2 agosto 2025 | Regole per i modelli di uso generale |
| 2 agosto 2026 | Obblighi di trasparenza |
| 2 dicembre 2027 | Sistemi ad alto rischio (rinviati dal 2026) |
| 2 agosto 2028 | AI dentro prodotti già regolati |

**Approfondimento**

- La maggior parte degli usi in una funzione finanza ricade nel rischio minimo o nella trasparenza.
- L'articolo 4 chiede alle aziende di adottare misure perché il personale sappia usare l'AI in modo consapevole. La formazione è una di queste misure.
- Questa è una panoramica di orientamento. Le valutazioni sui singoli casi spettano alle funzioni legale e di conformità.

---

## Slide 51: Dove aiuta nella finanza

| | Analisi del documento | Analisi dei numeri |
|---|---|---|
| **Accounting & Balance** | Fatture, contratti a fini contabili, note al bilancio, rapporto con i revisori, principi contabili | Riconciliazioni, chiusure, controllo delle anomalie |
| **Origination & Analysis** | Ricerca di opportunità, controparti, confronto di contratti, documenti per l'approvazione, norme | Previsioni, simulazioni, modelli di calcolo |

**Approfondimento**

- Sui documenti il modello è già molto utile da solo.
- Sui numeri è utile quando i conti li fa un programma.

---

## Slide 52: La chiave di accesso

Per usare un modello da un programma esterno serve una chiave di accesso, in inglese API key. È una lunga stringa di caratteri che identifica chi sta facendo la richiesta.

Attenzione ai nomi: la chiave di accesso non ha nulla a che vedere con i token in cui viene diviso il testo.

**A cosa serve**

- Dice al fornitore chi sta chiamando
- Lega l'uso ai limiti e ai costi di quel conto

**Come si tratta**

- È come una password: non si condivide e non si incolla in una conversazione
- Si può revocare e rigenerare in qualsiasi momento
- Conviene crearne una per ogni uso, così se ne revoca una senza fermare le altre

**Dove si crea, per i fornitori gratuiti di oggi**

| Fornitore | Dove |
|---|---|
| Google (Gemini) | Google AI Studio, sezione delle chiavi |
| Mistral | Console di Mistral, sezione delle chiavi |
| Z.ai (GLM) | Piattaforma di Z.ai, sezione delle chiavi, accesso "Standard" |

---

## Slide 53: Esercizio 1, prima parte. Preparare l'ambiente

1. Scegliete uno dei tre fornitori: Gemini, Mistral o GLM
2. Create un conto sul sito del fornitore
3. Generate la vostra chiave di accesso e copiatela
4. Aprite chat.deep4it.com ed entrate con le vostre credenziali
5. Scegliete il fornitore dal menu dei modelli e inserite la chiave quando viene richiesta
6. Scrivete una prima domanda e controllate che arrivi la risposta

**Cosa osservare**

- Nel sito del fornitore compare il consumo: quante richieste, quanti token
- Con la stessa chiave si possono usare più modelli dello stesso fornitore, di taglie diverse

---

## Slide 54: Esercizio 1, seconda parte. La memoria

**Prova 1: la memoria della conversazione**

1. Scrivete: "Lavoro nell'area Accounting & Balance e mi occupo di chiusure mensili."
2. Fate due o tre domande su altro
3. Chiedete: "Di cosa mi occupo?"

**Prova 2: conversazione nuova**

1. Aprite una conversazione nuova
2. Chiedete di nuovo: "Di cosa mi occupo?"

**Prova 3: la memoria tra conversazioni**

1. Accendete la memoria dalle impostazioni
2. Scrivete: "Ricorda che voglio sempre le risposte in forma di tabella."
3. Aprite una conversazione nuova e fate una domanda qualsiasi
4. Aprite il pannello delle memorie: guardate cosa è stato annotato, poi cancellatelo

**Prova 4: una finestra più stretta**

1. Nei parametri della conversazione riducete il limite di contesto
2. Continuate a conversare, poi chiedete un dettaglio detto all'inizio

**Cosa osservare**

In quale prova il modello "ricorda", in quale no, e perché.

---

## Slide 55: Esercizio 1, terza parte. L'ancoraggio alle fonti

**Prova 1: senza ricerca**

Con la ricerca in rete spenta, chiedete:

> Qual è stato l'utile netto dell'ultimo trimestre di un grande gruppo quotato dell'energia a vostra scelta? Indica la fonte.

**Prova 2: con la ricerca**

Accendete la ricerca in rete e ripetete la stessa domanda.

**Prova 3: la verifica**

Aprite la fonte indicata e controllate il numero.

**Cosa osservare**

- Senza ricerca: il modello dichiara di non sapere, oppure dà un numero senza fonte o con una fonte inesistente
- Con la ricerca: la risposta cita pagine reali
- La fonte citata dice davvero quello che il modello riporta?

**Cosa resta**

Un modello senza fonte ricostruisce. Un modello con una fonte legge. In entrambi i casi il numero si verifica.
