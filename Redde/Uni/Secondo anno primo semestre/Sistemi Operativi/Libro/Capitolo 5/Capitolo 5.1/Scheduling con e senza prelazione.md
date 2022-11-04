Le decisioni riguardanti lo scheduling della cpu vengono prese nelle seguenti quattro circostanze:
1.  un processo passa dallo stato di esecuzione allo stato di attesa (per esempio, richiesta di i/o o invocazione di wait() per la terminazione di uno dei processi figli);
2.  un processo passa dallo stato di esecuzione allo stato pronto (per esempio, quando si verifica un segnale d’interruzione);
3.  un processo passa dallo stato di attesa allo stato pronto (per esempio, al completamento di un’operazione di i/o);
4.  un processo termina.

I casi 1 e 4 non danno alternative in termini di scheduling: si deve comunque scegliere un nuovo processo da eseguire, sempre che ce ne sia almeno uno nella ready queue per l’esecuzione. Una scelta si può invece fare nei casi 2 e 3.

**Quando lo scheduling interviene solo nelle condizioni 1 e 4, si dice che lo schema di scheduling è senza prelazione (_nonpreemptive_) o cooperativo (_cooperative_); altrimenti, lo schema di scheduling è con prelazione (_preemptive_).**

Nel caso dello scheduling senza prelazione, quando si assegna la cpu a un processo, questo rimane in possesso della cpu fino al momento del suo rilascio, dovuto al termine dell’esecuzione o al passaggio nello stato di attesa. Praticamente tutti i moderni sistemi operativi, inclusi Windows, macos, Linux e unix, utilizzano algoritmi di scheduling con prelazione.

Sfortunatamente lo scheduling con prelazione può portare a _race condition_ quando i dati sono condivisi tra diversi processi. Si consideri il caso in cui due processi condividono dati; mentre uno di questi aggiorna i dati si ha la sua prelazione in favore dell’esecuzione dell’altro. Il secondo processo può, a questo punto, tentare di leggere i dati che sono stati lasciati in uno stato incoerente dal primo processo.

La capacità di prelazione si ripercuote anche sulla progettazione del kernel del sistema operativo.
Durante l’elaborazione di una chiamata di sistema, il kernel può essere impegnato in attività per conto di un processo; tali attività possono comportare la necessità di modifiche a importanti dati del kernel, come le code di i/o. Se si ha la prelazione del processo durante tali modifiche e il kernel (o un driver di dispositivo) deve leggere o modificare gli stessi dati, si può avere il caos.
Un kernel senza prelazione attenderà che una chiamata di sistema venga completata o che un processo si blocchi in attesa di terminare l’i/o prima di eseguire un cambio di contesto.
Questo schema garantisce che la struttura del kernel sia semplice, poiché il kernel non può esercitare la prelazione su un processo mentre le sue strutture dati si trovano in uno stato incoerente. Sfortunatamente, questo modello d’esecuzione non è adeguato alle elaborazioni in tempo reale, in cui i task devono essere conclusi entro un intervallo fissato di tempo.

Un kernel con prelazione richiede meccanismi come i lock mutex (capitolo 6?) per prevenire le race condition quando si accede a strutture dati condivise del kernel.

La maggior parte dei sistemi operativi moderni è interamente con prelazione durante l’esecuzione in modalità kernel.