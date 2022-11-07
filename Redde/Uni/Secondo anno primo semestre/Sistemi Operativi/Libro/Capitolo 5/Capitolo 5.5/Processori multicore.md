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

I processori Intel utilizzano il termine hyper-threading (noto anche come _multithreading simultaneo_ o smt) per descrivere l’assegnazione di più thread hardware a un singolo core di elaborazione. I processori Intel contemporanei, come l’i7, supportano due thread per core, mentre il processore Oracle Sparc M7 supporta otto thread per core, con otto core per processore, fornendo così al sistema operativo 64 cpu logiche.