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
