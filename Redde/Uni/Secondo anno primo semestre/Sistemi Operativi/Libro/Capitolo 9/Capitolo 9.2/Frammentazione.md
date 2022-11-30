Entrambi i criteri first-fit e best-fit di allocazione della memoria soffrono di frammentazione esterna. 
Caricando e rimuovendo i processi dalla memoria, si frammenta lo spazio libero della memoria in tante piccole parti. Si ha la frammentazione esterna se lo spazio di memoria totale è sufficiente per soddisfare una richiesta, ma non è contiguo; la memoria è frammentata in tanti piccoli buchi. Questo problema di frammentazione può essere molto grave; nel caso peggiore può verificarsi un blocco di memoria libera, sprecata, tra ogni coppia di processi. Se tutti questi piccoli pezzi di memoria costituissero in un unico blocco libero di grandi dimensioni, si potrebbero eseguire molti più processi.

Sia che si adotti l’uno o l’altro, l’impiego di un determinato criterio può influire sulla quantità di frammentazione: in alcuni sistemi dà migliori risultati il first-fit, in altri dà migliori risultati il best-fit; un altro elemento rilevante è quale sia l’estremità assegnata di un blocco libero (se la parte inutilizzata è quella in alto o quella in basso). 
**A prescindere dal tipo di algoritmo usato, la frammentazione esterna è un problema**.

La sua gravità dipende dalla quantità totale di memoria e dalla dimensione media dei processi. L’analisi statistica dell’algoritmo first-fit, per esempio, rivela che, pur con alcune ottimizzazioni, per _n_ blocchi assegnati, si perdono altri 0,5 _n_ blocchi a causa della frammentazione, ciò significa che potrebbe essere inutilizzabile un terzo della memoria. Questa caratteristica è nota come regola del 50 per cento.

La frammentazione può essere interna oltre che esterna. Si consideri uno schema a partizioni multiple con un buco di 18.464 byte. Supponendo che il processo successivo richieda 18.462 byte, assegnando esattamente il blocco richiesto rimane un buco di 2 byte. L’overhead necessario per tener traccia di questo buco è nettamente più grande del buco stesso. 
Il metodo generale per superare questo problema prevede di suddividere la memoria fisica in blocchi di dimensione fissa, che costituiscono le unità d’allocazione. 
Con questo metodo la memoria assegnata può essere leggermente maggiore della memoria richiesta. La differenza tra questi due numeri è la frammentazione interna che consiste nella memoria inutilizzata all’interno di una partizione.

Una soluzione al problema della frammentazione esterna è data dalla **compattazione**. Lo scopo è quello di riordinare il contenuto della memoria per riunire la memoria libera in un unico grosso blocco. 
La compattazione tuttavia non è sempre possibile: non si può realizzare se la rilocazione è statica ed è effettuata nella fase di assemblaggio o di caricamento; è possibile solo se la rilocazione è dinamica e si effettua nella fase d’esecuzione. 
Se gli indirizzi sono rilocati dinamicamente, la rilocazione richiede solo lo spostamento del programma e dei dati, e quindi la modifica del registro di rilocazione in modo che rifletta il nuovo indirizzo di base. 
Quando è possibile eseguire la compattazione, è necessario determinarne il costo. Il più semplice algoritmo di compattazione consiste nello spostare tutti i processi verso un’estremità della memoria: tutti i buchi si spostano nell’altra direzione formando un grosso buco di memoria. Questo metodo può essere assai oneroso.

Un’altra possibile soluzione del problema della frammentazione esterna è data dal consentire la non contiguità dello spazio degli indirizzi logici di un processo, permettendo così di assegnare la memoria fisica ai processi dovunque essa sia disponibile. 
Questa è la strategia utilizzata nella paginazione, la più comune tecnica di gestione della memoria nei sistemi elaborativi. 