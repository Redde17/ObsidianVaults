## Categorie di chiamate di sistema

Le chiamate di sistema sono classificabili approssimativamente in sei categorie principali:
- **controllo dei processi**
	- creazione e arresto di un processo
	- caricamento, esecuzione
	- terminazione normale e anormale
	- esame e impostazione degli attributi di un processo
	- attesa per il tempo indicato
	- attesa e segnalazione di un evento
	- assegnazione e rilascio di memoria
- **gestione dei file**
	- creazione e cancellaione di file
	- apertura, chiusura
	- lettura, scrittura, posizionamento
	- esame e impostazione degli attributi di un file
- **gestione dei dispositivi**
	- richiesta e rilascio di un dispositivo
	- lettura, scrittura, posizionamento
	- esame e impostazione degli attributi di un dispositivo
	- inserimento logico ed esclusione logica di un dispositivo
- **gestione delle informazioni**
	- esame e impostazione dell'ora e della data
	- esame e impostazione dei dati del sistema
- **comunicazioni**
- **protezione**


### Controllo dei processi
Un sistema operativo puó mettere a disposizione ad un processo diverse chiamate per il controllo del sistema. 
Un programma puó fermarsi in modo sia normale **end()** sia in modo anomalo **abort()**.
Per le fermate anomale il programma puó anche fare una copia dell'errore in un file (dump) e tramite programmi di debug si puó arrivare all'errore che ha causato l'interruzione anomale.
Un processo che esegue un programma puó richiedere di caricare ed eseguire un altro programma (**load()** ed **execute()**).
 In questo modo l’interprete dei comandi esegue un programma in seguito a una richiesta impartita, per esempio, da un comando utente, oppure dal clic di un mouse o da un comando batch. È interessante chiedersi dove si debba restituire il controllo una volta terminato il programma caricato. La questione è legata alle eventualità che il programma attuale sia terminato, sia stato sospeso oppure che abbia continuato l’esecuzione in modo concorrente con il nuovo programma.

Se al termine del nuovo programma il controllo rientra nel programma attuale, si deve salvare l’immagine della memoria del programma attuale, creando così effettivamente un meccanismo con cui un programma può richiamare un altro programma. Se entrambi i programmi continuano l’esecuzione in modo concorrente, si è creato un nuovo processo da eseguire in multiprogrammazione. A questo scopo spesso si ha una chiamata di sistema specifica (**create_process()**).

Quando si crea un nuovo processo, o anche un insieme di processi, è necessario mantenerne il controllo; ciò richiede la capacità di determinare e reimpostare gli attributi di un processo, compresi la sua priorità, il suo tempo massimo d’esecuzione e così via (**get_process_attributes()** e **set_process_attributes()**). Inoltre, può essere necessario terminare un processo creato, se si riscontra che non è corretto o se la sua esecuzione non è più utile (**terminate_process()**).

Una volta creati, può essere necessario attendere che i processi terminino la loro esecuzione. Quest’attesa si può impostare per un certo periodo di tempo (**wait_time()**), ma è più probabile che si preferisca attendere che si verifichi un dato evento (**wait_event()**). In tal caso i processi devono segnalare il verificarsi di quell’evento (**signal_event()**).


=======
Le chiamate di sistema (_system call_) costituiscono un’interfaccia per i servizi resi disponibili dal sistema operativo. Tali chiamate sono generalmente disponibili sotto forma di routine scritte in c o c++, sebbene per alcuni compiti di basso livello, come quelli che comportano un accesso diretto all’hardware, possa essere necessario il ricorso al linguaggio assembly.

## API
Anche programmi molto semplici possono fare un intenso uso del sistema operativo. Non è raro che un sistema esegua migliaia di chiamate di sistema al secondo. La maggior parte dei programmatori, tuttavia, non si dovrà mai preoccupare di questi dettagli: infatti, gli sviluppatori di applicazioni usano in genere un’**interfaccia per la programmazione di applicazioni (API, _application programming interface_).**
Le API specificano un insieme di funzioni a disposizione del programmatore e dettaglia i parametri necessari all’invocazione di queste funzioni, insieme ai valori restituiti.
Un programmatore ha accesso a un’api tramite una libreria di codice fornita dal sistema operativo.
Per programmi in C in ambienti Unix e Linux tale libreria si chiama libc.
Un dato sistema operativo adotterà nomi suoi propri per ogni system call.
Dietro le quinte, le funzioni fornite da un’api invocano le chiamate di sistema per conto del programmatore.
>>>>>>> 2dc2030001e3a48ca752b40db37f25eb8ed7cd7a
