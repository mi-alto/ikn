# Corso AI e finanza: scaletta oraria

Giornata dalle 9:30 alle 17:30. Ogni modulo: 45 minuti di discussione aperta e 15 minuti di esercitazione.

## Orario

| Orario | Modulo | Discussione | Esercitazione |
|---|---|---|---|
| 9:30 - 9:45 | Introduzione al corso e presentazione delle persone | | |
| 9:45 - 10:45 | 1. Fondamenti e primi passi | 45 min | 15 min |
| 10:45 - 11:45 | 2. Scrivere richieste efficaci | 45 min | 15 min |
| 11:45 - 12:00 | Pausa | | |
| 12:00 - 13:00 | 3. Costruire il proprio assistente | 45 min | 15 min |
| 13:00 - 14:15 | Pranzo | | |
| 14:15 - 15:15 | 4. Leggere documenti e dati | 45 min | 15 min |
| 15:15 - 16:15 | 5. Automazione, prima parte | 45 min | 15 min |
| 16:15 - 16:30 | Pausa | | |
| 16:30 - 17:20 | 6. Automazione, seconda parte | 35 min | 15 min |
| 17:20 - 17:30 | Chiusura e prossimi passi | | |

Totale: 260 minuti di discussione, 90 minuti di esercitazione, 10 minuti di chiusura.

## Contenuto dei moduli

### 1. Fondamenti e primi passi

- Cos'è un modello di linguaggio
- Gli strumenti sul mercato e come scegliere
- Sicurezza dei dati: cosa si può caricare e cosa no
- La mappa "analisi del documento" e "analisi dei numeri" per le due aree (Accounting & Balance, Origination & Analysis)

### 2. Scrivere richieste efficaci

- Come si formula una richiesta
- Come ottenere risposte ordinate e riutilizzabili
- Modelli pronti per le attività ricorrenti

### 3. Costruire il proprio assistente

- Come lavora un agente: l'obiettivo (goal) e il ciclo di lavoro (loop)
- Istruzioni fisse e documenti di riferimento
- Le skill: procedure salvate che l'assistente richiama quando servono
- I plugin e i collegamenti agli altri programmi (MCP)
- In aula si aprono le skill vere di Anthropic per la finanza (vedi il [repository Financial Services](https://github.com/anthropics/financial-services)), per mostrare che sono testo leggibile
- Messaggio chiave: ognuno può scrivere la propria skill, così spiega un processo una volta sola e lo fa ripetere sempre uguale
- Esercitazione: ognuno configura un assistente con una skill

### 4. Leggere documenti e dati

- Documenti: estrazione in locale con modelli dedicati oppure affidata al modello di linguaggio
- Numeri: il modello scrive codice (Python) e lo esegue in un ambiente protetto (sandbox); quando serve e come si verifica il risultato

- Esercitazione: creare una dashboard HTML dai dati verificati di Enel e Sorgenia

### 5. Automazione, prima parte

- Cos'è un flusso automatico e come si costruisce
- Esercitazione: caricare un Excel in n8n, applicare una soglia e scaricare il report degli scostamenti

### 6. Automazione, seconda parte

- Applicazione ai processi della finanza: chiusure, riconciliazioni, previsioni, avvisi sugli scostamenti
- Qualità, sicurezza e tracciabilità dei dati
- Esercitazione: riconciliare fatture e ordini a partire da due CSV
