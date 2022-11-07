Tradizionalmente i sistemi smp hanno reso possibile la concorrenza tra thread con l’utilizzo di diversi processori fisici. 
Tuttavia, la pratica recente nel progetto hardware dei calcolatori è di inserire più core di elaborazione in un unico chip fisico, dando origine a un processore multicore. 
Ogni core mantiene il proprio stato e appare dunque al sistema operativo come un processore fisico separato. 
I sistemi smp che usano processori multicore sono più veloci e consumano meno energia dei sistemi in cui ciascun processore è costituito da un singolo chip.

I processori multicore possono complicare i problemi relativi allo scheduling. 
Proviamo a vedere che cosa può succedere. Le ricerche hanno permesso di scoprire che quando un processore accede alla memoria, una quantità significativa di tempo trascorre in attesa della disponibilità dei dati. 
Questa situazione, nota come stallo della memoria, può verificarsi per varie ragioni, per esempio la mancanza dei dati richiesti nella cache. 
La seguente figura mostra uno stallo della memoria. In questo scenario, il processore può trascorrere fino al 50 per cento del suo tempo attendendo che i dati siano disponibili in memoria.
![[Pasted image 20221107160519.png]]

Per rimediare a questa situazione, molti dei progetti hardware recenti implementano delle unità di calcolo multithread in cui due o più thread hardware sono assegnati a un singolo core. 
In questo modo, se un thread è in situazione di stallo in attesa della memoria, il core può passare a eseguire un altro thread. 
La seguente figura mostra un processore a due thread nel quale l’esecuzione dei thread 0 e 1 sono avvicendate nel tempo.
![[Pasted image 20221107161308.png]]
Dal punto di vista del sistema operativo, ogni thread hardware mantiene il suo stato architetturale, come il puntatore alle istruzioni e il set di registri, e appare quindi come una cpu logica che è disponibile per eseguire un thread software. 
Questa tecnica, nota come chip multithreading (cmt), è illustrata nella seguente figura, dove è mostrato un processore contenente quattro core di elaborazione, ognuno dei quali contiene due thread hardware: dal punto di vista del sistema operativo sono presenti otto cpu logiche.
![[Pasted image 20221107161341.png]]
I processori Intel utilizzano il termine hyper-threading (noto anche come _multithreading simultaneo_ o smt) per descrivere l’assegnazione di più thread hardware a un singolo core di elaborazione. 
I processori Intel contemporanei, come l’i7, supportano due thread per core, mentre il processore Oracle Sparc M7 supporta otto thread per core, con otto core per processore, fornendo così al sistema operativo 64 cpu logiche.

In generale, ci sono due modi per rendere un core multithread:
attraverso il **multithreading a grana grossa (_coarse-grained_)** o il **multithreading a grana fine (_fine-grained_)**.
Nel **multithreading coarse-grained** un thread resta in esecuzione su un processore fino al verificarsi di un evento a lunga latenza, per esempio uno stallo di memoria. A causa dell’attesa introdotta dall’evento a lunga latenza, il processore deve passare a un altro thread e iniziare a eseguirlo. Tuttavia, il costo per cambiare il thread in esecuzione è alto, perché occorre ripulire la pipeline delle istruzioni prima che il nuovo thread possa iniziare a essere eseguito sull’unità di calcolo. Una volta che il nuovo thread è in esecuzione inizia a riempire la pipeline con le sue istruzioni.

Il multithreading fine (anche detto _interleaved multithreading_) passa da un thread a un altro a un livello molto più fine di granularità (tipicamente al termine di un ciclo di istruzione). Tuttavia, il progetto di sistemi a multithreading fine include una logica dedicata al cambio di thread. Ne risulta così che il costo del passaggio da un thread a un altro è piuttosto basso.

È importante notare che le risorse del core fisico (come cache e pipeline) devono essere condivise tra i suoi thread hardware e dunque un core di elaborazione può eseguire solo un thread hardware alla volta. 
Di conseguenza, un processore multithreaded e multicore richiede due diversi livelli di scheduling, come mostrato nella seguente figura, che illustra un core di elaborazione dual-threaded.
![[Pasted image 20221107162711.png]]
A un livello vi sono le decisioni di scheduling che devono essere prese dal sistema operativo per scegliere quale thread software eseguire su ogni thread hardware (cpu logica). 
Il sistema operativo può scegliere qualsiasi algoritmo.

Un secondo livello di scheduling specifica in che modo ciascun core decide quale thread hardware eseguire. 
In questa situazione è possibile adottare diverse strategie. 
Un approccio consiste nell’utilizzare un semplice algoritmo round-robin per assegnare un thread hardware al core di elaborazione:
Oppure viene assegnato a ciascun thread hardware un indice dinamico di urgenza (_urgency_) compreso tra 0 e 7, dove 0 rappresenta l’urgenza più bassa e 7 la più alta. 
Il processore identifica cinque diversi eventi in grado di attivare un cambio di thread. 
Quando si verifica uno di questi eventi, la logica di cambio di thread confronta l’urgenza dei due thread e seleziona il thread con il valore di urgenza più alto da eseguire sul core del processore.

Si noti che i due diversi livelli di scheduling mostrati nella figura precedente non sono necessariamente mutuamente esclusivi. 
Infatti, se lo scheduler del sistema operativo (il primo livello) viene reso consapevole della condivisione delle risorse del processore, può prendere decisioni di scheduling più efficaci.
Per esempio, supponiamo che una cpu abbia due core di elaborazione e che ogni core abbia due thread hardware. 
Se due thread software sono in esecuzione su questo sistema, possono essere in esecuzione sullo stesso core o su core separati. 
Se entrambi vengono assegnati allo stesso core, devono condividere le risorse del processore e quindi è probabile che procedano più lentamente rispetto al caso in cui siano assegnati a core distinti. 
Se il sistema operativo è a conoscenza del livello di condivisione delle risorse del processore può programmare i thread software su processori logici che non condividono risorse.

#### Chiarimenti personali:
Un thread logico é definibile come un processe da eseguire, una serie di comandi.
Un thread fisico sarebbe effettivamente il core che é in grado di eseguire i thread software.
Grazie all'hyper-threading un singolo core é in grado di gestire piú thread fisici ma eeffettivamente eseguirne uno alla volta poiché le risorse dei thread fisici sono condivisi. 
La quantitá di thread fisici per core dipende dall'architettura di un processore.