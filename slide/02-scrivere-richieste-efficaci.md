# Modulo 2 — Scrivere richieste efficaci

---

## Slide 56 — Che cos’è un prompt

- Un prompt è una richiesta rivolta a un modello di AI. Può contenere istruzioni, dati e indicazioni su come presentare la risposta.
- Se lasci aperti lo scopo, il destinatario o il formato, il modello li interpreta a partire dal contesto disponibile.
- Esplicita le scelte che cambiano il risultato. Per un compito semplice può bastare una frase.

---

## Slide 57 — Che cosa rende efficace una richiesta

- Chiarisci quale lavoro vuoi delegare e che cosa farai con il risultato.
- Fornisci le informazioni necessarie per svolgere quel lavoro.
- Stabilisci come riconoscere una risposta utilizzabile. Una sintesi per decidere e una scheda per verificare richiedono informazioni diverse.

---

## Slide 58 — I sei elementi di una richiesta

- **Contesto e compito.** Chi userà la risposta, per quale scopo e quale operazione deve svolgere il modello.
- **Materiale e vincoli.** Quali dati usare e quali limiti rispettare.
- **Formato e controlli.** Come presentare il risultato e come renderlo verificabile.

---

## Slide 59 — Contesto e compito

- Il contesto spiega a chi serve la risposta e quale azione o decisione deve supportare.
- Scegli un verbo che definisca il lavoro. **Estrarre** significa riportare informazioni presenti nel materiale. **Confrontare** significa evidenziare differenze secondo un criterio.
- Se vuoi una raccomandazione, indica quali criteri devono guidarla.

---

## Slide 60 — Materiale e vincoli

- Distingui le istruzioni dal testo o dai dati da analizzare. Puoi usare intestazioni come **Compito**, **Dati** e **Risposta attesa**.
- Specifica quali fonti si possono usare e quale periodo o perimetro considerare.
- Indica i limiti che servono davvero, come la lingua, il pubblico o le informazioni da escludere.

---

## Slide 61 — Formato e controlli

- Una tabella permette di confrontare più voci. Un paragrafo breve può essere pronto per una comunicazione interna.
- Indica i campi indispensabili. Per confrontare importi possono servire valore, valuta e periodo.
- Specifica come segnalare un dato mancante e come riportare la fonte di un’affermazione importante.

---

## Slide 62 — I quattro elementi dello schema Microsoft

- **Obiettivo** e **contesto** spiegano che cosa vuoi ottenere e a cosa serve.
- **Fonti** e **aspettative** indicano su quali informazioni lavorare e come deve essere la risposta.
- Lo schema in sei elementi rende espliciti anche i controlli, utili quando bisogna verificare dati e calcoli.

---

## Slide 63 — Zero-shot e few-shot

- **Zero-shot.** Descrivi il compito senza fornire casi già svolti. È un buon punto di partenza quando le istruzioni sono chiare.
- **Few-shot.** Aggiungi qualche caso svolto per mostrare come devono apparire o essere classificati i risultati.
- Scegli casi coerenti con le regole. Se conta come gestire un’eccezione, mostra anche quella.

---

## Slide 64 — Chiarimenti e assunzioni

- Se manca una scelta che cambia il risultato, chiedi al modello di fare una domanda mirata prima di procedere.
- Se il lavoro può proseguire, chiedi di dichiarare le assunzioni. Potrai confermarle o correggerle.
- Se manca un dato indispensabile per un calcolo, deve essere chiaro quale dato serve.

---

## Slide 65 — Prima le evidenze, poi la risposta

- Quando il compito parte da un documento, chiedi di individuare i passaggi pertinenti prima di formulare la risposta.
- Distingui ciò che il testo dice esplicitamente da ciò che se ne può dedurre.
- Per le affermazioni importanti, chiedi un riferimento che permetta di tornare alla fonte. Se manca un riscontro, chiedi di indicarlo.

---

## Slide 66 — Come chiedere un calcolo verificabile

- Chiedi formula, valori utilizzati, periodo, unità di misura e risultato.
- Se il calcolo dipende da una convenzione, specificala. Per una differenza tra due importi, indica quale sottrarre dall’altro.
- Per i modelli di ragionamento, OpenAI consiglia istruzioni dirette. Una richiesta di formula e dati rende chiaro che cosa vuoi poter controllare.

---

## Slide 67 — Scomporre un compito complesso

- Dividi il lavoro in passaggi con risultati intermedi che puoi controllare.
- Prima estrai le informazioni. Poi confrontale con la fonte. Infine usa quelle verificate per scrivere la sintesi.
- Intervenire su un risultato intermedio permette di correggere un errore prima che passi al risultato finale.

