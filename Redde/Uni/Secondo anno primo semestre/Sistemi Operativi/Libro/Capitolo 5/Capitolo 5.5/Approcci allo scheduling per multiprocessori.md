Una prima strategia di scheduling della cpu per i sistemi multiprocessore affida tutte le decisioni, l’elaborazione dell’ i/o e altre attività del sistema a un solo processore, il cosiddetto _master server_.
Gli altri processori eseguono soltanto il codice utente. Si tratta della multielaborazione asimmetrica, che riduce la necessità di condividere dati grazie all’accesso di un solo processore alle strutture dati del sistema. 

Lo svantaggio di questo approccio è che il master server costituisce un potenziale collo di bottiglia in grado di ridurre le prestazioni generali del sistema.

L’approccio standard per supportare i multiprocessori è la multielaborazione simmetrica (smp), in cui ciascun processore è in grado di autogestirsi. 
Lo scheduling viene realizzato facendo in modo che lo scheduler di ciascun processore esamini la ready queue e selezioni un thread da eseguire. 
Si noti che questo approccio offre due possibili strategie per organizzare i thread da selezionare per l’esecuzione:
1.  tutti i thread possono trovarsi in una ready queue comune;
2.  ogni processore può avere una propria coda privata di thread.
La seguente figura mostra un confronto tra le due strategie.
![[Pasted image 20221107153108.png]]
Se viene utilizzata la prima opzione è possibile avere race condition sulla coda condivisa e occorre quindi assicurarsi che due processori distinti non scelgano di eseguire lo stesso thread e che i thread nella coda non vengano persi. 
Come discusso nel Capitolo 6 è possibile usare una forma di lock per proteggere la ready queue comune da questa race condition.

 La seconda opzione permette a ciascun processore di schedulare i thread da una coda di esecuzione privata e pertanto non risente dei possibili problemi di prestazioni associati a una coda condivisa.
 Per questa ragione si tratta dell’approccio più comune sui sistemi che supportano smp.
 Inoltre, l’uso di code di esecuzione private, una per ogni processore, può portare a un uso più efficiente della memoria cache.
 Vi sono anche dei problemi nell’utilizzo di code distinte per ogni processore, in particolare relativi ai diversi carichi di lavoro. Tuttavia, come vedremo, possono essere utilizzati algoritmi di bilanciamento per distribuire equamente i carichi di lavoro tra tutti i processori.
 
Praticamente tutti i sistemi operativi moderni supportano smp, inclusi Windows, Linux, macos e i sistemi mobili Android e ios.