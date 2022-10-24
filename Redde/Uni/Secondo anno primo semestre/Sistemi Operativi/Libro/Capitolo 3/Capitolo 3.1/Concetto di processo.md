Sebbene noi preferiamo il termine più moderno _processo_, occorre ricordare che la maggior parte della terminologia e della teoria dei sistemi operativi si è sviluppata in un periodo in cui l’attività principale dei sistemi operativi riguardava la gestione dei _job_ in sistemi batch.

Informalmente, come affermato precedentemente, un processo è un programma in esecuzione. Lo stato dell’attività corrente di un processo è rappresentato dal valore del contatore di programma e dal contenuto dei registri del processore. La struttura di un processo in memoria è generalmente suddivisa in più sezioni, tali sezioni sono le seguenti.
![[Pasted image 20221024163506.png]]
- **Sezione di testo**: contenente il codice eseguibile.
- **Sezioni dati:** contenente le varibili globali.
- **Heap**: memoria allocata dinamicamente durante l'esecuzione del programma.
- **Stack**: memoria temporanea utilizzata durante le chiamate di funzioni (per esempio per i parametri delle funzioni, gli inidirizzi di ritorno e le variabili locali)

Si noti che le dimensioni delle **sezioni di testo e dati sono fisse**, ovvero non cambiano durante l’esecuzione del programma, mentre le **sezioni stack e heap possono ridursi e crescere dinamicamente** durante l’esecuzione. Ogni volta che si chiama una funzione, un **record di attivazione** (_activation record_) contenente i suoi parametri, le variabili locali e l’indirizzo di ritorno viene inserito nello stack; quando la funzione restituisce il controllo al chiamante, il record di attivazione viene rimosso dallo stack. Allo stesso modo, l’heap crescerà quando viene allocata memoria dinamicamente e si ridurrà quando la memoria viene restituita al sistema. **Visto che le sezioni stack e heap _crescono l’una verso l’altra_, tocca al sistema operativo garantire che _non si sovrappongano_.**

Sottolineiamo che **un programma di per sé non è un processo**; un programma è un’entità _passiva_, come un file su disco contenente una lista di istruzioni (normalmente chiamato file eseguibile), mentre un processo è un’entità _attiva_, con un contatore di programma che specifica qual è l’istruzione successiva da eseguire e un insieme di risorse associate. **Un programma diventa un processo allorquando il file eseguibile è caricato in memoria**.

**Sebbene due processi siano associabili allo stesso programma, sono tuttavia da considerare due sequenze d’esecuzione distinte.**

**Si noti che un processo può essere un ambiente di esecuzione per altro codice.**

La figura seguente mostra la struttura di un programma C in memoria, evidenziando la relazione tra le diverse sezioni di un processo e un programma C reale. Questa figura è simile alla rappresentazione generale di un processo in memoria, mostrata nella figura precedente, con alcune differenze.
-   La sezione dei dati globali è suddivisa in sezioni distinte per (a) dati inizializzati e (b) dati non inizializzati.
-   È presente una sezione separata per i parametri argc e argv passati alla funzione main().
![[Pasted image 20221024164312.png]]

