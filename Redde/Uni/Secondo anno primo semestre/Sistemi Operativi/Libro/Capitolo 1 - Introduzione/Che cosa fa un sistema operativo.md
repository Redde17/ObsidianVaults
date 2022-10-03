# Introduzione
*Un **sistema operativo** é un insieme di programmi che gestisce gli elementi fisici di un calcolatore*.
Esso fornisce una piattaforma ai programmi applicativi e agisce da intermediario fra l'utente e la struttura fisica del calcolatore.

Per esplorare il ruolo di un **sistema operativo** in un ambiente di elaborazione moderno é importante capire l'organizzazione e l'architettura dell'hardware del computer, ovvero CPU, memoria, periferiche e dispositivi di memorizzazione. *Una responsabilitá fondamentale del **sistema operativo** é allocare queste risorse ai programmi*.

Data la complessitá e ampiezza di un sistema operativo, esso deve essere costruito per parti, gradualmente e ciascuna parte deve rappresentare un'unitá ben riconoscibile del sistema, dotata di funzioni, dati in entrata e in uscita accuratamente definiti.

## Che cosa fa un sistema operativo
Per poter analizzare le mansioni di un sistema operativo va prima considerato il ruolo di quest'ultimo nell'insieme di elaborazione.
Un sistema di elaborazione si puó suddividere in quattro componenti:

![[Pasted image 20221003204241.png]]

- **Hardware**: Composto dalla CPU, dalla memoria e dalle periferiche di I/O, fornisce le risorse elaborative fondamentali. 
- **Sistema operativo**: controlla l'hardware e ne coordina l'utilizzo da parte dei programmi applicativi per gli utenti.
- **Programmi epplicativi**: definiscono il modo in cui si usano queste risorse per la risoluzione dei problemi computazionali degli utenti. 
- **Utente

Un sistema elaborativo si puó anche considerare come l'insieme di hardware, software e dati. Il sistema operativo offre gli strumenti per impegare in modo corretto queste risorse. Il sistema operativo quindi di per sé non compie operazioni utili ma fornisce un ambiente nel quale altri programmi possono lavorare in modo utile.

Per meglio approfondire il ruolo del sistema operativo, esso va esplorato dal punto di vista dell'utente e del sistema.

### Punto di vista dell'utente
La percezione di un calcolatore da parte di un utente dipende principalmente dall’interfaccia impiegata che varia a seconda del calcolatore utilizzato.

**Per utenti che utilizzano un pc o un portatile** composti da schrmo, tastiera e mouse, questi dispostivi, progettati per un singolo utente, impiegano le risorse in modo esclusivo con lo scopo di massimizzare la produttivitá, in questo caso il sistema operativo viene progettato considerando principalmente la facilitá d'uso.

Alcuni calcolatori hanno poca o nessuna visibilitá per gli utenti, essi vengono chiamati **calcolatori integrati** o **embedded**, e sono per lo piú presenti in elletrodomestici e automobili, hanno interfaccie minime se non assenti e i loro sistemi operativi, nella maggior parte dei casi sono progettati per funzionare senza l'intervento degli utenti.

### Punto di vista del sistema
Dal punto di vista del calcolatore il sistema operativo é il programma piú strettamente correlato al suo hardware. In tale contesto é possibile considerare un sistema operativo come un **assegnatore di risorse**. 

**Un** **sistema elaborativo dispone di risorse utili per la risoluzione di un problema**: *tempo di cpu, spazio di memoria, spazio per la memorizzazione di file, dispositivi di i/o e così via.* 
Il sistema operativo agisce come gestore di tali risorse. Di fronte a richieste di risorse numerose ed eventualmente conflittuali, il sistema operativo deve decidere come assegnarle agli specifici programmi e utenti affinché il sistema elaborativo operi in modo equo ed efficiente.

Una visione leggermente diversa di un sistema operativo enfatizza la necessità di controllare i dispositivi di i/o e i programmi utenti; un sistema operativo è in effetti un programma di controllo. Un programma di controllo gestisce l’esecuzione dei programmi utenti in modo da impedire che si verifichino errori o che il calcolatore sia usato in modo scorretto. Si occupa soprattutto del funzionamento e del controllo dei dispositivi di i/o.

### Definizione di sistema operativo
In generale, non esiste una definizione completa ed esauriente. I sistemi operativi esistono poiché rappresentano una soluzione ragionevole al problema di realizzare un sistema elaborativo che si possa impiegare facilmente, per eseguire i programmi e agevolare la soluzione dei problemi degli utenti. È proprio a questo scopo che viene realizzato l’hardware dei calcolatori; ma, poiché il solo hardware non è molto facile da utilizzare, sono stati sviluppati i programmi applicativi. Questi programmi sono diversi tra loro, ma richiedono alcune funzioni comuni, per esempio il controllo dei dispositivi di i/o. Tali funzioni comuni, di controllo e assegnazione delle risorse, sono state racchiuse in un unico insieme di programmi: il sistema operativo.

Non esiste neppure una definizione universalmente accettata di che cosa faccia parte di un sistema operativo poiché le funzionalitá di un sistema operativo variano da sistema a sistema.