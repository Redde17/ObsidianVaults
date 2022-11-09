Si usa distinguere tra **semafori contatore**, il cui valore è un numero intero, e i **semafori binari**, il cui valore è limitato a 0 o 1.
I semafori binari sono dunque simili ai lock mutex e vengono utilizzati al loro posto per la mutua esclusione nei sistemi dove i lock mutex non sono disponibili.

I semafori contatore trovano applicazione nel controllo dell’accesso a una data risorsa presente in un numero finito di esemplari. 
Il semaforo è inizialmente impostato al numero di risorse disponibili. I processi che desiderino utilizzare una risorsa invocano wait() sul semaforo, decrementandone così il valore; i processi che restituiscono una risorsa, invece, invocano signal() sul semaforo, incrementandone il valore. Quando il semaforo vale 0, tutte le risorse sono occupate, e i processi che ne richiedano l’uso dovranno bloccarsi fino a che il semaforo non ritorni positivo.

I semafori sono utilizzabili anche per risolvere diversi problemi di sincronizzazione. 
Si considerino, per esempio, due processi in esecuzione concorrente: _P1_ con un’istruzione _S1_ e _P2_ con un’istruzione _S2_. 
Si supponga di voler eseguire _S2_ solo dopo che _S1_ è terminata. 
Questo schema si può prontamente realizzare facendo condividere a _P1_ e _P2_ un semaforo comune, synch, inizializzato a 0, e inserendo nel processo _P1_ le istruzioni
```
S1;
signal(synch);
```

e nel processo _P2_ le istruzioni
```
wait(synch);
S2;
```

Poiché synch è inizializzato a 0, _P2_ esegue _S2_ solo dopo che _P1_ ha eseguito signal(synch), che si trova dopo _S1_.



