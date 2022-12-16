La tecnica di mirroring offre un’alta affidabilità ma è costosa; 
la tecnica di striping (sezionamento) offre un’alta capacità di trasferimento dei dati, ma non migliora l’affidabilità.

Sono stati proposti numerosi schemi per fornire ridondanza a basso costo usando l’idea dello striping combinata con i bit di parità (che vedremo a breve). 
Questi schemi realizzano diversi compromessi tra costi e prestazioni e sono stati classificati in livelli chiamati livelli raid.
(nella figura, la lettera _P_ indica i bit di correzione degli errori, la lettera _C_ indica una seconda copia dei dati).
![[Pasted image 20221216184514.png]]
In tutti i casi riportati nella figura, sono presenti quattro dischi di dati, mentre i dischi supplementari s’impiegano per memorizzare le informazioni ridondanti per il ripristino dai guasti.

-   raid di livello 0. 
	Il livello 0 si riferisce ad array di dischi con striping a livello di blocchi, ma senza ridondanza (come il mirroring o i bit di parità).

-   raid di livello 1. 
	Il livello 1 si riferisce alla tecnica di mirroring. La Figura 11.15(b) mostra un’organizzazione basata sul mirroring.

-   raid di livello 4. 
	Il livello 4 è anche noto come organizzazione con codici per la correzione degli errori di memoria (ecc). Tale organizzazione è anche usata nei raid di livello 5 e 6.

La stessa idea alla base degli ecc (_error-correcting codes_) si può usare immediatamente negli array di memorizzazione eseguendo lo striping dei byte presenti nelle unità di memorizzazione. 
Per esempio, il primo bit di ogni byte si potrebbe memorizzare nell’unità 1, il secondo bit nell’unità 2, e così via fino alla memorizzazione dell’ottavo bit nell’unità 8 e alla memorizzazione dei bit di correzione degli errori in ulteriori unità. Questo schema è rappresentato graficamente nella Figura 11.15(c), dove i dispositivi etichettati con la lettera _P_ contengono i bit di correzione. Se una delle unità si guasta, il ricalcolo del codice di correzione degli errori lo rileva e impedisce il passaggio dei dati al processo richiedente, generando un errore.

Il livello 4 può effettivamente correggere gli errori, anche se c’è soltanto un blocco ecc, considerando che, a differenza dei sistemi di memoria centrale, i controllori dei dischi possono rilevare se un settore è stato letto correttamente, così che un unico bit di parità si può usare sia per individuare gli errori sia per correggerli. 
L’idea è la seguente: se uno dei settori è danneggiato, si conosce esattamente di quale settore si tratta e, per ogni bit nel settore, è possibile determinare se debba avere valore 1 o 0 calcolando la parità dei bit corrispondenti dai settori negli altri dischi. 
Se la parità dei rimanenti bit è uguale a quella memorizzata, il bit mancante è 0, altrimenti è 1.

La lettura di un blocco richiede l’accesso a un solo dispositivo, permettendo la gestione di altre richieste da parte di altri dischi. 
Quindi, la capacità di trasferimento dei dati per ciascun accesso è minore, ma gli accessi in lettura possono procedere in modo parallelo ottenendo una velocità complessiva di i/o più alta. La capacità di trasferimento per la lettura di molti dati è alta, poiché si possono leggere in modo parallelo tutti i dischi e anche le operazioni di scrittura di grandi quantità di dati presentano un’alta capacità di trasferimento, poiché i dati e i bit di parità si possono scrivere in parallelo.

Il raid di livello 4 presenta due vantaggi rispetto al livello 1, fornendo allo stesso tempo un’uguale protezione dei dati. 
Il primo vantaggio è che si usa un solo disco per la parità dei dati memorizzati in diversi dischi di dati, anziché un disco di mirroring per ciascun disco di dati come nel livello 1. 
Il secondo vantaggio è che, essendo le letture e le scritture dei byte distribuite su più dischi con uno striping a _n_ vie, la velocità di trasferimento di un singolo blocco è pari a _n_ volte quella dei raid di livello 1.

Un altro problema di prestazioni riguardante il raid di livello 4 (come per tutti i livelli raid basati sui bit di parità) è il tempo richiesto dal calcolo e dalla scrittura della parità. 
Questo tempo aggiuntivo determina operazioni di scrittura significativamente più lente rispetto ad array raid senza parità. 
Tuttavia, le moderne cpu general-purpose sono molto veloci rispetto all’i/o sui dispositivi e l’impatto in termini di prestazioni può essere minimo. 
Inoltre, molti array raid dispongono di un controllore capace di gestire il calcolo della parità. Questo sposta il carico dovuto al calcolo della parità dalla cpu all’array di dischi. L’array ha anche una cache nvram per memorizzare i blocchi mentre viene calcolata la parità e per memorizzare transitoriamente le scritture dal controllore alle unità. 
Questa tecnica può evitare la maggior parte dei cicli di lettura-modifica-scrittura raccogliendo i dati da scrivere in una sezione e scrivendo contemporaneamente su tutte le unità della sezione. Questa combinazione di accelerazione hardware e buffering può rendere la tecnica raid con parità altrettanto veloce di quella senza parità; infatti, un array raid con cache e bit di parità può avere prestazioni migliori di un’organizzazione raid senza cache e senza parità.

-   raid di livello 5. 
	Il livello 5, o organizzazione con blocchi intercalati a parità distribuita, differisce dal livello 4 per il fatto che, invece di memorizzare i dati in _n_ unità e la parità in un disco separato, i dati e le informazioni di parità sono distribuite tra le _n_ + 1 unità. 
	Per ogni blocco, una delle unità memorizza la parità e le altre i dati. 
	Per esempio, considerando una batteria di cinque unità, la parità per il blocco _m_-esimo si memorizza nell’unità (_m_ mod 5) + 1, mentre i blocchi _m_-esimi delle altre quattro unità contengono i dati effettivi per quel blocco. 
	Questo schema è illustrato nella Figura 11.15(d), dove i simboli _P_ sono distribuiti su tutte le unità. 
	Un blocco di parità non può contenere informazioni di parità per blocchi che risiedono nella stessa unità, poiché un guasto all’unità provocherebbe sia la perdita di dati sia la perdita dell’informazione di parità e quindi i dati non sarebbero ripristinabili. Con la distribuzione della parità sui diverse unità, il raid di livello 5 evita un uso intensivo dell’ unità dove risiede la parità, che invece si ha con il raid di livello 4.
	 raid 5 è il più comune sistema di parità raid.
-  raid di livello 6. 
	Il livello 6, detto anche schema di ridondanza P + Q, è molto simile al raid di livello 5, ma memorizza ulteriori informazioni ridondanti per poter gestire guasti contemporanei di più dischi. 
	La parità xor non può essere utilizzata su entrambi i blocchi di parità perché sarebbero identici e non potrebbero fornire informazioni di ripristino. 
	Invece della parità, per calcolare Q vengono utilizzati codici di correzione degli errori basati sulla matematica dei campi di Galois. 
	Nello schema mostrato nella Figura 11.15 (e) sono memorizzati 2 blocchi di dati ridondanti per ogni 4 blocchi di dati (a differenza di 1 blocco di parità usato nel livello 5) e il sistema risultante può tollerare due guasti delle unità.