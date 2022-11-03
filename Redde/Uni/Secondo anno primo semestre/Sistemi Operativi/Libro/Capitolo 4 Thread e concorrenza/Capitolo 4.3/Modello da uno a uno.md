Il modello da uno a uno mette in corrispondenza ciascun thread a livello utente con un thread a livello kernel.

Questo modello offre un grado di concorrenza maggiore rispetto al molti a uno, poiché anche se un thread invoca una chiamata di sistema bloccante, è possibile eseguire un altro thread;
Il modello permette anche l’esecuzione dei thread in parallelo nei sistemi multiprocessore. 

L’unico svantaggio di questo modello è che la creazione di ogni thread a livello utente comporta la creazione del corrispondente thread a livello kernel.

Poiché il carico dovuto alla creazione di un thread a livello kernel può sovraccaricare le prestazioni di un’applicazione, la maggior parte delle realizzazioni di questo modello limita il numero di thread supportabili dal sistema.

![[Pasted image 20221102170340.png]]

I sistemi operativi Linux, insieme alla famiglia dei sistemi operativi Windows, adottano il modello da uno a uno.