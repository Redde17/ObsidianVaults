Uno dei metodi più semplici per l’allocazione della memoria consiste nel suddividere la stessa in partizioni di dimensione variabile, dove ciascuna partizione può contenere esattamente un processo. 
In questo schema a partizione variabile il sistema operativo conserva una tabella in cui sono indicate le partizioni di memoria disponibili e quelle occupate. Inizialmente tutta la memoria è a disposizione dei processi utenti; si tratta di un grande blocco di memoria disponibile, un buco (_hole_). 
Nel lungo periodo, come si vede nel seguito, la memoria contiene una serie di buchi di diverse dimensioni.

La seguente figura illustra questo schema. Inizialmente, la memoria è completamente utilizzata e contiene i processi 5, 8 e 2. Dopo l’uscita del processo 8 si forma un unico buco. Successivamente, entra in memoria il processo 9, per il quale viene allocata memoria. Quindi il processo 5 viene rimosso, producendo due buchi non contigui.
![[Pasted image 20221130162749.png]]
Quando i processi entrano nel sistema, il sistema operativo prende in considerazione i loro requisiti di memoria e la quantità di spazio di memoria disponibile e determina a quali processi allocare memoria. 
Quando gli viene assegnato dello spazio, un processo viene caricato in memoria e può quindi competere per il controllo della cpu. Quando termina, rilascia la memoria che gli era stata assegnata e il sistema operativo può impiegarla per un altro processo.

Che cosa succede quando non c’è sufficiente memoria per soddisfare le esigenze di un processo in arrivo? Un’opzione semplice è rifiutare il processo e fornire un messaggio di errore appropriato. 
In alternativa, possiamo inserire il processo in una coda di attesa. 
Quando, in seguito, la memoria viene rilasciata, il sistema operativo controlla la coda di attesa per determinare se può soddisfare le richieste di memoria di un processo in attesa.

In generale è sempre presente un insieme di buchi di diverse dimensioni sparsi per la memoria. Quando si presenta un processo che necessita di memoria, il sistema cerca nel gruppo un buco di dimensioni sufficienti per contenerlo. Se è troppo grande, il buco viene diviso in due parti: si assegna una parte al processo in arrivo e si riporta l’altra nell’insieme dei buchi. Quando termina, un processo rilascia il blocco di memoria, che si reinserisce nell’insieme dei buchi; se si trova accanto ad altri buchi, si uniscono tutti i buchi adiacenti per formarne uno più grande.

Questa procedura è una particolare istanza del più generale problema di allocazione dinamica della memoria, che consiste nel soddisfare una richiesta di dimensione _n_ data una lista di buchi liberi. Le soluzioni sono numerose. I criteri più usati per scegliere un buco libero tra quelli disponibili nell’insieme sono i seguenti.
- **First-fit**. Si assegna il _primo_ buco abbastanza grande. La ricerca può cominciare sia dall’inizio dell’insieme di buchi sia dal punto in cui era terminata la ricerca precedente. Si può fermare la ricerca non appena s’individua un buco libero di dimensioni sufficientemente grandi.
    
- **Best-fit**. Si assegna il _più piccolo_ buco in grado di contenere il processo. Si deve compiere la ricerca in tutta la lista, a meno che questa non sia ordinata per dimensione. Tale criterio produce le parti di buco inutilizzate più piccole.
    
- **Worst-fit**. Si assegna il buco _più grande_. Anche in questo caso si deve esaminare tutta la lista, a meno che non sia ordinata per dimensione. Tale criterio produce le parti di buco inutilizzate più grandi, che possono essere più utili delle parti più piccole ottenute col criterio best-fit.
- 
Con l’uso di simulazioni si è dimostrato che sia **first-fit sia best-fit sono migliori rispetto a worst-fit in termini di risparmio di tempo e di utilizzo di memoria**. D’altra parte nessuno dei due è chiaramente migliore dell’altro per quel che riguarda l’utilizzo della memoria ma, in genere, **first-fit è più veloce**.