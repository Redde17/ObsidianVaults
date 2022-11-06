Nello scheduling con priorità e in quello circolare tutti i processi possono essere collocati in una singola coda da cui lo scheduler seleziona il processo con la priorità più alta da eseguire. A seconda di come vengono gestite le code può essere necessaria una ricerca _O_(_n_) per determinare il processo con maggiore priorità.

Nella pratica è spesso più semplice disporre di code separate per ciascuna priorità distinta e lasciare che lo scheduling con priorità si occupi semplicemente di selezionare il processo nella coda con priorità più alta, come illustrato nella seguente figura:
![[Pasted image 20221106174959.png]]

Questo approccio, noto come scheduling a code multilivello, funziona bene anche quando lo scheduling con priorità è combinato con lo scheduling rr: se ci sono più processi nella coda con priorità più alta, questi vengono eseguiti in ordine circolare. 

Nella forma più generale di questo approccio viene assegnata una priorità statica a ciascun processo e un processo rimane nella stessa coda per tutto il suo tempo di esecuzione.

Un algoritmo di scheduling a code multilivello può anche essere utilizzato per suddividere i processi in diverse code in base al tipo di processo:
![[Pasted image 20221106175107.png]]
Per esempio, di solito vengono divisi i processi in primo piano (interattivi) e i processi in background (batch).
Questi due tipi di processi hanno requisiti diversi in termini di tempo di risposta e possono quindi avere esigenze di scheduling diverse. Inoltre, i processi in primo piano possono avere una priorità più alta (definita esternamente) rispetto ai processi in background.
È possibile utilizzare code distinte per i processi in primo piano e in background e ciascuna coda potrebbe avere il proprio algoritmo di schedulazione. Per la coda in primo piano si potrebbe utilizzare, per esempio, un algoritmo rr, mentre lo scheduling della coda in background potrebbe utilizzare un algoritmo fcfs.

In questa situazione è inoltre necessario avere uno scheduling tra le code; si tratta comunemente di uno scheduling a priorità fissa con prelazione. Per esempio, la coda dei processi in foreground (in primo piano) può avere la priorità assoluta sulla coda dei processi in background.

Si consideri come esempio il seguente algoritmo di scheduling a code multilivello, in ordine di priorità:
1.  processi in tempo reale
2.  processi di sistema
3.  processi interattivi
4.  processi batch

Ogni coda ha la priorità assoluta sulle code di priorità più bassa; per esempio nessun processo della coda dei processi batch può iniziare l’esecuzione finché le code per i processi di sistema, interattivi e interattivi di _editing_ non siano tutte vuote. Se un processo interattivo di _editing_ entrasse nella ready queue durante l’esecuzione di un processo in background, si avrebbe la prelazione su quest’ultimo.

Un’altra possibilità è definire porzioni di tempo per le code. A ogni coda si assegna una parte del tempo d’elaborazione della cpu, suddivisibile a sua volta tra i processi che la costituiscono. Nel caso foreground/background, per esempio, si può assegnare l’80 per cento del tempo d’elaborazione della cpu alla coda dei processi in foreground (in primo piano), con scheduling rr tra i suoi processi; mentre per la coda dei processi in background si riserva il 20 per cento del tempo d’elaborazione della cpu, assegnato col criterio fcfs.