# Architettura degli elaboratori

## Sistemi monoprocessore
Diversi anni fa la maggior parte dei sistemi utilizzava un solo processore contenente un’unica cpu con un unico nucleo di elaborazione (o unità di calcolo, o _core_). Il nucleo di elaborazione è la componente che esegue le istruzioni e utilizza registri per memorizzare i dati localmente. 
La singola cpu con il suo nucleo di elaborazione è in grado di eseguire un insieme di istruzioni di natura generale, comprese quelle necessarie ai processi utenti. 
I sistemi monoprocessore, inoltre, possiedono altri processori specializzati, deputati a compiti particolari questi processori specializzati sono dotati di un insieme ristretto di istruzioni, e non eseguono processi utenti. Talvolta sono guidati dal sistema operativo, che può inviare loro informazioni sul compito da eseguire successivamente, e controllarne lo stato. Prendiamo l’esempio di un microprocessore che funge da controllore del disco e che riceve dalla cpu un elenco di richieste; spetta a esso implementare una coda e un algoritmo di scheduling per gestirle.
**Questa organizzazione alleggerisce la cpu** dal sovraccarico di lavoro legato allo scheduling del disco.
I pc **ospitano un microprocessore** all’interno della tastiera, per convertire la pressione di ciascun tasto nel codice appropriato da trasmettere alla cpu. In altre circostanze o sistemi, i **processori specializzati** sono dispositivi di basso livello integrati nell’hardware. Il sistema operativo non può comunicare con questi processori, che svolgono in autonomia il proprio lavoro. L’utilizzo di **microprocessori specializzati** è comune e non trasforma un sistema monoprocessore in un sistema multiprocessore.

## Sistemi mutiprocessore
Nei moderni computer, dai dispositivi mobili ai server, i sistemi multiprocessore dominano oggi il panorama della computazione. Tradizionalmente, un sistema di questo tipo dispone di due o più processori, ciascuno con una cpu dotata di una singola unità di calcolo (_single-core_), che condividono il bus e talvolta il clock di sistema, la memoria e i dispositivi periferici. Il vantaggio principale dei sistemi multiprocessore è la maggiore capacità elaborativa (_throughput_). 
Tuttavia con _N_ unità di elaborazione la velocità non aumenta tuttavia di _N_ volte, ma in misura minore.
Infatti, se più unità di elaborazione collaborano nell’esecuzione di un compito, è necessario un certo lavoro supplementare (_overhead_) per garantire che tutti i componenti funzionino correttamente. Questo overhead, unito alla contesa per le risorse condivise, riduce il guadagno atteso dalla disponibilità di più unità di elaborazione.

I sistemi più comuni utilizzano la multielaborazione simmetrica (_symmetric multiprocessing_, smp), in cui ogni processore, alla pari degli altri, è abilitato all’esecuzione di tutte le operazioni del sistema, incluse le funzioni del sistema operativo e i processi utente.

![[Pasted image 20221006093013.png]]

L'**architettura smp** prevede che ogni CPU abbia il proprio set di registri e un cache privata (locale). Tuttavia i processi condividono la memoria fisica sul bus di sistema.

Il vantaggio offerto da questo modello è che molti processi sono eseguibili contemporaneamente (_N_ processi se si hanno _N_ cpu) senza causare un rilevante calo delle prestazioni. Tuttavia, poiché le unità di elaborazione sono separate, una potrebbe essere inattiva, mentre un’altra è sovraccarica e ciò determina un’inefficienza che sarebbe evitabile se le unità d’elaborazione condividessero alcune strutture dati. Questo problema è risolvibile con l'implementazione di un sistema apposito per la gestione del load tra le CPU.

La definizione di **multiprocessore** si è evoluta nel tempo e include ora i **sistemi multicore**, in cui più unità di calcolo (core) risiedono su un singolo chip. Questi sistemi possono essere più efficienti rispetto a più chip dotati di una singola unità di calcolo, perché la comunicazione all’interno di un singolo chip è più veloce rispetto a quella tra un chip e un altro. Inoltre, un chip dotato di diversi core usa molta meno potenza rispetto a diversi chip con un singolo core e ciò è particolarmente importante in dispositivi mobili e laptop.

>Componenti di un sistema di elaborazione
>**CPU**: componente hardware che esegue istruzioni.
>**Processore**: chip che contiene una o più cpu.
>**Unità di calcolo (core)**: unità di elaborazione di base della cpu.
>**Multicore**: Architettura che include più unità di calcolo sulla stessa cpu.
>**Multiprocessore**: che include più processori.

Nei sistemi multicore ogni **core** ha il proprio insieme di reistri e la propria cache spesso nota come cache di **livello 1** o **L1**. Esiste una cache di **livello 2** o **L2** che è locale al chip ma è condivisa tra i core.
La maggior parte delle architetture adotta un sistema con una combinazione di cache locali e condivise di dimensione e velocità diversa.
 A prescindere da considerazioni architetturali come la competizione per l’uso della cache, della memoria e del bus, queste cpu multicore appaiono al sistema operativo come _N_ normali processori

![[Pasted image 20221006112156.png]]
