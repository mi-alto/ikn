# Modulo 6 — Automazione agentica con n8n

---

## Slide 122 — Quando inserire un agente nel workflow

- Nel modulo 5 abbiamo usato una regola per calcolare lo scostamento di una fattura e segnalarlo sopra una soglia.
- Dopo la segnalazione può servire capire quali informazioni consultare e quale verifica proporre. È una decisione che possiamo delegare a un agente.
- I nodi del workflow continuano ad applicare le formule e le soglie definite dal team.

---

## Slide 123 — I componenti nel canvas di n8n

- Il trigger avvia l’esecuzione. I nodi a monte preparano i dati e li passano al nodo **AI Agent**.
- All’agente si collegano un **Chat Model**, gli **strumenti** che può chiamare e, se serve, la **memoria**.
- I nodi a valle ricevono il risultato e applicano le verifiche o le azioni previste dal workflow.

---

## Slide 124 — Obiettivo e istruzioni dell’agente

- L’obiettivo descrive il risultato da ottenere. Le istruzioni stabiliscono quali fonti usare, quali azioni sono ammesse e quando chiedere un intervento umano.
- Nel nodo AI Agent le istruzioni stabili possono andare nel **System Message**. La richiesta e i dati del singolo caso arrivano in ingresso.
- Un buon obiettivo rende riconoscibile il momento in cui il lavoro è completo.

---

## Slide 125 — Il ruolo del Chat Model

- Il Chat Model interpreta la richiesta e valuta se rispondere direttamente oppure invocare uno strumento.
- Scegli un modello compatibile con l’uso degli strumenti. Configura nel nodo del provider le credenziali e il modello da chiamare.
- n8n esegue le chiamate e passa al modello i risultati. Il modello può così decidere il passo successivo.

---

## Slide 126 — Il ciclo di lavoro dell’agente

- L’agente valuta l’obiettivo, sceglie un’azione e osserva il risultato.
- Se una fonte chiarisce solo una parte del caso, può consultare un altro strumento. Se le evidenze bastano, può preparare la risposta.
- In n8n **Max Iterations** limita il numero di iterazioni. Le istruzioni dicono come chiudere il caso quando mancano informazioni.

---

## Slide 127 — A cosa serve la memoria

- In un workflow conversazionale, la memoria conserva i messaggi precedenti per riprendere un riferimento come «quella fattura».
- **Simple Memory** associa lo storico a una chiave di sessione. La finestra di contesto della memoria determina quanto storico recuperare.
- Lo storico dei controlli, gli esiti approvati e i documenti di lavoro vanno conservati in fonti che il workflow può consultare.

---

## Slide 128 — Che cosa può essere uno strumento

- Uno strumento è un’operazione che l’agente può invocare. Può leggere una tabella, interrogare un servizio o eseguire un altro workflow.
- Il nome e la descrizione spiegano al modello quando usarlo. L’input definisce che cosa deve passargli, per esempio l’ID della fattura.
- L’output torna all’agente come nuova informazione su cui basare la decisione.

---

## Slide 129 — Chi decide i parametri dello strumento

- Alcuni parametri li fissiamo nel workflow. Per esempio, quale tabella può essere consultata.
- Altri dipendono dalla richiesta. Con **$fromAI()** n8n può chiedere al modello di valorizzare un parametro dello strumento, come l’ID cercato.
- La descrizione del parametro spiega che cosa estrarre. Verifica il valore prima di usarlo per operazioni che modificano dati.

---

## Slide 130 — Un agente può consultare un altro agente

- Con **AI Agent Tool**, un agente principale può chiamare un altro agente come strumento e affidargli un compito specifico.
- Lo specialista riceve la richiesta di delega, svolge il compito e restituisce il risultato al coordinatore.
- Se la revisione deve avvenire sempre, collega analisi e revisione in sequenza nel workflow e passa esplicitamente i dati al secondo agente.

---

## Slide 131 — Restituire un risultato che il flusso può usare

- Definisci i campi dell’output prima di costruire i nodi successivi. Per una fattura possono servire ID, scostamento, evidenza e prossima verifica.
- Distingui ciò che risulta dalla fonte da ciò che l’agente propone. Una spiegazione del fornitore può richiedere riscontro.
- Controlla che i campi essenziali siano presenti e manda i casi incompleti al percorso di revisione.

---

## Slide 132 — Controllo umano e tracciabilità

- L’agente può raccogliere elementi e preparare una proposta. Il workflow può richiedere un’approvazione prima di attività come aggiornare un registro o inviare una comunicazione.
- Nella cronologia di esecuzione controlliamo i dati ricevuti, gli strumenti chiamati e le conclusioni prodotte.
- Proviamo anche un caso con fonte mancante e uno con fonti discordanti per verificare il percorso di revisione.

---

## Slide 133 — Riferimenti ufficiali n8n da mostrare

- [n8n Academy — AI201 Introduction to Agents](https://learn.n8n.io/) per orientarsi nel canvas e riconoscere i componenti di un agente.
- [Esempio sui parametri degli strumenti](https://docs.n8n.io/build/integrate-ai/ai-examples/use-ai-for-parameters.md) per vedere come il modello può compilare un campo.
- [Simple Memory](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.memorybufferwindow/) e [AI Agent Tool](https://docs.n8n.io/integrations/builtin/cluster-nodes/sub-nodes/n8n-nodes-langchain.toolaiagent/) per osservare i collegamenti di memoria e delega.
