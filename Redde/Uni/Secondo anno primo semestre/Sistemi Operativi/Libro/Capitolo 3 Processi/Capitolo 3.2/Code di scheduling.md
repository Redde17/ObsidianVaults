Entrando nel sistema, ogni processo è inserito in una coda di processi pronti e in attesa d’essere eseguiti, detta **coda dei processi pronti (_ready queue_)**. Questa coda generalmente viene memorizzata come una lista concatenata: 
*un’intestazione della coda dei processi pronti contiene i puntatori al primo pcb della lista, e ciascun pcb comprende un campo puntatore che indica il successivo processo contenuto nella coda.*

Il sistema operativo ha anche altre code. Quando si assegna un core della cpu a un processo, quest’ultimo rimane in esecuzione per un certo tempo e prima o poi termina, viene interrotto, oppure si ferma nell’attesa di un evento particolare, come il completamento di una richiesta di i/o. Supponiamo che il processo effettui una richiesta di i/o su un disco. 
Poiché i dispositivi periferici sono molto più lenti dei processori, il processo dovrà attendere che l’ i/o diventi disponibile. I processi in attesa di un determinato evento, per esempio il completamento dell’ i/o, vengono collocati in una coda di attesa, o _wait queue_

[[Blocco di controllo del processo o PCB]]
![[Pasted image 20221027152426.png]]

Una comune rappresentazione dello scheduling dei processi è data da un diagramma di accodamento come quello illustrato nella figura sottostante. Sono presenti due tipi di coda: la ready queue e un insieme di wait queue. I cerchi rappresentano le risorse che servono le code, le frecce indicano il flusso di processi nel sistema.

![[Pasted image 20221027152448.png]]

Un nuovo processo si colloca inizialmente nella ready queue, dove attende finché non è selezionato per essere eseguito (_dispatched_). Una volta che il processo è assegnato alla cpu ed è nella fase d’esecuzione, si può verificare uno dei seguenti eventi:
-   il processo può emettere una richiesta di i/o e quindi essere inserito in una coda di i/o;
-   il processo può creare un nuovo processo figlio e attenderne la terminazione;
-   il processo può essere rimosso forzatamente dalla cpu a causa di un’interruzione, ed essere reinserito nella coda dei processi pronti.

Nei primi due casi, al completamento della richiesta di i/o o al termine del processo figlio, il processo passa dallo stato d’attesa allo stato pronto ed è nuovamente inserito nella ready queue. Un processo continua questo ciclo fino al termine della sua esecuzione: a questo punto viene rimosso da tutte le code, e vengono deallocati il suo pcb e le varie risorse.