La memoria centrale e i registri incorporati nel processore sono le sole aree di memorizzazione a cui la cpu può accedere direttamente.

Vi sono istruzioni macchina che accettano gli indirizzi di memoria come argomenti, ma nessuna accetta gli indirizzi del disco. Pertanto, qualsiasi istruzione in esecuzione, e tutti i dati utilizzati dalle istruzioni, devono risiedere in uno di questi dispositivi di memorizzazione ad accesso diretto. 

I dati che non sono in memoria devono essere caricati prima che la cpu possa operare su di loro.I registri incorporati nella cpu sono accessibili, in genere, nell’arco di un ciclo del clock della cpu.


I registri incorporati nella cpu sono accessibili, in genere, nell’arco di un ciclo del clock della cpu.
I core di alcune cpu sono capaci di decodificare istruzioni ed effettuare semplici operazioni sui contenuti dei registri alla velocità di una o più operazioni per ciclo. 
Ciò non vale per la memoria centrale, cui si accede tramite una transazione sul bus della memoria che può richiedere molti cicli di clock. 
In tal caso il processore entra necessariamente in stallo (_stall_), poiché manca dei dati richiesti per completare l’istruzione che sta eseguendo. Questa situazione è intollerabile, perché gli accessi alla memoria sono frequenti. 

Il rimedio consiste nell’interposizione di una memoria veloce tra cpu e memoria centrale. 
Di solito questo buffer di memoria, detto **cache**, si trova sul chip della cpu, in modo da garantire un accesso più rapido. Nella gestione di una cache interna alla cpu l’hardware si occupa direttamente di accelerare l’accesso alla memoria, senza l’intervento del sistema operativo.

Non basta prestare attenzione alle velocità relative di accesso alla memoria fisica, ma occorre anche assicurare una corretta esecuzione delle operazioni. 
A tal fine, bisogna proteggere il sistema operativo dall’accesso dei processi utenti, e, in sistemi multiutente, salvaguardare i processi utenti l’uno dall’altro. Tale protezione deve essere messa in atto a livello hardware, perché solitamente il sistema operativo, per una questione di prestazioni, non interviene negli accessi della cpu alla memoria. 
Come si vedrà lungo tutto il capitolo, questa protezione può essere realizzata dall’hardware con meccanismi diversi. In questo paragrafo evidenziamo una delle possibili implementazioni.

Innanzitutto, bisogna assicurarsi che ciascun processo abbia uno spazio di memoria separato, in modo da proteggere i processi l’uno dall’altro: ciò è fondamentale per avere più processi caricati in memoria per l’esecuzione concorrente. Per separare gli spazi di memoria occorre poter determinare l’intervallo degli indirizzi a cui un processo può accedere legalmente, e garantire che possa accedere soltanto a questi indirizzi. Si può implementare il meccanismo di protezione tramite due registri, detti **registro base** e **registro limite**, come illustrato nella seguente figura:
![[Pasted image 20221128162152.png]]
Il registro base contiene il più piccolo indirizzo legale della memoria fisica; il registro limite determina la dimensione dell’intervallo ammesso. 
Per esempio, se i registri base e limite contengono rispettivamente i valori 300040 e 120900, al programma si consente l’accesso agli indirizzi compresi tra 300040 e 420939, estremi inclusi.

Per mettere in atto il meccanismo di protezione, la cpu confronta ciascun indirizzo generato in modalità utente con i valori contenuti nei due registri. 
Qualsiasi tentativo da parte di un programma eseguito in modalità utente di accedere alle aree di memoria riservate al sistema operativo o a una qualsiasi area di memoria riservata ad altri utenti comporta l’invio di una **eccezione** (**_trap_**) che restituisce il controllo al sistema operativo che, a sua volta, interpreta l’evento come un **errore fatale**.

![[Pasted image 20221128162323.png]]

Questo schema impedisce a qualsiasi programma utente di alterare (accidentalmente o intenzionalmente) il codice o le strutture dati del sistema operativo o degli altri utenti.

Solo il sistema operativo può caricare i registri base e limite, grazie a una speciale istruzione privilegiata. 
Dal momento che le istruzioni privilegiate possono essere eseguite unicamente in modalità kernel, e poiché solo il sistema operativo può essere eseguito in tale modalità, tale schema gli consente di modificare il valore di questi registri, ma impedisce tale operazione ai programmi utenti.

Grazie all’esecuzione in modalità kernel, il sistema operativo ha la possibilità di accedere indiscriminatamente sia alla memoria a esso riservata sia a quella riservata agli utenti. 
Questo privilegio consente al sistema di caricare i programmi utenti nelle aree di memoria a loro riservate; di generare copie del contenuto di queste regioni di memoria (_dump_) a scopi diagnostici, qualora si verifichino errori; di modificare i parametri delle chiamate di sistema; di eseguire i/o da e verso la memoria utente e di fornire molti altri servizi. 
Consideriamo, per esempio, che un sistema operativo per un sistema multiprocessing deve effettuare cambi di contesto, memorizzando lo stato di un processo dai registri nella memoria centrale prima di caricare il contesto del processo successivo dalla memoria centrale nei registri.