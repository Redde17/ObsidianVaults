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
 A prescindere da considerazioni architetturali come la competizione per l’uso della cache, della memoria e del bus, queste cpu multicore appaiono al sistema operativo come _N_ normali processori.

![[Pasted image 20221006112156.png]]

### NUMA
Aggiungere nuove cpu a un multiprocessore ne aumenta la potenza di calcolo; tuttavia, come suggerito in precedenza, il concetto non scala molto bene e una volta aggiunte troppe cpu il conflitto per il bus di sistema diventa un collo di bottiglia e le prestazioni iniziano a peggiorare. Un approccio alternativo è quello di fornire a ciascuna cpu (o a ciascun gruppo di cpu) la propria memoria locale accessibile per mezzo di un bus locale piccolo e veloce. Ulteriormente le cpu sono collegate tra loro da un'interconnessione di sistema condivisa. Questo approccio è noto come accesso **non uniforme alla memoria o NUMA.** 

![[Pasted image 20221010203014.png]]

Un potenziale svantaggio di un **sistema numa** è la maggior latenza quando una cpu deve accedere alla memoria remota attraverso l’interconnessione di sistema, con un conseguente possibile peggioramento delle prestazioni.
I sistemi operativi possono minimizzare questo svantaggio del numa attraverso un attento scheduling della cpu e un’accurata gestione della memoria.
Poiché i sistemi numa possono scalare per ospitare un numero elevato di processori, stanno diventando sempre più diffusi nei server e nei sistemi di elaborazione ad alte prestazioni.

### Server blade
I cosiddetti server blade, che accolgono nello stesso contenitore fisico le schede del processore, dell’i/o e della rete. A differenza dei tradizionali sistemi multiprocessore, nei server blade ogni scheda dotata di processore avvia ed esegue in maniera indipendente il proprio sistema operativo. Alcune di queste schede, poi, possono essere a loro volta multiprocessore, il che rende più labile la distinzione tra questi diversi tipi di computer.

## Cluster di elaboratori
I cluster di elaboratori (_clustered systems_) o cluster sono un altro tipo di sistemi multiprocessore, basati sull’uso congiunto di più cpu, ma differiscono dai sistemi multiprocessore descritti nel paragrafo precedente per il fatto che sono composti di due o più calcolatori completi – detti nodi – collegati tra loro. Sistemi di questo tipo sono detti debolmente accoppiati (_loosely coupled_).
Pur non essendoci una definizione precisa per tale sistema, la definizione generalmente accettata è che si tratta di calcolatori che condividono la memoria di massa connessi per mezzo di una rete locale o da connessioni più veloci.

Di solito si adotta il clustering per offrire un’elevata disponibilità. Ciascun calcolatore esegue uno strato software di gestione del cluster; ogni nodo può tenere sotto controllo (attraverso la lan) uno o più degli altri nodi. Se il nodo controllato si guasta, il calcolatore che lo sta supervisionando può prendere il controllo della sua memoria e riavviare le applicazioni che erano in esecuzione. Gli utenti e i client delle applicazioni notano solo una breve interruzione del servizio.

Questi sistemi sono preferiti per la loro capacità nel **fault-toleration** che riescono a offrire un servizio proporzionale alla quantità di hardware ancora in funzione, ovvero sono capaci di fare **degrado controllato** (**graceful degradation**)

I **cluster di elaboratori** sono strutturabili in modo sia **asimmetrico sia simmetrico**. 
Nei **cluster asimmetrici** un calcolatore rimane nello stato di **attesa attiva (_hot standby mode_)** mentre l’altro esegue le applicazioni. Il calcolatore in **_hot standby_** non fa altro che monitorare il server attivo. Se questo presenta un problema, il calcolatore di controllo diventa il server attivo. 
**Nei cluster simmetrici** due o più calcolatori eseguono le applicazioni e allo stesso tempo si controllano reciprocamente; in questo modo si ottiene una maggiore efficienza, poiché si utilizzano meglio le risorse, ma ciò richiede che siano disponibili più applicazioni da eseguire.

I cluster, essendo formati da diversi sistemi di computer collegati in rete, possono anche essere utilizzati per ottenere **ambienti di elaborazione ad alte prestazioni (_high-performance computing_)**.
 Tuttavia, le applicazioni devono essere scritte specificatamente in modo da trarre vantaggio dal cluster sfruttando una tecnica chiamata **parallelizzazione (_parallelization_)**.

--Continua sul libro per ulteriori informazioni sui cluster