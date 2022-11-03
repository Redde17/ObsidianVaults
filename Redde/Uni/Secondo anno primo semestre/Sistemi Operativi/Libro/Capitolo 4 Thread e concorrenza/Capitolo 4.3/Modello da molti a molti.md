Il modello da molti a molti mette in corrispondenza più thread a livello utente con un numero minore o uguale di thread a livello kernel;

Il numero di thread a livello kernel può essere specifico per una certa applicazione o per un particolare calcolatore (a un’applicazione potrebbero essere assegnati più thread a livello kernel in un’architettura dotata di otto core rispetto a quanti ne verrebbero assegnati in una con quattro core).

![[Pasted image 20221102170628.png]]

Consideriamo l’effetto di questo modello sulla concorrenza. Nonostante il modello da molti a uno permetta ai programmatori di creare tanti thread a livello utente quanti ne desiderino, non viene garantita una concorrenza reale, poiché il meccanismo di scheduling del kernel può scegliere un solo thread alla volta. Il modello da uno a uno permette una maggiore concorrenza, ma i programmatori devono stare attenti a non creare troppi thread all’interno di un’applicazione (in qualche caso si possono avere limitazioni sul numero di thread che si possono creare). Il modello da molti a molti non ha alcuno di questi difetti: i programmatori possono creare liberamente i thread che ritengono necessari e i corrispondenti thread a livello kernel si possono eseguire in parallelo nelle architetture multiprocessore. Inoltre, se un thread impiega una chiamata di sistema bloccante, il kernel può schedulare un altro thread.

Una variante del modello da molti a molti mantiene la corrispondenza fra più thread utente e un numero minore o uguale di thread del kernel, ma permette anche di vincolare un thread utente a un solo thread del kernel. Questa variante è anche chiamata modello a due livelli.
![[Pasted image 20221102170824.png]]

Anche se il modello da molti a molti sembra essere il più flessibile tra quelli trattati è difficile metterlo in atto nella pratica. Inoltre, con un numero sempre crescente di core di elaborazione presenti nella maggior parte dei sistemi, la limitazione del numero di thread a livello kernel è diventata meno importante e, di conseguenza, la maggior parte dei sistemi operativi utilizza ora il modello da uno a uno.