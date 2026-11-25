# Modulo 3 — Dall’assistente all’agente in LibreChat

## Slide 77 — Dall’assistente all’agente

- Una chat può rispondere con testo. Un agente dispone anche di strumenti che gli permettono di leggere un file, cercare informazioni o eseguire codice.
- In LibreChat, un agente è una configurazione salvata che combina un modello, istruzioni e le capacità disponibili nell’istanza.

---

## Slide 78 — Goal e criterio di completamento

- Il goal descrive il risultato da ottenere. Il criterio di completamento dice come riconoscere che il risultato è pronto.
- Indicare il risultato e la verifica attesa permette all’agente di scegliere i passaggi da compiere entro i permessi disponibili.

---

## Slide 79 — Il loop dell’agente

- Il modello decide il prossimo passo. Se serve uno strumento, l’applicazione lo invoca e restituisce l’esito al modello.
- L’esito entra nel contesto e orienta il passo successivo. Il ciclo può terminare con un risultato, una richiesta di intervento o un limite raggiunto.

---

## Slide 80 — Le istruzioni dell’agente

- Le istruzioni salvate nell’Agent Builder definiscono il comportamento dell’agente nelle conversazioni che lo usano.
- Il messaggio dell’utente definisce l’obiettivo della singola sessione. Le regole generali dell’applicazione restano applicabili.

---

## Slide 81 — Documenti e ambiente di lavoro

- In LibreChat il punto di partenza sono gli allegati e le fonti che l’istanza rende disponibili all’agente.
- File Search e Run Code hanno scopi diversi. Il primo recupera passaggi di documenti, il secondo può usare file come input di un programma.

---

## Slide 82 — Memoria della conversazione e memoria persistente

- Lo storico della chat fornisce contesto ai messaggi successivi. La memoria persistente, quando abilitata, può conservare informazioni da usare in altre chat.
- Le istruzioni dell’agente sono una configurazione salvata. La memoria è un meccanismo distinto per recuperare informazioni conservate.

---

## Slide 83 — La memoria su file negli ambienti agentici

- In un agente che lavora su una cartella, un file Markdown può conservare decisioni o lo stato del lavoro. L’agente deve poterlo trovare e leggerlo nella sessione successiva.
- In LibreChat, per riusare un file di appunti occorre renderlo disponibile tramite allegato o fonte configurata.

---

## Slide 84 — Che cos’è una skill

- Una skill raccoglie istruzioni e materiali per una capacità riutilizzabile. Il file SKILL.md descrive la capacità e quando usarla.
- LibreChat documenta la creazione o l’importazione dalla sezione Skills e la selezione delle skill nell’Agent Builder. La disponibilità dipende dalla versione e dai permessi.

---

## Slide 85 — Le skill finanziarie di Anthropic

- Il [repository Financial Services](https://github.com/anthropics/financial-services) contiene skill e altri componenti per il lavoro finanziario. Earnings analysis è dedicata alla lettura dei risultati societari.
- Il file di una skill si può leggere prima di usarlo. Mostra quali fonti, passaggi e risultati la skill dà per scontati.

---

## Slide 86 — Adattare una skill al mercato europeo

- Una skill che presuppone fonti o documenti statunitensi può richiedere modifiche per altri mercati.
- Prima di riusarla, controlla le fonti disponibili, il perimetro del bilancio e i principi contabili dell’emittente. Rendi esplicite le sostituzioni nelle istruzioni.

---

## Slide 87 — Plugin e importazione di una skill

- Un plugin può raggruppare skill, comandi e connettori pensati per una piattaforma.
- L’eventuale importazione in LibreChat riguarda il file o l’archivio della singola skill. Connettori e strumenti richiesti dalla skill devono essere disponibili separatamente.

---

## Slide 88 — MCP e gli strumenti esterni

- MCP è un protocollo che permette a LibreChat di collegarsi a un server che espone strumenti.
- La skill descrive come svolgere un lavoro. Uno strumento MCP rende eseguibile una specifica operazione, come interrogare un servizio di ricerca.

---

## Slide 89 — Brave Search come strumento MCP

- Un server Brave Search può esporre la ricerca web all’agente. La chiave API autentica il server presso Brave.
- LibreChat deve avere accesso a un server compatibile raggiungibile dalla sua istanza. La registrazione da interfaccia e le credenziali per utente dipendono dal ruolo e dalla configurazione.

---

## Slide 90 — Run Code e la sandbox

- Run Code permette all’agente di eseguire programmi in un ambiente isolato se il servizio Code Interpreter è configurato.
- Se disponibile, l’agente può passare allegati al programma e restituire file prodotti. Le librerie installate e i permessi della sandbox determinano quali operazioni sono fattibili.

---

## Slide 91 — Esercitazione finale — Configura l’agente in LibreChat

- Apri l’Agent Builder. Se la sezione Skills è disponibile, importa uno SKILL.md finanziario di Anthropic e associalo all’agente dopo aver letto i requisiti.
- Se l’istanza offre il server Brave Search, selezionalo nella libreria degli strumenti. Usa MCP Settings per aggiungere un server remoto solo se hai il permesso e il docente fornisce URL e configurazione.

---

## Slide 92 — Esercitazione finale — Scrivi ed esegui il programma

- Se Run Code è disponibile, allega l’[estratto Enel](https://github.com/mi-alto/ikn/tree/main/modulo-2) alla sessione dell’agente.
- Chiedi: «Scrivi ed esegui un programma Python che divida il PDF dopo la terza pagina. Restituisci i due PDF e verifica che ciascuno abbia tre pagine».
- Se Run Code è assente o manca la libreria, chiedi il programma e identifica il requisito mancante. La prova di esecuzione richiede una sandbox già configurata.

---

## Slide 93 — Esercitazione finale — Verifica il risultato

- Se il programma è stato eseguito, scarica i due PDF e controlla il conteggio e il punto di taglio. Il risultato atteso è 3 + 3 pagine nello stesso ordine dell’originale.
- Ripercorri ciò che è successo: goal assegnato, strumento invocato, risultato osservato e verifica finale.