---

## Slide 68 — Domanda, contesto, stessa domanda

- Per cercare un dato preciso in un testo lungo, puoi mettere la domanda all’inizio e ripeterla alla fine dello stesso messaggio.
- Negli esperimenti di *Lost in the Middle*, questa tecnica ha aiutato molto nella ricerca di un valore preciso e poco nelle domande su più documenti.
- Il beneficio dipende dal modello e dal compito. Confronta le due formulazioni sul materiale che usi davvero.

---

## Slide 69 — Dove fermarsi con il dettaglio

- Definisci chi leggerà la risposta e quale azione o decisione deve compiere.
- Per ogni dettaglio chiediti se ometterlo potrebbe cambiare la decisione, causare un errore o creare un fraintendimento.
- Applica lo stesso criterio a condizioni, eccezioni e incertezze. Fermati quando aggiungere altro non aiuta il lettore a decidere o ad agire meglio.

---

## Slide 70 — Fatti scrivere il prompt dal modello

- Nella prima chat, descrivi il lavoro, i dati disponibili, chi userà il risultato e come lo valuterai.
- Chiedi al modello di segnalare le ambiguità e di scrivere una richiesta completa da copiare.
- Questa tecnica si chiama **meta-prompting**. Usi una richiesta per farti costruire la richiesta che svolgerà il lavoro.

---

## Slide 71 — Prova il prompt in una seconda chat

- Apri una nuova conversazione. Incolla il prompt, completa i segnaposto e aggiungi il materiale del caso.
- Puoi usare lo stesso modello. Una nuova chat ti permette di vedere se la richiesta contiene anche le informazioni emerse mentre la preparavi.
- Se la piattaforma usa memoria o istruzioni personalizzate, possono influire anche sulla seconda chat.

---

## Slide 72 — Migliora il prompt in base al risultato

- Riporta nella chat di progettazione il prompt, la risposta ottenuta e il difetto osservato.
- Chiedi una modifica mirata. Se il modello inventa un dato mancante, specifica come deve segnalarlo.
- Ripeti la prova sullo stesso caso, poi su un caso diverso. Il risultato di ogni prova guida la modifica successiva.

---

## Slide 73 — Come capire se il prompt è migliorato

- Prima della prova, stabilisci cosa deve fare la risposta per essere utilizzabile.
- Per una richiesta ricorrente, verifica un caso ordinario, uno con un dato mancante e uno con dati in conflitto.
- Dopo una modifica, riprova i casi precedenti. Controlla che la correzione funzioni ogni volta che serve e che le risposte già corrette restino utilizzabili.

---

## Slide 74 — Istruzioni ricorrenti e modelli di prompt

- Le istruzioni personalizzate contengono preferenze valide per più richieste, come lingua e stile.
- Un modello di prompt conserva le istruzioni di un’attività ricorrente e lascia spazi da compilare per i dati che cambiano.
- Quando riusi il prompt, sostituisci periodo, destinatario e materiale con quelli del caso corrente.

---

## Slide 75 — Esploriamo il tutorial di Anthropic

- Apriamo insieme il [tutorial interattivo di prompt engineering](https://github.com/anthropics/prompt-eng-interactive-tutorial/tree/master).
- Esploriamo i capitoli su come separare dati e istruzioni, specificare il formato e usare esempi nel prompt.
- Scegliamo un esercizio del tutorial e discutiamo che cosa cambia quando modifichiamo le istruzioni.

---

## Slide 76 — Esercitazione finale: Enel e Sorgenia

- Scarica i due estratti dal [repository del corso](https://github.com/mi-alto/ikn/tree/main/modulo-2).
- **Obiettivo comune.** Confronta gli estratti dei bilanci consolidati di Enel e Sorgenia. Dal 2024 al 2025, in quale gruppo sono cresciuti i ricavi? Dove è migliorato il margine operativo? I due indicatori si muovono nella stessa direzione?
- **Cambia il prompt.** Usa lo stesso modello e gli stessi due estratti. Parti da una domanda aperta, poi aggiungi metriche, formato e richiesta delle fonti. Usa una chat nuova per ogni prova.
- **Cambia il modello.** Ripeti il prompt più efficace su un altro modello, usando gli stessi estratti.
- **Confronta le risposte.** Verifica almeno un dato per gruppo. Controlla la variazione dei ricavi in percentuale, la variazione del margine operativo in punti percentuali e se la risposta segnala cambi di perimetro o differenze nelle definizioni.
