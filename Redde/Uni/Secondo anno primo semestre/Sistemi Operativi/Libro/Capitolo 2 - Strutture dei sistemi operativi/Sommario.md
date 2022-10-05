-   Un sistema operativo offre un ambiente per l’esecuzione dei programmi fornendo servizi a utenti e applicazioni.
    
-   I tre approcci principali per l’interazione con un sistema operativo sono (1) gli interpreti dei comandi, (2) le interfacce grafiche e (3) le interfacce touch-screen.
    
-   Le chiamate di sistema forniscono un’interfaccia per i servizi resi disponibili da un sistema operativo. I programmatori utilizzano un’api (Application Programming Interface) come interfaccia per l’accesso ai servizi forniti dalle chiamate di sistema.
    
-   Le chiamate di sistema possono essere suddivise in sei categorie principali: (1) controllo dei processi, (2) gestione dei file, (3) gestione dei dispositivi, (4) manutenzione delle informazioni, (5) comunicazioni e (6) protezione.
    
-   La libreria standard del linguaggio C fornisce l’interfaccia alle chiamate di sistema su sistemi unix e Linux.
    
-   I sistemi operativi includono anche una raccolta di programmi di sistema che offrono varie funzionalità agli utenti.
    
-   Un linker combina diversi moduli oggetto rilocabili in un singolo file binario eseguibile. Un loader carica il file eseguibile in memoria, dove diventa idoneo per essere eseguito su una cpu disponibile.
    
-   Vi sono diversi motivi per cui le applicazioni sono specifiche del sistema operativo, tra cui i differenti formati binari per i file eseguibili di un programma, i diversi set di istruzioni per cpu distinte e le chiamate di sistema che variano da un sistema operativo all’altro.
    
-   Un sistema operativo è progettato pensando a obiettivi specifici che determinano, in ultima analisi, le politiche del sistema operativo. Un sistema operativo implementa queste politiche attraverso meccanismi specifici.
    
-   Un sistema operativo monolitico non ha struttura; tutte le funzionalità sono contenute in un singolo file binario statico che viene eseguito in un unico spazio d’indirizzamento. Sebbene tali sistemi siano difficili da modificare, il loro principale vantaggio è l’efficienza.
    
-   Un sistema operativo stratificato è suddiviso in un certo numero di strati, in cui lo strato inferiore è l’interfaccia hardware e quello superiore è l’interfaccia utente. Sebbene i sistemi stratificati abbiano avuto un certo successo, questo approccio non è generalmente ideale per la progettazione di sistemi operativi a causa di problemi di prestazioni.
    
-   L’approccio microkernel per la progettazione di sistemi operativi utilizza un kernel minimale; la maggior parte dei servizi è eseguita come applicazione a livello utente. La comunicazione avviene tramite lo scambio di messaggi.
    
-   Un approccio modulare per la progettazione di sistemi operativi fornisce i servizi del sistema operativo attraverso moduli che possono essere caricati e rimossi durante l’esecuzione. Molti sistemi operativi contemporanei sono progettati come sistemi ibridi e combinano un kernel monolitico con l’utilizzo di moduli.
    
-   Un boot loader carica un sistema operativo in memoria, esegue l’inizializzazione e avvia l’esecuzione del sistema.
    
-   Le prestazioni di un sistema operativo possono essere monitorate utilizzando contatori o tracing. I contatori sono una raccolta di statistiche a livello di sistema o di processo, mentre il tracing segue l’esecuzione di un programma attraverso il sistema operativo.