---------------
#### Riassunto
Per migliorare le prestazioni si possono usare una maggiore quantitá di dischi in parallelo cosí da potervi accedere in parallelo, questa tecnica é chiamata striping, lo striping puó essere eseguito su bit di byte, quindi avendo 8 unitá di memoria é possibile conservare un bit su ogni drive per formare un byte durante la lettura, questa permette tempi di lettura elevati rispetto a un sistema senza striping.
Lo striping puó anche essere svolto a blocchi invece che a bit

-------------


Vediamo come l’accesso in parallelo a più dischi può migliorare le prestazioni. Con il mirroring, la frequenza con la quale si possono gestire le richieste di lettura raddoppia, poiché ciascuna richiesta si può inviare indifferentemente a uno dei due dischi (sempre che entrambi i dischi siano funzionanti, condizione che è quasi sempre soddisfatta). La capacità di trasferimento di ciascuna lettura è la stessa di quella di un sistema a singolo disco, ma il numero di letture per unità di tempo raddoppia.

Attraverso l’uso di più unità di memorizzazione è possibile anche (o alternativamente) migliorare la capacità di trasferimento distribuendo i dati in sezioni su più dispositivi. La forma più semplice di questa distribuzione (_data striping_), consiste nel distribuire i bit di ciascun byte su più dispositivi; in questo caso si parla di sezionamento o striping a livello dei bit. Per esempio, se il sistema impiega un array di otto dispositivi, si scriverà il bit _i_ di ciascun byte nel disco _i_. L’array di otto dispositivi si può trattare come un unico dispositivo avente settori che hanno una dimensione otto volte superiore a quella normale e, soprattutto, che hanno una capacità di trasferimento otto volte superiore. In un’organizzazione di questo tipo, ogni dispositivo è coinvolto in ogni accesso (lettura o scrittura che sia), così che il numero di accessi che si possono gestire nell’unità di tempo è circa lo stesso di quello per un sistema a dispositivo singolo, ma ogni accesso permette di leggere una quantità di dati pari a otto volte quella che si può leggere con un singolo dispositivo.

Lo striping a livello dei bit si può generalizzare a un numero di dispositivi multiplo di 8 o che divide 8. Per esempio, se un sistema adopera un array di quattro dispositivi, i bit _i_ e _i_ + 4 di ciascun byte si memorizzano nel disco _i_. Inoltre, lo striping non si deve realizzare necessariamente a livello dei bit di un byte: nello striping a livello di blocco, per esempio, i blocchi di un file si distribuiscono su più dispositivi; con _n_ dispositivi, il blocco _i_ di un file si memorizza nel dispositivi (_i_ mod _n_) + 1. Sono possibili anche altri livelli di striping, come quelli basati sui byte di un settore o sui settori di un blocco, ma lo striping a livello di blocco è il più comune.

Riassumendo, gli obiettivi principali del parallelismo mediante striping in un sistema di dispositivi sono due:
1.  l’aumento, tramite il bilanciamento del carico, del throughput per accessi multipli a piccole porzioni di dati (cioè accessi a pagine);
2.  la riduzione del tempo di risposta relativo ad accessi a grandi quantità di dati.