L’algoritmo di sostituzione delle pagine più semplice è un algoritmo fifo.
Questo algoritmo associa a ogni pagina l’istante di tempo in cui quella pagina è stata portata in memoria. 
Se si deve sostituire una pagina, si seleziona quella presente in memoria da più tempo. Occorre notare che non è strettamente necessario registrare l’istante in cui si carica una pagina in memoria; infatti si può creare una coda fifo di tutte le pagine presenti in memoria. 
In questo caso si sostituisce la pagina che si trova in testa alla coda. 
Quando si carica una pagina in memoria, la si inserisce nell’ultimo elemento della coda.


Nella successione di riferimenti di esempio, i nostri tre frame sono inizialmente vuoti.
I primi tre riferimenti (7, 0, 1) accusano ciascuno un page fault con conseguente caricamento delle relative pagine nei frame vuoti.
Il riferimento successivo (2) causa la sostituzione della pagina 7, perché essa è stata caricata per prima in memoria.
Siccome 0 è il riferimento successivo e si trova già in memoria, per questo riferimento non ha luogo alcun page fault.
Il primo riferimento a 3 causa la sostituzione della pagina 0, che ora è la prima pagina in coda.
A causa di questa sostituzione il riferimento successivo, a 0, causerà un page fault. 
La pagina 1 è poi sostituita dalla pagina 0. 
Questo processo prosegue come è illustrato nella seguente figura. 
![[Pasted image 20221213170505.png]]
Ogni volta che si verifica un page fault sono indicate le pagine presenti nei tre frame. Complessivamente si hanno 15 page fault.

L’algoritmo fifo di sostituzione delle pagine è facile da capire e da programmare; tuttavia la sue prestazioni non sono sempre buone. 
La pagina sostituita potrebbe essere un modulo di inizializzazione usato molto tempo prima e che non serve più, ma potrebbe anche contenere una variabile molto usata, inizializzata precedentemente, e ancora in uso.

Occorre notare che anche se si sceglie una pagina da sostituire che è in uso attivo, tutto continua a funzionare correttamente. 
Dopo aver rimosso una pagina attiva per inserirne una nuova, quasi immediatamente si verifica un’eccezione di page fault per riprendere la pagina attiva. Per riportare la pagina attiva in memoria è necessario sostituire un’altra pagina. 
Quindi, una cattiva scelta della pagina da sostituire aumenta il tasso di page fault e rallenta l’esecuzione del processo, ma non causa errori.


Per illustrare i problemi che possono insorgere con l’uso dell’algoritmo di sostituzione delle pagine fifo, si consideri la seguente successione di riferimenti:

1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5

Nella Figura 10.13 è illustrata la curva dei page fault per questa successione di riferimenti in funzione del numero dei frame disponibili. Occorre notare che il numero dei page fault (10) per quattro frame è _maggiore_ del numero dei page fault (9) per tre frame. Questo inatteso risultato è noto col nome di anomalia di Belady: con alcuni algoritmi di sostituzione delle pagine, il tasso di page fault può _aumentare_ con l il tasso minimo di page fault aumentare del numero dei frame assegnati. A prima vista sembra logico supporre che fornendo più memoria a un processo le prestazioni di quest’ultimo migliorino. In alcune delle prime ricerche sperimentali si notò invece che questo presupposto non sempre è vero; venne così individuata l’anomalia di Belady.

![[Pasted image 20221213171114.png]]