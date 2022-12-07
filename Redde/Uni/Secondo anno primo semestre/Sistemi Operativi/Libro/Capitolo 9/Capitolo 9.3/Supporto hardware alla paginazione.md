Poiché ogni processo ha la sua tabella delle pagine, un puntatore alla tabella di pagina viene memorizzato insieme ai valori di altri registri nel **_process control block_** di ciascun processo.
Quando lo scheduler della cpu seleziona un processo per l’esecuzione, deve ricaricare i registri utente e i valori appropriati della tabella delle pagine hardware dalla tabella delle pagine utente memorizzata.

L’implementazione hardware della tabella delle pagine si può realizzare in modi diversi. Nel caso più semplice è implementata come un insieme di registri hardware dedicati ad alta velocità, così da rendere la traduzione dell’indirizzo molto efficiente. Tuttavia, questo approccio aumenta il tempo dei cambi di contesto, poiché durante un cambio di contesto ogni registro dovrà essere scambiato.

L’uso di registri per la tabella delle pagine è efficiente se la tabella stessa è ragionevolmente piccola, nell’ordine, per esempio, di 256 elementi. 
Però la maggior parte dei calcolatori contemporanei usa tabelle molto grandi, per esempio di un milione di elementi.
Quindi **non si possono impiegare i registri veloci per realizzare la tabella delle pagine**; quest’ultima viene invece mantenuta nella memoria principale e un registro di base della tabella delle pagine (_page-table base register_, ptbr) punta alla tabella stessa. 
Il cambio della tabelle delle pagine richiede soltanto di modificare questo registro, riducendo considerevolmente il tempo dei cambi di contesto.

#### **Riassuntino**
Visto che ogni processo ha la sua tabella delle pagine essa viene aggiunta nel process block di un processo.
Per implementare la tabella delle pagine si puó pensare di utilizzare una memoria veloce ma ció renderebbe i tempi di context switch troppo elevati.
Per rimediare a questo problema la tabella delle pagine rimane in memoria principale e viene caricato nel registro di base solo un puntatore alla tabella.


-----

## TLB
La memorizzazione della tabella delle pagine nella memoria principale può favorire cambi di **contesto più rapidi,** ma può anche comportare **tempi di accesso alla memoria più lenti**.

Poiché per reperire le informazioni sulla posizione di un dato bisogna leggere la memoria e poi per reperire il dato bisogna eseguire un altra lettura, questo significa raddoppiare le letture svolte in memoria per recuperare un dato.

La soluzione tipica a questo problema consiste nell’impiego del **tlb** (_translation look-aside buffer_), una speciale, piccola cache hardware.
Il **tlb** è una memoria associativa ad alta velocità in cui ogni elemento consiste di due parti: una chiave (o _tag_) e un valore.

Quando si presenta un elemento, la memoria associativa lo confronta contemporaneamente con tutte le chiavi; se trova una corrispondenza, riporta il valore correlato. 
La ricerca è molto rapida e in un hardware moderno è parte della pipeline delle istruzioni: non induce dunque nessuna penalizzazione in termini di prestazioni.

Per poter eseguire la ricerca in uno stadio della pipeline, tuttavia, il tlb deve essere di dimensioni ridotte, in genere contenute tra le 32 e le 1.024 voci. 
Alcune cpu implementano tlb separate per istruzioni e dati, in modo da poter raddoppiare il numero di voci tlb disponibili, poiché le due ricerche vengono effettuate in diversi stadi della pipeline. 
Questo sviluppo rappresenta un esempio di evoluzione della tecnologia delle cpu: i sistemi si sono evoluti passando dall’assenza di tlb fino ad avere più livelli di tlb, proprio come nel caso delle cache.

Il tlb si usa insieme con le tabelle delle pagine nel modo seguente: 
il tlb contiene una piccola parte degli elementi della tabella delle pagine; quando la cpu genera un indirizzo logico, si presenta il suo numero di pagina al tlb; **se tale numero è presente**, il corrispondente numero del frame è immediatamente disponibile e si usa per accedere alla memoria. 

Come abbiamo appena menzionato, queste operazioni vengono eseguite come parte della pipeline delle istruzioni all’interno della cpu, senza penalizzare il sistema rispetto ad altri sistemi che non implementano la paginazione.

**Se nel tlb non è presente il numero di pagina**, situazione nota come insuccesso del tlb (_tlb_ _miss_), si deve consultare la tabella delle pagine in memoria.
A seconda della cpu, questa operazione può essere effettuata automaticamente a livello hardware oppure per mezzo di un interrupt al sistema operativo.
Il numero del frame così ottenuto viene usato per accedere alla memoria. 
Inoltre, i numeri della pagina e del frame vengono inseriti nel tlb, e al riferimento successivo la ricerca sarà molto più rapida.
![[Pasted image 20221207171521.png]]

