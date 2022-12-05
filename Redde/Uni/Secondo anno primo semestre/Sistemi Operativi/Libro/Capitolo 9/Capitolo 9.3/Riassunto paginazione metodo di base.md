Bisogna tenere conto che quando si parla di memoria si tiene in considerazione la memoria volatile /RAM di un elaboratore.

Per realizzare la paginazione con il metodo di base dividiamo la memoria in fisica e logica secondo i seguenti criteri:
La **memoria fisica** viene suddivisa in **frame** ovvero blocchi di dimensione fissa.
La **memoria logica** viene suddivisa in **pagine** ovvero blocchi di pari dimensioni.

Quando si deve eseguire un processo le sue **pagine** vengono caricate in memoria nei **frame** liberi.
Le pagine risiedono nella memoria ausiliare o nel file system.
La memoria ausiliare é a sua volta divisa in blocchi di dimensione fissa

Questa metodologia di gestione della memoria permette di separare gli indirizzi logici da quelli fisici e permettere ad esempio, ad un processo di avere uno spazio degli indirizzi logici a 64 bit nonostante il sistema ha meno di $2^{64}$.  

Ogni inidirizzo logico generato dalla CPU é diviso in due parti, un numero di pagina e un offset di pagina.

Il numero di pagina indica il frame da reperire mentre l'offset di pagina indica da dove iniziare a leggere la memoria.

Per la generazione dell'indirizzo fisico, viene preso il numero di pagina, che svolge la funzione da indice nella tabella delle pagine inerenti al processo e viene tradotto nel frame al quale si vuole accedere, questo dato viene unito insieme all'offset per indicare precisamente all'informazione neccessaria.
![[Pasted image 20221130164727.png]]
![[Pasted image 20221130164829.png]]

La traduzione avviene tramie la MMU o Memory Managment Unit che svolge i seguenti passaggi per convertire un indirizzo logico ad un fisico:
1. Estrae il numero di pagina per utilizzarlo come indice nella tabella delle pagine
2. Estrarre il numero del frame corrispondente dalla tabella delle pagine 
3. Sostituire il numero di pagina nell'indirizzo logico con il numero di frame
L' offset non cambia e pertanto non viene sostituito. Quindi il numero del frame e l'offset combinati formano un indirizzo fisico.

La dimensione di una pagina viene generalmente definita dall'hardaware ed é in genere un potenza di 2. 
La motivazione per la potenza di 2 risiede nella facilitá di traduzione di un indirizzo logico
non so perché non riesco a capirlo.

Con la paginazione viene eliminata la frammentazione esterna ma rimane ancora quella interna poiché un processo potrebbe richiedere una quantitá di memoria che é minore di quella offerte dalle pagine impiegate.
Es. un processo che occupa 72.766 byte in un sistema con pagine da 2048 byte occupera 35 pagine piú 1086 byte, quindi si assegnano 36 pagine e nell'ultima pagina rimangono vuoti 962 byte.
Il caso peggiore che si puó avere é una pagina con un singolo byte occupato.

La dimensione delle pagina va evaluata a seconda della macchina poiché una dimensione troppo piccola diminuiribbe la presenza di frammentazione interna ma aumenterebbe l'overhead, quindi pagine di dimensioni maggiori aumenterebbero le prestazioni.

La paginazione consente di utilizzare una memoria fisica decisamente piú grande di quella che potrebbe essere indirizzata dalla lunghezza del puntutatore agli indirizzi della cpu.
Questo é dato dal fatto che una voce nella tabella delle pagine é lunga 4 byte, nonostante questo valore possa variare, una singola voce da 32 bit puó puntare a uno dei $2^{32}$ frame di pagina fisici.
Se la dimensione di un frame é di 4 kb ($2^{12}$), un sistema con voci della tabella delle pagine di 4 byte può indirizzare $2^{44}$ byte (o 16 tb) di memoria fisica.

Quando si deve eseguire un nuovo processo il sistema esamina la sua dimensione espressa in pagine. Poiché ogni pagina necessitá di un frame, la quantitá di pagine che un processo necessitá deve essere disponibile in frame in memoria.
Il caricamento delle pagine dei frame avviene prima svolgendo l'effettivo caricamento della pagina nel frame e poi si inserisce il numero del frame nella tabella delle pagine relative al processo. Si svolge questa azione per tutte le pagine da caricare.
![[Pasted image 20221205183632.png]]

Utilizzando la paginazione il programmatore vede la memoria di un processo come un blocco di memoria contigua quando in veritá é sparsa per la memoria insieme ad altri programmi.
Si noti che un processo utente non puó accedere alla memoria di altri processi.

Poiché il sistema operativo gestisce la memoria fisica, deve essere informato dei dettagli della allocazione: quali frame sono assegnati, quali sono disponibili, il loro numero totale, e così via. In genere queste informazioni sono contenute in una struttura dati chiamata tabella dei frame, contenente un elemento per ogni frame, indicante se sia libero oppure assegnato e, se è assegnato, a quale pagina di quale processo o di quali processi.

Inoltre, il sistema operativo deve sapere che i processi utenti operano nello spazio utente, e tutti gli indirizzi logici si devono far corrispondere a indirizzi fisici. Se un utente usa una chiamata di sistema (per esempio per eseguire un’operazione di i/o) e fornisce un indirizzo come parametro (per esempio l’indirizzo di un buffer), si deve tradurre questo indirizzo nell’indirizzo fisico corretto.