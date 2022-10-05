# Organizzazione di un sistema elaborativo
Un moderno calcolatore general-purpose è composto da una o più cpu e da un certo numero di controllori di dispositivi connessi attraverso un canale di comunicazione comune (_bus_) che permette l’accesso alla memoria condivisa dal sistema.

![[Pasted image 20221005181716.png]]

I sistemi operativi possiedono in genere per ogni controllore di dispositivo un driver del dispositivo che gestisce le specificità del controllore e funge da interfaccia uniforme con il resto del sistema. La cpu e i controllori possono eseguire operazioni in parallelo, competendo per i cicli di memoria. Per garantire un accesso ordinato alla memoria condivisa un controllore della memoria sincronizza gli accessi.

------------

## Sintesi delle interruzioni
Le interruzioni vengono utilizzate nei moderni sistemi operativi per gestire eventi asincroni (e per altri scopi, che vedremo più avanti nel testo). Le interruzioni sono sollevate dai controllori dei dispositivi e dal verificarsi di errori. Per consentire al lavoro più urgente di essere completato per primo, i computer moderni utilizzano un sistema di priorità delle interruzioni. Poiché le interruzioni vengono pesantemente utilizzate nell’elaborazione time-sensitive, è necessaria una gestione efficiente delle interruzioni per garantire buone prestazioni del sistema.

-----------------

## Interruzioni
Si consideri un’operazione tipica del computer: un programma che esegue i/o. Per avviare un’operazione di i/o, il driver del dispositivo scrive negli appropriati registri all’interno del controllore, il quale esamina i contenuti di questi registri per determinare l’azione da intraprendere (per esempio “leggi un carattere dalla tastiera”). Il controllore comincia a trasferire i dati dal dispositivo al proprio buffer e a trasferimento completato informa il driver, tramite un’interruzione, di avere terminato l’operazione. Il driver passa quindi il controllo ad altre parti del sistema operativo, restituendo i dati (o un puntatore a essi) se l’operazione è di lettura; per altre operazioni, il driver restituisce delle informazioni di stato come “scrittura completata correttamente” o “periferica occupata”. 

Come fa il controllore a comunicare al driver del dispositivo che ha terminato la sua operazione? Lo fa per mezzo di un’interruzione (_interrupt_).

-----------

### Panoramica
L’hardware può generare un’interruzione in qualsiasi momento inviando un segnale alla cpu, solitamente tramite il bus di sistema (ci possono essere molti bus all’interno di un sistema di elaborazione, ma il bus di sistema è il principale percorso di comunicazione tra i componenti fondamentali). Le interruzioni sono utilizzate anche per molti altri scopi e costituiscono una componente chiave nell’interazione tra i sistemi operativi e l’hardware.

Quando riceve un segnale d’interruzione, la cpu interrompe l’elaborazione corrente e trasferisce immediatamente l’esecuzione a una locazione fissa della memoria. Di solito, questa locazione contiene l’indirizzo iniziale della procedura di servizio dell’interruzione. Una volta completata l’esecuzione della procedura richiesta, la cpu riprende l’elaborazione precedentemente interrotta.

![[Pasted image 20221005182157.png]]

Ciascun tipo di calcolatore ha il proprio meccanismo di gestione delle interruzioni; ciò nonostante molte funzioni sono comuni. Ogni interruzione deve causare il trasferimento del controllo all’appropriata procedura di servizio. Il modo più semplice per gestire quest’operazione è quello di impiegare una procedura generale che esamini le informazioni associate all’interruzione, e a sua volta invochi la procedura di gestione dello specifico evento.
La gestione di un’interruzione deve essere molto rapida, perché le interruzioni si verificano frequentemente. È possibile usare una tabella di puntatori alle specifiche procedure in modo che l’attivazione delle procedure di servizio delle interruzioni avvenga in modo indiretto. 
In genere questa tabella di puntatori è memorizzata nella memoria agli indirizzi più bassi.  L’accesso a questa sequenza d’indirizzi, detta vettore delle interruzioni, avviene per mezzo di un indice, codificato nello stesso segnale d’interruzione, allo scopo di fornire l’indirizzo della procedura di servizio relativa all’evento segnalato dall’interruzione.

