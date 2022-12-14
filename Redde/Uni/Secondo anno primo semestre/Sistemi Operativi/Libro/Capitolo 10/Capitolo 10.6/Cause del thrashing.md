Il thrashing causa notevoli problemi di prestazioni.
Si consideri il seguente scenario, basato sul comportamento effettivo dei primi sistemi di paginazione.

Il sistema operativo controlla l’utilizzo della cpu.
Se questo è basso, aumenta il grado di multiprogrammazione introducendo un nuovo processo. 
Si usa un algoritmo di sostituzione delle pagine globale, che sostituisce le pagine senza tener conto del processo al quale appartengono. 
Ora si ipotizzi che un processo entri in una nuova fase d’esecuzione e richieda più frame; se ciò si verifica si ha una serie di page fault, cui segue la sottrazione di frame ad altri processi. Questi processi hanno però bisogno di quelle pagine e quindi subiscono anch’essi dei page fault, con conseguente sottrazione di frame ad altri processi. 
Per effettuare il caricamento e lo scaricamento delle pagine per questi processi si deve usare il dispositivo di paginazione. Mentre si mettono i processi in coda per il dispositivo di paginazione, la coda dei processi pronti per l’esecuzione si svuota, quindi l’utilizzo della cpu diminuisce.

Lo scheduler della cpu rileva questa riduzione dell’utilizzo della cpu e _aumenta_ il grado di multiprogrammazione. 
Si tenta di avviare il nuovo processo sottraendo pagine ai processi in esecuzione, causando ulteriori page fault e allungando la coda per il dispositivo di paginazione. Come risultato l’utilizzo della cpu scende ulteriormente, e lo scheduler della cpu tenta di aumentare ancora il grado di multiprogrammazione. 
Si è in una situazione di thrashing che fa precipitare la produttività del sistema. Il tasso dei page fault aumenta enormemente, e di conseguenza aumenta il tempo effettivo d’accesso alla memoria. I processi non svolgono alcun lavoro, poiché si sta spendendo tutto il tempo nell’attività di paginazione.

Questo fenomeno è illustrato nella seguente figura:
![[Pasted image 20221214174509.png]]
in cui si riporta l’utilizzo della cpu in funzione del grado di multiprogrammazione. Aumentando il grado di multiprogrammazione aumenta anche l’utilizzo della cpu, anche se più lentamente, fino a raggiungere un massimo. 
Se a questo punto si aumenta ulteriormente il grado di multiprogrammazione, l’attività di paginazione degenera e fa crollare l’utilizzo della cpu. In questa situazione, per aumentare l’utilizzo della cpu e bloccare il thrashing occorre _ridurre_ il grado di multiprogrammazione.

Gli effetti di questa situazione si possono limitare usando un algoritmo di sostituzione locale, o algoritmo di sostituzione per priorità. Con la sostituzione locale, se un processo entra in thrashing, non può sottrarre frame a un altro processo e quindi provocarne a sua volta la degenerazione. 
Tuttavia il problema non è completamente risolto. 
I processi in thrashing rimangono nella coda d’attesa del dispositivo di paginazione per la maggior parte del tempo. Il tempo di servizio medio di un page fault aumenta a causa dell’allungamento della coda media d’attesa del dispositivo di paginazione. Di conseguenza, il tempo effettivo d’accesso in memoria aumenta anche per gli altri processi.

Per evitare il verificarsi di queste situazioni, occorre fornire a un processo tutti i frame di cui necessita. Per cercare di sapere quanti frame “servano” a un processo si impiegano diverse tecniche. 
L’approccio del working-set comincia osservando quanti siano i frame che un processo sta effettivamente usando. 
Questo approccio definisce il modello di località d’esecuzione del processo.

Il modello di località stabilisce che un processo, durante la sua esecuzione, si sposta di località in località. 
Una località è un insieme di pagine usate attivamente insieme. Generalmente un programma è formato di parecchie località diverse, che sono sovrapponibili. Per esempio, quando s’invoca una procedura, essa definisce una nuova località. In questa località si fanno riferimenti alla memoria per le istruzioni della procedura, per le sue variabili locali e per un sottoinsieme delle variabili globali. Quando la procedura termina, il processo lascia questa località, poiché le variabili locali e le istruzioni della procedura non sono più usate attivamente. Potrà tornare più tardi in questa località.

La seguente figura illustra il concetto di località e come la località di un processo cambia nel tempo. 
![[Pasted image 20221214174802.png]]
Al momento (a), la località è l’insieme di pagine {18, 19, 20, 21, 22, 23, 24, 29, 30, 33}. 
Al momento (b), la località cambia in {18, 19, 20, 24, 25, 26, 27, 28, 29, 31, 32, 33}. Si noti la sovrapposizione: alcune pagine (per esempio, 18, 19 e 20) fanno parte di entrambe le località.

Quindi, le località sono definite dalla struttura del programma e dalle relative strutture dati. Il modello di località sostiene che tutti i programmi mostrino questa struttura di base di riferimenti alla memoria. Si noti che il modello di località è il principio non dichiarato sottostante all’analisi fin qui svolta sul caching. Se gli accessi ai vari tipi di dati fossero casuali, anziché strutturati in località, il caching sarebbe inutile.

Si supponga di allocare a un processo un numero di frame sufficiente per sistemare le sue località attuali. Finché tutte queste pagine non si trovano in memoria, si verificano le assenze delle pagine relative a tali località; quindi, finché le località non vengano modificate, non hanno luogo altri page fault. Se si assegnano meno frame rispetto alla dimensione della località attuale, la paginazione del processo degenera, poiché non si possono tenere in memoria tutte le pagine che il processo sta usando attivamente.