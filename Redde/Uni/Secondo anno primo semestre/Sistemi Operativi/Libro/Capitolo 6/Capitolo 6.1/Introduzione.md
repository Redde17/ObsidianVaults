Abbiamo già visto che i processi possono essere eseguiti in modo concorrente o in parallelo.
Il Paragrafo 3.2.2 ha introdotto il ruolo dello scheduling dei processi e ha descritto come lo scheduler della cpu passi rapidamente da un processo all’altro per offrire un’esecuzione concorrente.
Questo significa che un processo può avere completato solo in parte la sua esecuzione quando viene schedulato un altro processo. In effetti, un processo può essere interrotto in qualsiasi punto del proprio flusso d’esecuzione, assegnando il core di elaborazione all’esecuzione di istruzioni di un altro processo. 
Il Paragrafo 4.2 ha inoltre introdotto l’esecuzione parallela, in cui due flussi di istruzioni (che rappresentano processi differenti) vengono eseguiti contemporaneamente su core distinti. In questo capitolo viene spiegato come l’esecuzione concorrente o parallela possa contribuire a problematiche che riguardano l’integrità dei dati condivisi da più processi.

Prendiamo in considerazione un esempio di come ciò può accadere. Nel Capitolo 3 è stato descritto un modello di sistema costituito da un certo numero di processi sequenziali cooperanti o thread, tutti in esecuzione asincrona e con la possibilità di condividere dati. Tale modello è stato illustrato attraverso l’esempio del produttore/consumatore, che ben rappresenta molte situazioni che riguardano i sistemi operativi. 

Nel Paragrafo 3.5, in particolare, si è descritto come un buffer limitato sia utilizzabile per permettere ai processi la condivisione della memoria.


Torniamo al concetto di buffer limitato.

Com’è stato sottolineato, la nostra soluzione consentiva la presenza contemporanea di non più di BUFFER_SIZE – 1 elementi. 
Si supponga di voler modificare l’algoritmo per rimediare a questa carenza. Una possibilità consiste nell’aggiungere una variabile intera, contatore, inizializzata a 0, che si incrementa ogniqualvolta s’inserisce un nuovo elemento nel buffer e si decrementa ogniqualvolta si preleva un elemento dal buffer. Il codice per il processo produttore si può modificare come segue:

```
while (true) {
	/* produce un elemento in next_produced */
	while (contatore == BUFFER_SIZE)
		; /* non fa niente */
		
	buffer[in] = next_produced;
	in = (in + 1) % BUFFER_SIZE;
	
	contatore++;
}
```

Il codice per il processo consumatore si può modificare come segue:

```
while (true) {
	while (contatore == 0)
		; /* non fa niente */
	
	next_consumed = buffer[out];
	out = (out + 1) % BUFFER_SIZE;
	
	contatore--;
	/* consuma un elemento in next_consumed */
}
```

Sebbene siano corrette se si considerano separatamente, le procedure del produttore e del consumatore possono non funzionare altrettanto correttamente se si eseguono in modo concorrente.
Si supponga per esempio che il valore della variabile contatore sia attualmente 5, e che i processi produttore e consumatore eseguano le istruzioni contatore++ e contatore-- in modo concorrente.
Terminata l’esecuzione delle due istruzioni, il valore della variabile contatore potrebbe essere 4, 5 o 6! Il solo risultato corretto è contatore == 5, che si ottiene se si eseguono separatamente il produttore e il consumatore.

Si può dimostrare che il valore di contatore può essere scorretto: l’istruzione **contatore++** si può codificare in un tipico linguaggio macchina, come
-  _registro_1 := contatore
-  _registro_1 := _registro_1 + 1  
-  contatore := _registro_1
dove _registro_1 è un registro locale della cpu. 

Analogamente, l’istruzione contatore-- si può codificare come
-  _registro_2 := contatore
-  _registro_2 := _registro_2 - 1
-  contatore := _registro_2

dove _registro_2 è un registro locale della cpu.

Anche se _registro_1 e _registro_2 possono essere lo stesso registro fisico, per esempio un accumulatore, occorre ricordare che il contenuto di questo registro viene salvato e recuperato dal gestore dei segnali d’interruzione.

L’esecuzione concorrente delle istruzioni contatore++ e contatore-- equivale a un’esecuzione sequenziale delle istruzioni del linguaggio macchina introdotte precedentemente, intercalate (_interleaved_) in una qualunque sequenza che però conservi l’ordine interno di ogni singola istruzione di alto livello. Una di queste sequenze è
-   _T0: produttore_ esegue _registro1 := contatore {registro1 = 5}
-   _T1: produttore_ esegue _registro1_:= registro_1 + 1 {_registro1 = 6}
-   _T2: consumatore_ esegue _registro2 := contatore {registro2 = 5}
-   _T3: consumatore_  esegue _registro2 := _registro_2 – 1 {registro2 = 4}
-   _T4: produttore_ esegue contatore := _registro_1 {contatore_ = 6}
-   _T5: consumatore_ esegue contatore := _registro_2 {contatore = 4}
e conduce al risultato errato in cui contatore == 4; si registra la presenza di 4 elementi nel buffer, mentre in realtà gli elementi sono 5. Se si invertisse l’ordine delle istruzioni in _T_4 e _T_5 si giungerebbe allo stato errato in cui contatore == 6.

Si è arrivati a questo stato non corretto perché si è permesso a entrambi i processi di manipolare concorrentemente la variabile contatore. Per evitare le situazioni di questo tipo, in cui più processi accedono e modificano gli stessi dati in modo concorrente e i risultati dipendono dall’ordine degli accessi (le cosiddette race condition) occorre assicurare che un solo processo alla volta possa modificare la variabile contatore. Questa garanzia richiede una forma di sincronizzazione dei processi.

Tali situazioni si verificano spesso nei sistemi operativi, nei quali diversi componenti del sistema compiono operazioni su risorse condivise. 
Inoltre, come evidenziato nei precedenti capitoli, la crescente importanza dei sistemi multicore ha dato maggior enfasi allo sviluppo di applicazioni multithread in cui diversi thread, che probabilmente possono condividere dei dati, sono in esecuzione in parallelo su core distinte. 
Ovviamente tali operazioni non devono interferire reciprocamente in modi indesiderati. 

Data l’importanza della questione, la maggior parte di questo capitolo è dedicata ai problemi della sincronizzazione e coordinamento dei processi.