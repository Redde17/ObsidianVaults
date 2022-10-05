>Definizione e notazioner di memoria
>L’unità di memorizzazione di base di un computer è il **bit**. Un bit può assumere uno tra i due valori 0 e 1. Tutto ciò che viene memorizzato su un computer è formato da una collezione di bit.
>
>Un **byte** è formato da 8 bit e nella maggior parte dei calcolatori è la più piccola unità di memorizzazione utile. Ad esempio, la maggior parte dei computer non dispone di un’istruzione per spostare un singolo bit, ma ne possiede una per spostare un byte.
>
>Una nozione meno comune è quella di **parola** (_word_), l’unità di memorizzazione nativa di una data architettura. Una parola è costituita da uno o più byte. Ad esempio, un computer con registri di 64 bit e indirizzamento della memoria a 64 bit ha di solito parole di 64 bit (8 byte). Un computer esegue diverse operazioni utilizzando la dimensione di parola nativa, piuttosto che un byte alla volta.
>
>La memoria di un computer, come molti altri suoi parametri, è generalmente misurata e manipolata in byte o gruppi di byte
>Le misure relative alle reti costituiscono un’eccezione a queste regole generali e vengono espresse in bit (perché le reti spostano i dati un bit alla volta).
------------------
## Struttura della memoria
La cpu può caricare istruzioni **esclusivamente** dalla memoria, quindi tutti i programmi da eseguire devono esservi caricati. 
I computer general-purpose eseguono la maggior parte dei programmi da una memoria riscrivibile, la memoria principale, chiamata anche **memoria ad accesso casuale (_random access memory_, RAM)**.
La memoria principale è realizzata solitamente con una tecnologia basata su semiconduttori chiamata memoria dinamica ad accesso casuale (_dynamic random access memory_, dram).

I computer utilizzano anche altri tipi di memoria. Per esempio, il primo programma che viene eseguito all’avvio di un computer è il programma di avviamento (_bootstrap_), che si occupa di caricare il sistema operativo. Visto che la ram è volatile, essa non può essere utilizzata per il programma di bootstrap. Al suo posto i computer utilizzano una memoria di sola lettura elettricamente cancellabile e programmabile (eeprom) e altre forme di archiviazione del firmware che vengono riscritte raramente e che non sono volatili.
>Le eeprom sono modificabili ma non di frequente, inoltre sono lente.

Tutte le tipologie di memoria forniscono un vettore di byte. Ciascun byte possiede un proprio indirizzo. 
L’interazione avviene per mezzo di una sequenza di istruzioni **load** e **store** opportunamente indirizzate. 
	**L’istruzione load** trasferisce il contenuto di un byte o una parola della memoria centrale in uno dei registri interni della cpu.
	**L’istruzione store** copia il contenuto di uno di questi registri nella locazione di memoria specificata. 
Oltre agli accessi espliciti, tramite load e store, la cpu preleva automaticamente dalla memoria centrale, alla locazione di memoria contenuta nel contatore di programma, le istruzioni da eseguire.

La tipica sequenza d’esecuzione di un’istruzione, in un sistema con architettura di von Neumann, comincia con il **prelievo (_fetch_)** di un’istruzione dalla memoria centrale e il suo trasferimento nel registro d’istruzione. 
Quindi si decodifica l’istruzione che eventualmente può richiedere il trasferimento di alcuni operandi dalla memoria in alcuni registri interni. Una volta terminata l’esecuzione dell’istruzione sugli operandi, il risultato si può scrivere nella memoria. 
>L’unità di memoria “vede” soltanto un flusso di indirizzi di memoria; non importa né il modo in cui questi sono stati generati né a che cosa fanno riferimento.

