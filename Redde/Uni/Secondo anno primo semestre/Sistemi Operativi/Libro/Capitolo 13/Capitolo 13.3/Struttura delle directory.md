La directory si può considerare come una tabella di simboli che traduce i nomi dei file negli elementi in essa contenuti.
Considerando questo punto di vista, si capisce che la stessa directory si può organizzare in molti modi diversi; l’organizzazione deve rendere possibile l’inserimento di nuovi elementi, la cancellazione di elementi esistenti, la ricerca di un elemento, e l’elenco di tutti gli elementi della directory. In questo paragrafo esaminiamo diversi schemi per definire la struttura logica del sistema di directory. 
Nel considerare una particolare struttura della directory si deve tenere presente l’insieme delle seguenti operazioni che si possono eseguire su una directory.

-   Ricerca di un file. 
	Deve esserci la possibilità di scorrere una directory per individuare l’elemento associato a un particolare file. Poiché i file possono avere nomi simbolici, e poiché nomi simili possono indicare relazioni tra file, deve esistere la possibilità di trovare tutti i file il cui nome soddisfi una particolare espressione.
    
-   Creazione di un file. 
	Deve essere possibile creare nuovi file e aggiungerli alla directory.
    
-   Cancellazione di un file. 
	Quando non serve più, si deve poter rimuovere un file dalla directory.
    
-   Elencazione di una directory. '
	Deve esistere la possibilità di elencare tutti i file di una directory, e il contenuto degli elementi della directory associati a ciascun file nell’elenco.
    
-   Ridenominazione di un file. 
	Poiché il nome di un file rappresenta per i suoi utenti il contenuto del file, questo nome deve poter essere modificato quando il contenuto o l’uso del file subiscono cambiamenti. La ridenominazione di un file potrebbe anche permettere la variazione della posizione del file nella directory.
    
-   Attraversamento del file system. 
	Si potrebbe voler accedere a ogni directory e a ciascun file contenuto in una directory. Per motivi di affidabilità, è opportuno salvare il contenuto e la struttura dell’intero file system a intervalli regolari. Questo salvataggio consiste nella copiatura di tutti i file in un nastro magnetico; tale tecnica consente di avere una copia di riserva (_backup_) che sarebbe utile nel caso in cui si dovesse verificare un guasto nel sistema. Inoltre, se un file non è più in uso, si può copiarlo su nastro e liberare lo spazio da esso occupato nel disco, rendendolo riutilizzabile per altri file.

### 13.3.3 [[Directory con struttura ad albero]]
### 13.3.4 [[Directory con struttura a grafo aciclico]]
### 13.3.5 [[Directory con struttura a grafo generale]]