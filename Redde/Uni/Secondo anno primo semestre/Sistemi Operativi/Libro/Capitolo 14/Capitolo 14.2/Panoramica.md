Per realizzare un file system si usano parecchie strutture dati, sia nei dischi sia in memoria. 
Queste strutture variano a seconda del sistema operativo e del file system, ma esistono dei princìpi generali. 
Nei dischi, il file system tiene informazioni su come eseguire l’avviamento di un sistema operativo memorizzato nei dischi stessi, il numero totale di blocchi, il numero e la locazione dei blocchi liberi, la struttura delle directory e i singoli file.
Molte di loro sono analizzate in modo particolareggiato nel seguito di questo capitolo.

Fra le strutture presenti nei dischi ci sono le seguenti.
-   Il **blocco di controllo dell’avviamento** (_boot control block_), 
	per ogni volume, contenente le informazioni necessarie al sistema per l’avviamento di un sistema operativo da quel volume; se il disco non contiene un sistema operativo, tale blocco può essere vuoto. 
	Di solito è il primo blocco di un volume.
	Nell’ufs, si chiama blocco d’avviamento (_boot block_); nell’ntfs, settore d’avviamento della partizione (_partition boot sector_).
	 
-   Il blocco di controllo del volume (_volume control block_); 
	ciascuno di essi contiene i dettagli riguardanti il relativo volume (o partizione), come il numero e la dimensione dei blocchi nella partizione, il contatore dei blocchi liberi e i relativi puntatori, il contatore degli fcb liberi e i relativi puntatori. Nell’ufs si chiama superblocco; nell’ntfs si chiama tabella principale dei file (_master file table_, mft).
	
-   La struttura della directory (una per file system) usata per organizzare i file. 
	Nel caso dell’ufs comprende i nomi dei file e i numeri di inode associati. Nel caso dell’ntfs è memorizzata nella tabella principale dei file (_master file table_).
	
-   Il blocco di controllo del file (fcb),
	contenenti molti dettagli del relativo file. Ha un identificatore unico per poterlo associare a una voce della directory. Nell’ntfs, queste informazioni sono memorizzate all’interno della tabella principale dei file, che si serve di una struttura di base di dati relazionale, con una riga per ciascun file.

Le informazioni tenute in memoria servono sia per la gestione del file system sia per migliorare le prestazioni attraverso l’uso di cache. I dati si caricano al momento del montaggio, si aggiornano mentre si opera sul file system e si eliminano allo smontaggio. Le strutture che vi possono essere incluse sono di diverso tipo:
-   La tabella di montaggio, 
	in memoria, che contiene informazioni relative a ciascun volume montato;
    
-   una cache della struttura della directory, 
	tenuta in memoria, contenente le informazioni relative a tutte le directory cui i processi hanno avuto accesso di recente (per le directory che costituiscono dei punti di montaggio, può essere presente un puntatore alla tabella dei volumi);
    
-   la tabella di sistema dei file aperti, 
	contenente una copia dell’fcb per ciascun file aperto, insieme con altre informazioni;
    
-   la tabella dei file aperti per ciascun processo, 
	contenente un puntatore al corrispondente elemento della tabella generale dei file aperti, insieme con altre informazioni;
    
-   i buffer che conservano blocchi del file system durante la loro lettura o scrittura sul disco.

Le applicazioni, per creare un nuovo file, eseguono una chiamata al file system logico, il quale conosce il formato della struttura della directory. 
Per creare un nuovo file, esso crea un nuovo fcb. (In alternativa, nel caso dei file system che creano tutti gli fcb al momento della loro installazione, esso alloca semplicemente un fcb libero.) 
Il sistema carica quindi la directory appropriata in memoria, la aggiorna con il nome del nuovo file e con l’fcb associato, e la scrive nuovamente sul disco. 
Una tipica struttura di fcb è illustrata nella seguente figura.
![[Pasted image 20221219193040.png]]
Alcuni sistemi operativi, compreso unix, trattano le directory esattamente come i file, distinguendole con un campo per il tipo che indica che si tratta di una directory. Altri, tra cui il sistema operativo Windows, dispongono di chiamate di sistema distinte per i file e le directory e trattano le directory come entità separate dai file.
Indipendentemente da tali questioni strutturali, il file system logico può basarsi sul modulo che si occupa dell’organizzazione dei file per far corrispondere l’i/o su directory ai numeri di blocchi di disco, che poi si passano al file system di base e al sistema per il controllo dell’i/o.