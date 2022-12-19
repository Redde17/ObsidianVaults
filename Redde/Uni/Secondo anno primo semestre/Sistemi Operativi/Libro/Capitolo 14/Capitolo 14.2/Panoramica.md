Per realizzare un file system si usano parecchie strutture dati, sia nei dischi sia in memoria. 
Queste strutture variano a seconda del sistema operativo e del file system, ma esistono dei princìpi generali. 
Nei dischi, il file system tiene informazioni su come eseguire l’avviamento di un sistema operativo memorizzato nei dischi stessi, il numero totale di blocchi, il numero e la locazione dei blocchi liberi, la struttura delle directory e i singoli file.
Molte di loro sono analizzate in modo particolareggiato nel seguito di questo capitolo.

Fra le strutture presenti nei dischi ci sono le seguenti.
-   Il **blocco di controllo dell’avviamento** (_boot control block_), 
	per ogni volume, contenente le informazioni necessarie al sistema per l’avviamento di un sistema operativo da quel volume; se il disco non contiene un sistema operativo, tale blocco può essere vuoto. Di solito è il primo blocco di un volume.
	 Nell’ufs, si chiama blocco d’avviamento (_boot block_); nell’ntfs, settore d’avviamento della partizione (_partition boot sector_).
	 
-   Il blocco di controllo del volume (_volume control block_); 
	ciascuno di essi contiene i dettagli riguardanti il relativo volume (o partizione), come il numero e la dimensione dei blocchi nella partizione, il contatore dei blocchi liberi e i relativi puntatori, il contatore degli fcb liberi e i relativi puntatori. Nell’ufs si chiama superblocco; nell’ntfs si chiama tabella principale dei file (_master file table_, mft).