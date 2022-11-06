In un sistema dotato di un singolo core di elaborazione si può eseguire al massimo un processo alla volta; gli altri processi, se ci sono, devono attendere che la cpu sia libera e possa essere nuovamente sottoposta a scheduling. L’obiettivo della multiprogrammazione è avere sempre un processo in esecuzione, in modo da massimizzare l’utilizzazione della cpu. L’idea è relativamente semplice. Un processo è in esecuzione finché non deve attendere un evento, generalmente il completamento di qualche richiesta di i/o; durante l’attesa, in un sistema di calcolo semplice, la cpu resterebbe inattiva, e tutto il tempo d’attesa sarebbe sprecato. Con la multiprogrammazione si cerca d’impiegare questi tempi d’attesa in modo produttivo: si tengono contemporaneamente più processi in memoria, e quando un processo deve attendere un evento, il sistema operativo gli sottrae il controllo della cpu per cederlo a un altro processo. Su un sistema multicore questo concetto di mantenere occupata la cpu è esteso a tutti i core di elaborazione del sistema.

Lo scheduling è una funzione fondamentale dei sistemi operativi; si sottopongono a scheduling quasi tutte le risorse di un calcolatore. Naturalmente la cpu è una delle risorse principali, e il suo scheduling è alla base della progettazione dei sistemi operativi.

### 5.1.1 [[Ciclicità delle fasi d’elaborazione e di IO]]
### 5.1.2 [[Scheduler della cpu]]
### 5.1.3 [[Scheduling con e senza prelazione]]
### 5.1.4 [[Dispatcher]]