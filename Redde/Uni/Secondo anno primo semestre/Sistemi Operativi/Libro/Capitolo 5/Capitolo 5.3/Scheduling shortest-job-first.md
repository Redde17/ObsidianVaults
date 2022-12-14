Un criterio diverso di scheduling della cpu è l’algoritmo di **scheduling per brevità (_shortest-job-first_, sjf)**.

Questo algoritmo associa a ogni processo la lunghezza della successiva sequenza di operazioni della cpu. Quando è disponibile, si assegna la cpu al processo che ha la più breve lunghezza della successiva sequenza di operazioni della cpu. 

Se due processi hanno le successive sequenze di operazioni della cpu della stessa lunghezza si applica lo scheduling fcfs. 

Si noti che sarebbe più appropriato il termine _shortest next_ _cpu_ _burst_, infatti lo scheduling si esegue esaminando la lunghezza della successiva sequenza di operazioni della cpu del processo e non la sua lunghezza totale. 

Tuttavia, poiché è comunemente usato ed è presente nella maggior parte dei libri di testo, anche qui si fa uso del termine sjf.

Come esempio si consideri il seguente insieme di processi, con la durata della sequenza di operazioni della cpu espressa in millisecondi:
![[Pasted image 20221105163243.png]]
Con lo scheduling sjf questi processi si ordinerebbero secondo il seguente diagramma di Gantt.
![[Pasted image 20221105163254.png]]
Il tempo d’attesa è di 3 millisecondi per il processo P1, di 16 millisecondi per il processo P2, di 9 millisecondi per il processo P3 e di 0 millisecondi per il processo P4. Quindi, **il tempo d’attesa medio è di (3 + 16 + 9 + 0)/4 = 7 millisecondi**. 
Usando lo scheduling fcfs, il tempo d’attesa medio sarebbe di 10,25 millisecondi.

Si può dimostrare che l’algoritmo di scheduling sjf è _ottimale_, nel senso che rende minimo il tempo d’attesa medio per un dato insieme di processi. Spostando un processo breve prima di un processo lungo, il tempo d’attesa per il processo breve diminuisce più di quanto aumenti il tempo d’attesa per il processo lungo. Di conseguenza, il tempo d’attesa **_medio_** diminuisce.

L’algoritmo sjf può essere sia _con prelazione_ sia _senza prelazione_. 
La scelta si presenta quando alla ready queue arriva un nuovo processo mentre un altro processo è ancora in esecuzione. Il nuovo processo può richiedere una sequenza di operazioni della cpu più breve di quella che resta al processo correntemente in esecuzione. Un algoritmo sjf con prelazione sostituisce il processo attualmente in esecuzione, mentre un algoritmo sjf senza prelazione permette al processo correntemente in esecuzione di portare a termine la propria sequenza di operazioni della cpu. (Lo scheduling sjf con prelazione è talvolta chiamato scheduling _shortest-remaining-time-first_).

Come esempio, si considerino i quattro processi seguenti, dove la durata delle sequenze di operazioni della cpu è data in millisecondi:
![[Pasted image 20221105163659.png]]
Se i processi arrivano alla ready queue nei momenti indicati e richiedono i tempi di cpu illustrati, dallo scheduling sjf con prelazione risulta la sequenza indicata dal seguente diagramma di Gantt.
![[Pasted image 20221105163719.png]]
All’istante 0 si avvia il processo _P1, poiché è l’unico che si trova nella coda. 
All’istante 1 arriva il processo _P2. Il tempo necessario per completare il processo _P1 (7 millisecondi) è maggiore del tempo richiesto dal processo _P2 (4 millisecondi), perciò si effettua la prelazione del processo _P_1 sostituendolo col processo _P2.
Il tempo d’attesa medio per questo esempio è **\[(10 – 1) + (1 – 1) + (17 – 2) + (5 – 3)]/4 = 26/4 = 6,5 millisecondi**. 
Con uno scheduling sjf senza prelazione si otterrebbe un tempo d’attesa medio di 7,75 millisecondi.