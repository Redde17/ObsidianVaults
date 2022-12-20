L’allocazione concatenata risolve tutti i problemi dell’allocazione contigua. Con questo tipo di allocazione, infatti, ogni file è composto da una lista concatenata di blocchi del disco i quali possono essere sparsi in qualsiasi punto del disco stesso. La directory contiene un puntatore al primo e all’ultimo blocco del file. Per esempio, un file di cinque blocchi può cominciare dal blocco 9, continuare al blocco 16, quindi al blocco 1, al blocco 10 e infine terminare al blocco 25.
Ogni blocco contiene un puntatore al blocco successivo. Questi puntatori non sono disponibili all’utente, quindi se ogni blocco è formato di 512 byte e un indirizzo del disco (il puntatore) richiede 4 byte, l’utente vede blocchi di 508 byte.
![[Pasted image 20221220141509.png]]

Per creare un nuovo file si crea semplicemente un nuovo elemento nella directory. 
Con l’allocazione concatenata, ogni elemento della directory ha un puntatore al primo blocco del file. 
Questo puntatore s’inizializza a null (valore del puntatore di fine lista) a indicare un file vuoto; anche il campo della dimensione s’imposta a 0. 
Un’operazione di scrittura nel file determina la ricerca di un blocco libero attraverso il sistema di gestione dello spazio libero, la scrittura in tale blocco, e la concatenazione di tale blocco alla fine del file. 
Per leggere un file occorre semplicemente leggere i blocchi seguendo i puntatori da un blocco all’altro. 
Con l’allocazione concatenata non esiste frammentazione esterna e per soddisfare una richiesta si può usare qualsiasi blocco libero della lista. Inoltre non è necessario dichiarare la dimensione di un file al momento della sua creazione. Un file può continuare a crescere finché sono disponibili blocchi liberi, di conseguenza non è mai necessario compattare lo spazio del disco.

L’allocazione concatenata presenta comunque alcuni svantaggi. 
Il problema principale riguarda il fatto che può essere usata in modo efficiente solo per i file ad accesso sequenziale. 
Per trovare l’_i_-esimo blocco di un file occorre partire dall’inizio del file e seguire i puntatori finché non si raggiunge l’_i_-esimo blocco. Ogni accesso a un puntatore implica una lettura del disco, e talvolta un posizionamento della testina. Di conseguenza, per file il cui spazio è assegnato in modo concatenato, la funzione d’accesso diretto è inefficiente.

Un altro svantaggio dell’allocazione concatenata riguarda lo spazio richiesto per i puntatori. Se un puntatore richiede 4 byte di un blocco di 512 byte, allora lo 0,78 per cento del disco è usato per i puntatori anziché per le informazioni: ogni file richiede un po’ più spazio di quanto ne richiederebbe altrimenti.