L’architettura di gestione delle interruzioni deve anche salvare le informazioni di stato dell’operazione interrotta, in modo da poterle ripristinare una volta che l’interruzione è stata servita. Se la procedura di gestione dell’interruzione richiede la modifica dello stato del processore, per esempio modificando il contenuto di qualche registro, deve salvare esplicitamente lo stato corrente per poterlo ripristinare prima di restituire il controllo. Terminato il servizio dell’interruzione, l’indirizzo di ritorno precedentemente salvato viene caricato nel contatore di programma (_program counter_), consentendo la ripresa della computazione interrotta come se nulla fosse accaduto.

----------------------------------------------

### Implementazione
L’hardware della cpu dispone di un filo chiamato linea di richiesta di interruzione (_interrupt-request line_) che la cpu controlla dopo l’esecuzione di ogni istruzione.
Quando la cpu rileva che un controllore ha asserito un segnale sulla linea di richiesta di interruzione, legge il numero di interruzione e salta alla routine di gestione dell’interruzione utilizzando il numero letto come indice nel vettore delle interruzioni, per poi avviare l’esecuzione all’indirizzo associato a tale indice.
Il gestore delle interruzioni salva le informazioni di stato che verranno modificate durante le operazioni, determina la causa dell’interruzione, esegue l’elaborazione necessaria, ripristina lo stato ed esegue un’istruzione di ritorno dall’interruzione (return_from_interrupt) per riportare la cpu allo stato di esecuzione precedente all’interrupt.

In altre parole, il controllore del dispositivo _solleva_ un’interruzione asserendo un segnale sulla linea di richiesta di interruzione, la cpu _intercetta_ l’interruzione e la _invia_ al gestore delle interruzioni che, a sua volta, soddisfa l’interruzione offrendo al dispositivo il servizio richiesto.

![[Pasted image 20221005183745.png]]

Il meccanismo di interruzione appena descritto consente alla cpu di rispondere a un evento asincrono, come nel caso in cui un controllore di periferica diventi pronto per offrire un servizio. In un moderno sistema operativo, tuttavia, sono necessarie funzionalità di gestione delle interruzioni più sofisticate. In particolare:
- La possibilità di posticipare la gestione degli interrupt durante un’elaborazione critica;
- Un modo efficiente per inviare l’interruzione al gestore appropriato per un dispositivo;
- Interruzioni multilivello, in modo che il sistema operativo possa distinguere tra interruzioni ad alta e bassa priorità e possa rispondere con il livello di urgenza appropriato.
- 
In un’architettura moderna queste tre funzioni sono fornite dalla cpu e dall’hardware del controllore delle interruzioni.

La maggior parte delle cpu ha **due linee di richiesta di interruzione**: una è **non mascherabile (_nonmaskable interrupt_)**, riservata a eventi come errori irreversibili di memoria, mentre la seconda è **mascherabile (_maskable interrupt_)**, ovvero può essere disattivata dalla cpu prima dell’esecuzione di sequenze di istruzioni critiche che non devono essere interrotte. 

>L’interruzione mascherabile è quella utilizzata dai controllori dei dispositivi per richiedere un servizio.

lo scopo di un meccanismo di interruzione basato sul vettore delle interruzioni è quello di evitare a un singolo gestore di interruzioni di dover cercare tra tutte le possibili fonti per determinare quale ha bisogno di assistenza. Tuttavia i computer hanno più dispositivi, quindi, più gestori di interruzioni di quanti siano i campi indirizzo presenti nel vettore delle interruzioni. 
Un modo comune per risolvere questo problema è utilizzare il **concatenamento delle interruzioni (_interrupt chaining_)**, in cui ogni elemento nel vettore delle interruzioni punta alla testa di un elenco di gestori.
Quando viene sollevata un’interruzione, i gestori nell’elenco corrispondente vengono chiamati a uno a uno, finché non ne viene trovato uno in grado di servire la richiesta.

*vettore delle interruzioni dei processori Intel, da 0 a 31 gli eventi non sono mascherabili*
![[Pasted image 20221005184423.png]]


