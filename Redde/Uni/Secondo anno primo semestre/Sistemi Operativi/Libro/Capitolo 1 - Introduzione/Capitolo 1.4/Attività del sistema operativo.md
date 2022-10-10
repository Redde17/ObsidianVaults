## Attività del sistema operativo
Il sistema operativo costituisce l’ambiente di esecuzione dei programmi. Sebbene la struttura dei sistemi operativi possa variare grandemente, vi sono alcuni aspetti comuni che esponiamo in questo paragrafo.

L’avviamento del sistema, conseguente all’accensione del calcolatore, così come il riavvio di un calcolatore già acceso, richiedono la presenza di un **programma di avviamento (_bootstrap program_)** normalmente memoriazzato nel firmware.


### Multiprogrammazione e multitasking
n generale, un singolo programma non è in grado di tenere costantemente occupati la cpu e i dispositivi di i/o. Inoltre, gli utenti vogliono solitamente eseguire più programmi allo stesso tempo. La multiprogrammazione, oltre a soddisfare questa esigenza degli utenti, consente di aumentare la percentuale di utilizzo della cpu, organizzando i programmi in modo tale da mantenerla in continua attività. In un sistema multiprogrammato un programma in esecuzione è chiamato _processo_.

In un sistema non multiprogrammato, nei periodi di attesa di un programma la CPU resta inattiva.
In un sistema con multiprogrammazione, nei periodi di attesa di un processo la CPU passa a un altro processo e lo esegue.