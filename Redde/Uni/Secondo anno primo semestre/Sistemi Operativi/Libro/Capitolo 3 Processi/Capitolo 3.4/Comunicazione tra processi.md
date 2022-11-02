I processi eseguiti concorrentemente nel sistema operativo possono essere **indipendenti** o **cooperanti**.

Un processo è **_indipendente_** se non può influire su altri processi del sistema o subirne l’influsso. Chiaramente, un processo che non condivide dati (temporanei o permanenti) con altri processi è indipendente.

Un processo è **_cooperante_** se influenza o può essere influenzato da altri processi in esecuzione nel sistema. Ovviamente, qualsiasi processo che condivide dati con altri processi è un processo cooperante.

Un ambiente che consente la cooperazione tra processi può essere utile per diverse ragioni.
-   **Condivisione d’informazioni**. Poiché più utenti possono essere interessati alle stesse informazioni (per esempio un file condiviso) è necessario offrire un ambiente che consenta un accesso concorrente a tali risorse.
-   **Velocizzazione del calcolo**. Alcune attività d’elaborazione sono realizzabili più rapidamente se si suddividono in sottoattività eseguibili in parallelo. Un’accelerazione di questo tipo è ottenibile solo se il calcolatore dispone di più core di elaborazione.
-   **Modularità**. Può essere utile la costruzione di un sistema modulare, che suddivida le funzioni di sistema in processi o thread distinti (si veda il Capitolo 2).

Per lo scambio di dati e informazioni i processi cooperanti necessitano di un meccanismo di comunicazione tra processi **(ipc, _interprocess communication_)**_._ I modelli fondamentali della comunicazione tra processi sono due: **a memoria condivisa e a scambio di messaggi.**

Nel modello a memoria condivisa si stabilisce una zona di memoria condivisa dai processi cooperanti, che possono così comunicare scrivendo e leggendo da tale zona. 
![[Pasted image 20221031165100.png]]

Nel modello a scambio di messaggi la comunicazione ha luogo tramite scambio di messaggi tra i processi cooperanti.
![[Pasted image 20221031165113.png]]

Nei sistemi operativi sono diffusi entrambi i modelli; spesso coesistono in un unico sistema. Lo scambio di messaggi è utile per trasmettere piccole quantità di dati, non essendovi bisogno di evitare conflitti. Lo scambio di messaggi è anche più facile da implementare, rispetto alla memoria condivisa, in un sistema distribuito.

La memoria condivisa può essere più veloce dello scambio di messaggi, che è solitamente implementato tramite chiamate di sistema che impegnano il kernel; la memoria condivisa, invece, richiede l’intervento del kernel solo per allocare le regioni di memoria condivisa, dopo di che tutti gli accessi sono gestiti alla stregua di ordinari accessi in memoria che non richiedono l’assistenza del kernel.

Nei Paragrafi [3.5](obsidian://open?vault=Redde&file=Uni%2FSecondo%20anno%20primo%20semestre%2FSistemi%20Operativi%2FLibro%2FCapitolo%203%2FCapitolo%203.5%2FIPC%20in%20sistemi%20a%20memoria%20condivisa) e 3.6 esploriamo i sistemi a memoria condivisa e a scambio di messaggi in modo più dettagliato.