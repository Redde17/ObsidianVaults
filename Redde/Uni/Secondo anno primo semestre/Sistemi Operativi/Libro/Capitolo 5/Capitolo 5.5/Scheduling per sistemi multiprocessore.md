Se sono disponibili più unità d’elaborazione è possibile la distribuzione del carico (_load sharing_), ma il problema dello scheduling diviene proporzionalmente più complesso. Si sono sperimentate diverse possibilità e, come s’è visto nella trattazione dello scheduling di una sola cpu, “la soluzione migliore” non esiste.

Tradizionalmente, il termine multiprocessore faceva riferimento a sistemi che fornivano più processori fisici, in cui ogni processore conteneva una cpu single-core. Tuttavia, la definizione di multiprocessore si è evoluta in modo significativo e sui moderni sistemi di elaborazione il termine multiprocessore si applica ora alle seguenti architetture di sistema:

-   cpu multicore.    
-   Core multithread.
-   Sistemi numa.
-   Sistemi multiprocessore eterogenei.

Nel seguito si analizzano brevemente alcuni problemi attinenti lo scheduling per sistemi multiprocessore nel contesto di queste diverse architetture. Nei primi tre casi ci concentriamo su sistemi in cui i processori sono identici – omogenei – in termini di funzionalità: si può quindi utilizzare qualsiasi cpu disponibile per eseguire qualsiasi processo presente nella coda. Nell’ultimo caso analizziamo un sistema in cui i processori non hanno le stesse capacità.

### 5.5.1 [[Approcci allo scheduling per multiprocessori]]
### 5.5.2 [[Processori multicore]]
### 5.5.3 [[Bilanciamento del carico]]
### 5.5.4 [[Predilezione per il processore]]