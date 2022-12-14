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

Idealmente si vorrebbe che sia i programmi sia i dati da essi trattati risiedessero in modo permanente nella memoria centrale. 
Questo non è possibile per i seguenti due motivi:
1. La capacità della memoria centrale non è di solito sufficiente a contenere in modo permanente tutti i programmi e i dati richiesti;
2. La memoria centrale è un dispositivo di memorizzazione _volatile_, che perde il proprio contenuto quando l’alimentazione elettrica viene spenta o si interrompe.
Per queste ragioni la maggior parte dei sistemi elaborativi comprende una **memoria secondaria** come estensione della memoria centrale. 
La caratteristica fondamentale di questi dispositivi è la capacità di conservare in modo permanente grandi quantità di informazioni.

I dispositivi più comunemente impiegati a questo scopo sono **il disco magnetico (_hard-disk drive_, hdd) e i dispositivi di memoria non volatile (nvm)**.
 Molti programmi fanno uso del disco come sorgente e destinazione delle informazioni elaborate. Quindi, una corretta gestione delle unità a disco è di fondamentale importanza per un sistema elaborativo.
*(Altri tipi di memoria possono essere, cache, cd-rom, blu-ray e nastri magnetici)*

![[Pasted image 20221006082413.png]]
La memoria viene gerarchizzata in base a dimensione e velocità di accesso, più si sale più la memoria è veloce ma di minore dimensione.

Dal momento che la memorizzazione gioca un ruolo importante nella struttura del sistema operativo useremo la seguente terminologia.
- **La memoria volatile** verrà indicata semplicemente come **memoria**. Se sarà necessario enfatizzare un particolare tipo di dispositivo di memorizzazione (per esempio un registro), lo faremo esplicitamente.
- **La memoria non volatile**, che indicheremo con l’acronimo **nvs** (_nonvolatile storage_), conserva il suo contenuto quando viene persa l’alimentazione. La maggior parte del tempo che dedicheremo a nvs riguarderà la memoria secondaria, classificabile in due diverse tipologie:
	- **Meccanica**. Alcuni esempi di tali sistemi di memorizzazione sono gli hdd, i dischi ottici, la memoria olografica e il nastro magnetico.
	- **Elettrica**. Alcuni esempi di tali sistemi di archiviazione sono la memoria flash, la fram, la nram e gli ssd. La memoria elettrica verrà indicata come nvm.
