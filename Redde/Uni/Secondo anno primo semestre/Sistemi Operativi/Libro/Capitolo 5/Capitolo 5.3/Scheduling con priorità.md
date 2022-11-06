L’algoritmo sjf è un caso particolare del più generale algoritmo di scheduling con priorità: 
si associa una priorità a ogni processo e si assegna la cpu al processo con priorità più alta; 
i processi con priorità uguali si ordinano secondo uno schema fcfs. 

Un algoritmo sjf è semplicemente un algoritmo con priorità in cui la priorità (_p_) è l’inverso della lunghezza (prevista) della successiva sequenza di operazioni della cpu. A una maggiore lunghezza corrisponde una minore priorità, e viceversa.

Occorre notare che la discussione si svolge in termini di priorità _alta_ e priorità _bassa_. Generalmente le priorità sono indicate da un intervallo fisso di numeri, come da 0 a 7, oppure da 0 a 4.095. Tuttavia, non c’è un orientamento comune sull’attribuire allo 0 la priorità più alta o quella più bassa; alcuni sistemi usano numeri bassi per rappresentare priorità basse, altri usano numeri bassi per priorità alte, il che può generare confusione. **In questo testo i numeri bassi indicano priorità alte.**

Come esempio, si consideri il seguente insieme di processi, che si suppone siano arrivati al tempo 0, nell’ordine _P1, _P2 ... _P5, e dove la durata delle sequenze di operazioni della cpu è espressa in millisecondi:
![[Pasted image 20221106174053.png]]
Usando lo scheduling con priorità, questi processi sarebbero ordinati secondo il seguente diagramma di Gantt.
![[Pasted image 20221106174125.png]]
**Il tempo d'attesa medio é di (0+1+6+16+18) / 5 = 8,2 millisecondi.** 

Le priorità si possono definire sia **_internamente_ sia _esternamente_**.
Quelle definite **internamente** usano una o più quantità misurabili per calcolare la priorità del processo; per esempio sono stati utilizzati i limiti di tempo, i requisiti di memoria, il numero dei file aperti e il rapporto tra la lunghezza media delle sequenze di operazioni di i/o e la lunghezza media delle sequenze di operazioni della cpu.
Le priorità **esterne** si definiscono secondo criteri esterni al sistema operativo, come l’importanza del processo, il tipo e la quantità dei fondi pagati per l’uso del calcolatore, il dipartimento che promuove il lavoro e altri fattori, spesso di ordine politico.

**Lo scheduling con priorità può essere sia con prelazione sia senza prelazione.**
Quando un processo arriva alla ready queue, si confronta la sua priorità con quella del processo attualmente in esecuzione. 
Un algoritmo di scheduling con priorità con diritto di prelazione sottrae la cpu al processo attualmente in esecuzione se la priorità del processo appena arrivato è superiore. 
Un algoritmo senza prelazione si limita a porre l’ultimo processo arrivato alla testa della ready queue.

Un problema importante relativo agli algoritmi di scheduling con priorità è l’attesa indefinita (_starvation_). Un processo pronto per l’esecuzione, ma che non dispone della cpu, si può considerare bloccato nell’attesa della cpu.
Un algoritmo di scheduling con priorità può lasciare processi a bassa priorità nell’attesa indefinita della cpu. In un sistema con carico elevato, un flusso costante di processi con priorità maggiore può impedire a un processo con bassa priorità di accedere alla cpu.

Una soluzione al problema dell’attesa indefinita dei processi con bassa priorità è costituita dall’invecchiamento (_aging_); si tratta di una tecnica di aumento graduale delle priorità dei processi che attendono nel sistema da parecchio tempo. Per esempio, se le priorità variano da 127 (bassa) a 0 (alta), si potrebbe incrementare di 1 ogni secondo il livello di priorità di un processo in attesa. Alla fine anche un processo con priorità iniziale 127 può ottenere la priorità massima nel sistema e quindi essere eseguito: un processo con priorità 127 impiegherebbe poco più di 2 minuti per raggiungere la priorità 0.

Un’altra opzione consiste nel combinare scheduling circolare e scheduling con priorità in modo tale che il sistema esegua il processo con la priorità più alta ed esegua processi con la stessa priorità utilizzando lo scheduling circolare. Si consideri per esempio il seguente insieme di processi, con la durata delle sequenze di operazioni della cpu espressa in millisecondi:
![[Pasted image 20221106174755.png]]
Utilizzando lo scheduling con priorità insieme allo scheduling circolare per processi con uguale priorità, con un quanto di tempo di 2 millisecondi, questi processi sarebbero ordinati secondo il seguente diagramma di Gantt:
![[Pasted image 20221106174845.png]]
In questo esempio, il processo _P_4 ha la priorità più alta e verrà quindi eseguito fino al completamento. Dopo _P_4, i processi _P_2 e _P_3 hanno la priorità maggiore e verranno eseguiti in modalità rr. Si noti che quando il processo _P_2 termina, all’istante 16, il processo _P_3 è il processo con la priorità più alta e verrà quindi eseguito fino al suo completamento. Restano poi i processi _P_1 e _P_5 che, avendo uguale priorità, verranno eseguiti in ordine circolare fino al completamento.