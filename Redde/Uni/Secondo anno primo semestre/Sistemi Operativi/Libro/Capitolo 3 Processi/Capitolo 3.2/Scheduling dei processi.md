L’obiettivo della **multiprogrammazione** consiste nell’avere sempre un processo in esecuzione in modo da massimizzare l’utilizzo della cpu.
L’obiettivo del **time-sharing** è di commutare l’uso della cpu tra i vari processi così frequentemente che gli utenti possano interagire con ciascun programma mentre è in esecuzione.

Per raggiungere questi obiettivi, lo scheduler dei processi seleziona un processo da eseguire dall’insieme di quelli disponibili. Ogni core della cpu può eseguire un processo alla volta. In un sistema con un singolo core non verrà quindi mai eseguito più di un processo alla volta, mentre un sistema multicore può eseguire più processi contemporaneamente. Se vi sono più processi che core, i processi in eccesso dovranno attendere fino a quando un core diventa libero e può essere riassegnato.

Il numero di processi in memoria in un dato istante è noto come il grado di multiprogrammazione.

### 3.2.1 [[Code di scheduling]]
### 3.2.2 [[Scheduling della CPU]]
### 3.2.3 [[Cambio di contesto]]