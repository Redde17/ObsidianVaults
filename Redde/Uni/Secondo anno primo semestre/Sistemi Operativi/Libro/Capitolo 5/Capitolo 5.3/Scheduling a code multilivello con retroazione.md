Di solito in un algoritmo di scheduling a code multilivello i processi si assegnano in modo permanente a una coda all’entrata nel sistema, e non si possono spostare tra le code.

Se, per esempio, esistono code distinte per i processi che si eseguono in foreground e quelli che si eseguono in background, i processi non possono passare da una coda all’altra, poiché non possono cambiare la loro natura di processi in foreground o in background. Quest’impostazione è rigida, ma ha il vantaggio di avere un basso carico di scheduling.

**Lo scheduling a code multilivello con retroazione (_multilevel feedback queue scheduling_)**, invece, permette ai processi di spostarsi fra le code.
L’idea consiste nel separare i processi che hanno caratteristiche diverse in termini di cpu burst. 
Se un processo usa troppo tempo di elaborazione della cpu, viene spostato in una coda con priorità più bassa. Questo schema mantiene i processi con prevalenza di i/o e i processi interattivi nelle code con priorità più elevata. Inoltre, si può spostare in una coda con priorità più elevata un processo che attende troppo a lungo in una coda a priorità bassa. Questa forma di aging impedisce il verificarsi di un’attesa indefinita.

Si consideri, per esempio, uno scheduler a code multilivello con retroazione con tre code, numerate da 0 a 2, come nella seguente figura:
![[Pasted image 20221106175737.png]]

Lo scheduler fa eseguire tutti i processi presenti nella coda 0; quando la coda 0 è vuota, si eseguono i processi nella coda 1; analogamente, i processi nella coda 2 si eseguono solo se le code 0 e 1 sono vuote. Un processo in ingresso nella coda 1 ha la prelazione sui processi della coda 2; un processo in ingresso nella coda 0, a sua volta, ha la prelazione sui processi della coda 1.

All’ingresso nella ready queue i processi vengono assegnati alla coda 0 e ottengono un quanto di tempo di 8 millisecondi; 
i processi che non terminano entro tale quanto di tempo, vengono spostati alla fine della coda 1. Se la coda 0 è vuota, si assegna un quanto di tempo di 16 millisecondi al processo alla testa della coda 1, ma se questo non riesce a completare la propria esecuzione, viene sottoposto a prelazione e messo nella coda 2.
Se le code 0 e 1 sono vuote, si eseguono i processi della coda 2 secondo il criterio fcfs. Per evitare l’attesa indefinita, un processo in attesa da troppo tempo in una coda a priorità bassa viene gradualmente spostato in una coda con priorità più alta.


Questo algoritmo di scheduling dà la massima priorità ai processi con una sequenza di operazioni della cpu della durata di non più di 8 millisecondi. 
I processi di questo tipo ottengono rapidamente la cpu, terminano la propria sequenza di operazioni della cpu e passano alla successiva sequenza di operazioni di i/o; anche i processi che necessitano di più di 8 ma di non più di 24 millisecondi (coda 1) vengono serviti rapidamente, anche se con una priorità inferiore. 
I processi più lunghi finiscono automaticamente nella coda 2 e sono serviti secondo il criterio fcfs all’interno dei cicli di cpu lasciati liberi dai processi delle code 0 e 1.

Generalmente uno scheduler a code multilivello con retroazione è caratterizzato dai seguenti parametri:
-   numero di code;
-   algoritmo di scheduling per ciascuna coda;
-   metodo usato per determinare quando spostare un processo in una coda con priorità maggiore;
-   metodo usato per determinare quando spostare un processo in una coda con priorità minore;
-   metodo usato per determinare in quale coda si deve mettere un processo quando richiede un servizio.

La definizione di uno scheduler a code multilivello con retroazione costituisce il più generale criterio di scheduling della cpu, che nella fase di progettazione si può adeguare a un sistema specifico. Sfortunatamente corrisponde anche all’algoritmo più complesso; la definizione dello scheduler migliore richiede infatti particolari metodi per la selezione dei valori dei diversi parametri.