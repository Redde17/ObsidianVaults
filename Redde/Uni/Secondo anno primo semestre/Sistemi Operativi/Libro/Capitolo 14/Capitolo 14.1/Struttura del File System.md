I dischi costituiscono la maggior parte della memoria secondaria in cui si conservano i file system. Hanno due caratteristiche importanti che ne fanno un mezzo adatto a questo scopo:
1.  si possono riscrivere localmente; si può leggere un blocco dal disco, modificarlo e quindi scriverlo nella stessa posizione;
2.  è possibile accedere direttamente a qualsiasi blocco di informazioni del disco, quindi risulta semplice accedere a qualsiasi file, sia in modo sequenziale sia in modo diretto, e passare da un file all’altro spostando le testine di lettura e scrittura e attendendo la rotazione del disco.

I dispositivi nvm sono sempre più utilizzati per l’archiviazione dei file e su di essi vengono quindi creati dei file system.
Questi dispositivi differiscono dagli hard disk, in quanto non possono essere riscritti direttamente e presentano differenti performance.

Per migliorare l’efficienza dell’i/o, i trasferimenti tra memoria centrale e dischi si eseguono per blocchi. Ciascun blocco è composto da uno o più settori. A seconda dell’unità a disco, la dimensione dei settori è compresa tra 32 byte e 4096 byte; di solito è pari a 512 byte o 4096 byte. I dispositivi nvm hanno normalmente blocchi di 4096 byte e utilizzano metodi di trasferimento simili a quelli delle unità disco.

Per fornire un efficiente e conveniente accesso al disco, il sistema operativo fa uso di uno o più file system che consentono di memorizzare, individuare e recuperare facilmente i dati. 
Un file system presenta due problemi di progettazione molto diversi.
Il primo riguarda la definizione dell’aspetto del file system agli occhi dell’utente. Questo compito implica la definizione di un file e dei suoi attributi, delle operazioni permesse su un file e della struttura delle directory per l’organizzazione dei file. 
Il secondo riguarda la creazione di algoritmi e strutture dati che permettano di far corrispondere il file system logico ai dispositivi fisici di memoria secondaria.

Lo stesso file system è generalmente composto da molti livelli distinti. La struttura illustrata nella seguente figura è un esempio di struttura stratificata. Ogni livello si serve delle funzioni dei livelli inferiori per crearne di nuove impiegate dai livelli superiori.
![[Pasted image 20221219190559.png]]

- Il livello più basso, **il controllo dell’i/o**,
	costituito dai driver dei dispositivi e dai gestori dei segnali d’interruzione, si occupa del trasferimento delle informazioni tra memoria centrale e memoria secondaria. Un driver di dispositivo si può concepire come un traduttore che riceva comandi ad alto livello, come “recupera il blocco 123”, e che emette istruzioni di basso livello dipendenti dall’hardware, usate dal controllore che fa da interfaccia tra i dispositivi di i/o e il resto del sistema. Un driver di dispositivo di solito scrive specifiche configurazioni di bit in specifiche locazioni della memoria del controllore di i/o per indicare quali azioni il dispositivo di i/o debba compiere, e su quali locazioni.
	
- Il **file system di base**
	deve soltanto inviare dei generici comandi all’appropriato driver di dispositivo per leggere e scrivere blocchi fisici nel disco. Ogni blocco fisico si identifica col suo indirizzo numerico nel disco, per esempio unità 1, cilindro 73, traccia 2, settore 10. Questo strato gestisce inoltre buffer di memoria e le cache che conservano vari blocchi dei file system, delle directory e dei dati. Un blocco viene allocato nel buffer prima che possa verificarsi il trasferimento di un blocco del disco. Quando il buffer è pieno, il gestore del buffer deve recuperare più spazio di memoria per il buffer oppure deve liberare spazio nel buffer per permettere il completamento di un i/o richiesto. Le cache servono a conservare i metadati del file system usati frequentemente, in modo da migliorare le prestazioni. La gestione dei loro contenuti è quindi un punto critico per conseguire prestazioni ottimali del sistema.
	
- **Il modulo di organizzazione dei file** 
	è a conoscenza dei file e dei loro blocchi logici, così come dei blocchi fisici dei dischi. Conoscendo il tipo di allocazione dei file usato e la locazione dei file, può tradurre gli indirizzi dei blocchi logici negli indirizzi dei blocchi fisici che il file system di base deve trasferire. Il modulo di organizzazione dei file comprende anche il gestore dello spazio libero, che registra i blocchi non assegnati e li mette a disposizione del modulo di organizzazione dei file quando sono richiesti.
	
- Infine, il file system logico
	gestisce i metadati; si tratta di tutte le strutture del file system, eccetto gli effettivi dati (il contenuto dei file). 
	Il file system logico gestisce la struttura della directory per fornire al modulo di organizzazione dei file le informazioni di cui necessita, dato un nome simbolico di file. Mantiene le strutture di file tramite i blocchi di controllo dei file (_file control block_, fcb), detti inode nei file system unix, contenenti informazioni sui file, come la proprietà, i permessi, e la posizione del contenuto del file.

Nei file system stratificati la duplicazione di codice è ridotta al minimo. 
Il controllo dell’i/o e, talvolta, il codice di base del file system, possono essere utilizzati da più di un file system. 
Ogni file system ha poi i propri moduli che gestiscono il file system logico e l’organizzazione dei file. Sfortunatamente, la stratificazione può comportare un maggior overhead del sistema operativo, che può generare un conseguente decadimento delle prestazioni. 
L’utilizzo della stratificazione e le scelte sul numero di strati da impiegare e sulle loro funzionalità rappresentano una grande sfida per la progettazione di nuovi sistemi.

Esistono svariati tipi di file system al giorno d’oggi, e non è raro che i sistemi operativi ne prevedano più d’uno. Molti cd-rom, a esempio, sono scritti nel formato iso 9660, uno standard concordato dai produttori di cd-rom. Oltre ai file system dei supporti rimovibili, ciascun sistema operativo possiede un file system, o più di uno, basato sui dischi_._ unix adotta il file system unix (ufs), che si fonda a sua volta sul Berkeley Fast File System (ffs). Windows adotta i formati fat, fat32 e ntfs (o File System di Windows nt), così come i formati per cd-rom e dvd. Sebbene Linux possa funzionare con più di quaranta file system diversi, quello standard è noto come file system esteso, le cui versioni maggiormente diffuse sono ext2 ed ext3. Esistono anche file system distribuiti, in cui un file system su server è montato da uno o più client in una rete.

La ricerca relativa ai file system continua a essere un’area attiva della progettazione e dell’implementazione dei sistemi operativi. Per soddisfare esigenze di memorizzazione e recupero dati specifiche dell’azienda, Google ha progettato un proprio file system che permette un accesso ad alte prestazioni a un gran numero di dischi da parte di numerosi client. Un altro progetto interessante è fuse, che garantisce flessibilità nello sviluppo e nell’utilizzo del file system grazie all’implementazione e all’esecuzione di file system a livello utente invece che a livello del codice del kernel. Gli utenti di fuse possono aggiungere nuovi file system a numerosi sistemi operativi e utilizzarli per gestire i propri file.