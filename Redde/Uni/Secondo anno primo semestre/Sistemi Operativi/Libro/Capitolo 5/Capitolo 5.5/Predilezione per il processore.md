Si consideri che cosa accade alla memoria cache dopo che un processo è stato eseguito da uno specifico processore: i dati che il processore ha trattato più recentemente permangono nella cache e, di conseguenza, i successivi accessi alla memoria da parte del processo tendono a utilizzare spesso la memoria cache (chiamata warm cache). 

Si consideri ora che cosa succede se un processo si sposta su un altro processore: i contenuti della memoria cache devono essere invalidati sul processore di partenza, mentre la cache del processore di arrivo deve essere nuovamente riempita. 
A causa degli alti costi di svuotamento e riempimento della cache, molti sistemi smp tentano di impedire il passaggio di thread da un processore all’altro, mirando a mantenere un thread sempre sullo stesso processore e a sfruttare i vantaggi della warm cache. 
Si parla di predilezione per il processore (_processor affinity_), intendendo con ciò che un processo ha una predilezione per il processore su cui è in esecuzione.

Le due strategie per l’organizzazione della coda dei thread disponibili per lo scheduling descritte nel [Paragrafo 5.5.1](obsidian://open?vault=Redde&file=Uni%2FSecondo%20anno%20primo%20semestre%2FSistemi%20Operativi%2FLibro%2FCapitolo%205%2FCapitolo%205.5%2FApprocci%20allo%20scheduling%20per%20multiprocessori) hanno implicazioni sulla predilezione per il processore.

Infatti, se adottiamo l’approccio di una ready queue comune, un thread può essere selezionato per l’esecuzione da qualsiasi processore e ogni volta che un thread è schedulato su un nuovo processore la cache del processore deve essere ripopolata. 
Con le ready queue private, distinte per ogni processore, un thread viene sempre schedulato sullo stesso processore e può quindi trarre vantaggio dal contenuto di una warm cache. In sostanza, le ready queue private forniscono la predilezione del processore gratuitamente!

------------------
La predilezione per il processore può assumere varie forme. 
Quando un sistema operativo si propone di mantenere un processo su un singolo processore, ma non garantisce che sarà così, si parla di **predilezione debole (_soft affinity_)**. In questo caso il sistema operativo tenta di mantenere il processo su un singolo processore, ma è possibile che un processo migri da un processore all’altro.
Alcuni sistemi dispongono di chiamate di sistema per realizzare la **predilezione forte (_hard affinity_),** permettendo così a un processo di specificare un sottoinsieme di processori su cui può essere eseguito. 

Molti sistemi supportano sia la predilezione debole sia la predilezione forte. 
Linux, per esempio, implementa la predilezione debole, ma fornisce anche la chiamata **sched_setaffinity()** per il supporto della predilezione forte, consentendo così a un thread di specificare l’insieme di cpu su cui può essere eseguito.

Anche l’architettura della memoria principale di un sistema può influenzare le questioni relative alla predilezione.
![[Pasted image 20221107165358.png]]
La figura sopra riportata mostra un’architettura con accesso non uniforme alla memoria (numa) in cui sono presenti due chip fisici di processore, ciascuno con la propria cpu e memoria locale. Sebbene un’interconnessione di sistema consenta a tutte le cpu in un sistema numa di condividere uno spazio di indirizzamento fisico, una cpu ha un accesso più rapido alla propria memoria locale rispetto alla memoria locale di un’altra cpu.

Se lo scheduler della cpu del sistema operativo e gli algoritmi di gestione della memoria sono _consci del_ _numa_ e lavorano insieme, a un thread che è stato schedulato su una particolare cpu può essere allocata la memoria più vicina a dove risiede la cpu, fornendo così al thread un accesso alla memoria più veloce possibile.

È interessante notare che il bilanciamento del carico spesso contrasta i vantaggi della predilezione per il processore. 
Il vantaggio di mantenere un thread in esecuzione sullo stesso processore, infatti, è che il thread può sfruttare i suoi dati nella memoria cache di quel processore. 
Il bilanciamento del carico, spostando un thread da un processore a un altro, rimuove questo vantaggio. 
Allo stesso modo, la migrazione di un thread tra processori può comportare svantaggi su sistemi numa, in cui un thread può essere spostato su un processore che richiede tempi di accesso alla memoria più lunghi. 

In altre parole, esiste un conflitto naturale tra il bilanciamento del carico e la riduzione dei tempi di accesso alla memoria. Per questa ragione gli algoritmi di scheduling per i moderni sistemi numa multicore sono diventati piuttosto complessi.