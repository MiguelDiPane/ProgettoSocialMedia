# Ecosistemi di Supporto nel Fediverso: Analisi Macro-Strutturale delle Comunità di Salute Mentale

## Obiettivo del Progetto
Questo progetto analizza la struttura e le dinamiche di interazione tra i server (istanze) della piattaforma decentralizzata Mastodon, concentrandosi sulle discussioni relative alla salute mentale. Lo scopo è comprendere come l'informazione e il supporto emotivo si diffondano all'interno del Fediverso.

## Fasi dell'Analisi

**1. Data Mining ed Estrazione Dati**
Estrazione dei messaggi tramite le API di Mastodon utilizzando hashtag legati a emozioni, diagnosi specifiche e neurodiversità (es. `#Depression`, `#ADHD`, `#Neurodivergent`). L'estrazione filtra e conserva esclusivamente le risposte (*replies*) tra istanze diverse, permettendo di costruire una mappatura delle interazioni reali ed escludendo i *self-loop*.

**2. Sentiment Analysis**
Elaborazione del linguaggio naturale (NLP) per determinare la polarità emotiva dei contenuti. Ogni interazione viene valutata assegnando un punteggio per definire se il legame semantico tra i server è positivo ($+1$), neutro ($0$) o negativo ($-1$).

**3. Costruzione della Rete (Graph Analysis)**
Costruzione di un grafo diretto e pesato delle interazioni. I nodi rappresentano le istanze Mastodon, mentre gli archi indicano i messaggi scambiati, pesati per volume e polarità. Per l'analisi strutturale, il grafo viene filtrato preservando i collegamenti statisticamente più forti (top 5%), riducendo il rumore di fondo.

**4. Analisi dell'Omofilia Semantica**
Studio dell'omofilia, ovvero la tendenza dei server con argomenti affini ad aggregarsi. Sfruttando modelli avanzati di *Sentence Embeddings* (`all-MiniLM-L6-v2`), il testo di ciascun nodo viene convertito in vettori ad alta dimensionalità. La *similarità coseno* calcolata tra i vettori permette di correlare l'affinità tematica con l'effettiva frequenza dei collegamenti.

**5. Community Detection e Metriche di Centralità**
Individuazione dei macro-cluster e della struttura comunitaria del network avvalendosi dell'algoritmo di partizionamento di Louvain (valutato tramite l'indice di modularità $Q$). 
Vengono inoltre estratte metriche di centralità fondamentali per inquadrare il ruolo di ciascuna istanza:
* **Degree Centrality:** Quantifica il volume totale di interazioni di un nodo.
* **Betweenness Centrality:** Identifica le istanze "ponte" cruciali per il flusso di supporto tra comunità isolate.
* **Closeness Centrality:** Misura quanto un nodo sia vicino al resto della rete per una rapida propagazione.
* **Eigenvector Centrality:** Pesa l'influenza di un'istanza in base all'importanza dei suoi vicini.

**6. Dinamiche di Propagazione**
Modellazione della diffusione delle informazioni. Viene studiata l'influenza e la probabilità di "attivazione" di nodi adiacenti, classificando l'impatto di certe istanze che fungono da barriere o da acceleratori per la propagazione del testo nel grafo.

## Strumenti e Tecnologie
* **Raccolta Dati:** `mastodon.py`, `BeautifulSoup`
* **Data Science e Analisi Dati:** `pandas`, `numpy`
* **Machine Learning e NLP:** `sentence-transformers`, `textblob`
* **Scienza delle Reti:** `networkx`, `community_louvain`
* **Visualizzazione:** `matplotlib`, `seaborn`, `pyvis`
