Le chiamate di sistema (_system call_) costituiscono un’interfaccia per i servizi resi disponibili dal sistema operativo. Tali chiamate sono generalmente disponibili sotto forma di routine scritte in c o c++, sebbene per alcuni compiti di basso livello, come quelli che comportano un accesso diretto all’hardware, possa essere necessario il ricorso al linguaggio assembly.

## API
Anche programmi molto semplici possono fare un intenso uso del sistema operativo. Non è raro che un sistema esegua migliaia di chiamate di sistema al secondo. La maggior parte dei programmatori, tuttavia, non si dovrà mai preoccupare di questi dettagli: infatti, gli sviluppatori di applicazioni usano in genere un’**interfaccia per la programmazione di applicazioni (API, _application programming interface_).**
Le API specificano un insieme di funzioni a disposizione del programmatore e dettaglia i parametri necessari all’invocazione di queste funzioni, insieme ai valori restituiti.
Un programmatore ha accesso a un’api tramite una libreria di codice fornita dal sistema operativo.
Per programmi in C in ambienti Unix e Linux tale libreria si chiama libc.
Un dato sistema operativo adotterà nomi suoi propri per ogni system call.
Dietro le quinte, le funzioni fornite da un’api invocano le chiamate di sistema per conto del programmatore.