Le decisioni riguardanti lo scheduling della cpu vengono prese nelle seguenti quattro circostanze:
1.  un processo passa dallo stato di esecuzione allo stato di attesa (per esempio, richiesta di i/o o invocazione di wait() per la terminazione di uno dei processi figli);
2.  un processo passa dallo stato di esecuzione allo stato pronto (per esempio, quando si verifica un segnale d’interruzione);
3.  un processo passa dallo stato di attesa allo stato pronto (per esempio, al completamento di un’operazione di i/o);
4.  un processo termina.

I casi 1 e 4 non danno alternative in termini di scheduling: si deve comunque scegliere un nuovo processo da eseguire, sempre che ce ne sia almeno uno nella ready queue per l’esecuzione. Una scelta si può invece fare nei casi 2 e 3.

**Quando lo scheduling interviene solo nelle condizioni 1 e 4, si dice che lo schema di scheduling è senza prelazione (_nonpreemptive_) o cooperativo (_cooperative_); altrimenti, lo schema di scheduling è con prelazione (_preemptive_).**

Nel caso dello scheduling senza prelazione, quando si assegna la cpu a un processo, questo rimane in possesso della cpu fino al momento del suo rilascio, dovuto al termine dell’esecuzione o al passaggio nello stato di attesa. Praticamente tutti i moderni sistemi operativi, inclusi Windows, macos, Linux e unix, utilizzano algoritmi di scheduling con prelazione.

Sfortunatamente lo scheduling con prelazione può portare a _race condition_ quando i dati sono condivisi tra diversi processi. Si consideri il caso in cui due processi condividono dati; mentre uno di questi aggiorna i dati si ha la sua prelazione in favore dell’esecuzione dell’altro. Il secondo processo può, a questo punto, tentare di leggere i dati che sono stati lasciati in uno stato incoerente dal primo processo.