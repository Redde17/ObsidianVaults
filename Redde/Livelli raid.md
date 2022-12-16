La tecnica di mirroring offre un’alta affidabilità ma è costosa; 
la tecnica di striping (sezionamento) offre un’alta capacità di trasferimento dei dati, ma non migliora l’affidabilità.

Sono stati proposti numerosi schemi per fornire ridondanza a basso costo usando l’idea dello striping combinata con i bit di parità (che vedremo a breve). 
Questi schemi realizzano diversi compromessi tra costi e prestazioni e sono stati classificati in livelli chiamati livelli raid.
(nella figura, la lettera _P_ indica i bit di correzione degli errori, la lettera _C_ indica una seconda copia dei dati).
![[Pasted image 20221216184514.png]]
In tutti i casi riportati nella figura, sono presenti quattro dischi di dati, mentre i dischi supplementari s’impiegano per memorizzare le informazioni ridondanti per il ripristino dai guasti.

-   raid di livello 0. Il livello 0 si riferisce ad array di dischi con striping a livello di blocchi, ma senza ridondanza (come il mirroring o i bit di parità).

-   raid di livello 1. Il livello 1 si riferisce alla tecnica di mirroring. La Figura 11.15(b) mostra un’organizzazione basata sul mirroring.

-   raid di livello 4. Il livello 4 è anche noto come organizzazione con codici per la correzione degli errori di memoria (ecc). Tale organizzazione è anche usata nei raid di livello 5 e 6.

La stessa idea alla base degli ecc (_error-correcting codes_) si può usare immediatamente negli array di memorizzazione eseguendo lo striping dei byte presenti nelle unità di memorizzazione. 
Per esempio, il primo bit di ogni byte si potrebbe memorizzare nell’unità 1, il secondo bit nell’unità 2, e così via fino alla memorizzazione dell’ottavo bit nell’unità 8 e alla memorizzazione dei bit di correzione degli errori in ulteriori unità. Questo schema è rappresentato graficamente nella Figura 11.15(c), dove i dispositivi etichettati con la lettera _P_ contengono i bit di correzione. Se una delle unità si guasta, il ricalcolo del codice di correzione degli errori lo rileva e impedisce il passaggio dei dati al processo richiedente, generando un errore.

Il livello 4 può effettivamente correggere gli errori, anche se c’è soltanto un blocco ecc, considerando che, a differenza dei sistemi di memoria centrale, i controllori dei dischi possono rilevare se un settore è stato letto correttamente, così che un unico bit di parità si può usare sia per individuare gli errori sia per correggerli. 
L’idea è la seguente: se uno dei settori è danneggiato, si conosce esattamente di quale settore si tratta e, per ogni bit nel settore, è possibile determinare se debba avere valore 1 o 0 calcolando la parità dei bit corrispondenti dai settori negli altri dischi. Se la parità dei rimanenti bit è uguale a quella memorizzata, il bit mancante è 0, altrimenti è 1.

La lettura di un blocco richiede l’accesso a un solo dispositivo, permettendo la gestione di altre richieste da parte di altri dischi. Quindi, la capacità di trasferimento dei dati per ciascun accesso è minore, ma gli accessi in lettura possono procedere in modo parallelo ottenendo una velocità complessiva di i/o più alta. La capacità di trasferimento per la lettura di molti dati è alta, poiché si possono leggere in modo parallelo tutti i dischi e anche le operazioni di scrittura di grandi quantità di dati presentano un’alta capacità di trasferimento, poiché i dati e i bit di parità si possono scrivere in parallelo.

Il raid di livello 4 presenta due vantaggi rispetto al livello 1, fornendo allo stesso tempo un’uguale protezione dei dati. Il primo vantaggio è che si usa un solo disco per la parità dei dati memorizzati in diversi dischi di dati, anziché un disco di mirroring per ciascun disco di dati come nel livello 1. Il secondo vantaggio è che, essendo le letture e le scritture dei byte distribuite su più dischi con uno striping a _n_ vie, la velocità di trasferimento di un singolo blocco è pari a _n_ volte quella dei raid di livello 1.