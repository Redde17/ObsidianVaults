Sui sistemi smp è importante che il carico di lavoro sia distribuito equamente tra tutte le unità elaborative per sfruttare appieno i vantaggi di avere più processori. 
Se ciò non avvenisse, alcuni processori potrebbero restare inattivi mentre altri verrebbero intensamente sfruttati con una coda di processi in attesa. 

Il bilanciamento del carico tenta di ripartire il carico di lavoro uniformemente tra tutti i processori di un sistema smp. Bisogna notare che il bilanciamento è necessario, di norma, solo nei sistemi in cui ciascun processore ha una coda privata di processi eseguibili. 

Nei sistemi che mantengono una coda comune, il bilanciamento del carico è sovente superfluo: un processore inattivo passerà immediatamente all’esecuzione di un processo dalla coda comune dei processi eseguibili.

-----------------
Il bilanciamento del carico può seguire due approcci: **la migrazione push e la migrazione pull.**
**La migrazione push** prevede che un processo apposito controlli periodicamente il carico di ogni processore: se identifica uno sbilanciamento, riporta il carico in equilibrio, spostando i processi dal processore saturo ad altri più liberi, o inattivi.
**La migrazione pull**, invece, si ha quando un processore inattivo prende un processo in attesa a un processore sovraccarico. I due tipi di migrazione non sono mutuamente esclusivi, e trovano spesso applicazione contemporanea nei sistemi con bilanciamento del carico.

Il concetto di “carico bilanciato” può avere significati diversi. Una prima possibilità è richiedere semplicemente che tutte le code contengano approssimativamente lo stesso numero di thread. In alternativa, il bilanciamento potrebbe richiedere un’equa distribuzione delle priorità dei thread su tutte le code. Inoltre, in determinate situazioni, potrebbe non essere sufficiente alcuna di queste strategie, poiché esse possono essere in contrasto con gli obiettivi dell’algoritmo di scheduling.