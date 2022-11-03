
### Introduzione e Strutture dei sistemi operativi
1. Indicare sinteticamente quali sono i moduli principali di un SO e come è possibile vederli in maniera strutturata
2. Quali sono le principali componenti di un sistema operativo (fornire una risposta sintetica per categorie)
3. Elencare in maniera sintetica i servizi offerti da un SO e le relazioni/dipendenze che li legano
4. Indicare in maniera sintetica quali sono le funzioni (obiettivi) di un SO e quali sono le principali risorse che deve gestire
5. Descrivere l’approccio allo sviluppo di un SO basato su Microkernel indicandone vantaggi e svantaggi
6. Presentare la tecnica di sviluppo di un SO basato su microkernel indicandone anche i principali vantaggi rispetto alle tecniche tradizionali (kernel monolitico)
7. Definire il concetto di macchina virtuale ed elencare brevemente i vantaggi introdotti e gli svantaggi
8. Cosa è una system call e come avviene il meccanismo di chiamata in un programma utente?
9. Cosa è una “System Call” e qual è il meccanismo di invocazione da un programma utente? Quali sono le implicazioni in termini di sicurezza del sistema (come si discrimina tra gli stati kernel/utente)?
10. Perchè il processore deve avere almeno due modalità operative per il SO? Descrivere le differenze tra le due modalità: stato kernel e stato utente
11. Perchè i moderni processori hanno più modalità di funzionamento? (Protection ring o il concetto di istruzione privilegiata) Descrivere inoltre il meccanismo utilizzato per passare dalla modalità utente alla modalità kernel
12. Descrivere brevemente le modifiche necessarie al kernel per supportare un hardware multiprocessore (SMP)
13. Quali sono le caratteristiche di un sistema multiprocessore SMP? Disegnare l’architettura di massima
14. Quali sono le differenze tra l’elaborazione batch e quella interattiva
15. Descrivere i concetti di “multiprogrammazione” e “multitasking” dal punto di vista del SO, indicando quali moduli del SO coinvolge e quali vantaggi/svantaggi introduce
16. Illustrare brevemente le tecniche per l’I/O basate su interrupt e DMA spiegando in quali casi d’uso (quali dispositivi di I/O) ognuna risulti più adatta ed i vantaggi attesi da ciascuna tecnica


### Gestione dei processi
1. Elencare le informazioni solitamente contenute nel PCB
2. Definire il concetto di processo. Disegnare il diagramma degli stati in cui si può trovare un pocesso ed elencare le principali informazioni contenute nel PCB
3. Descrivere brevemente il concetto di processo e fornire una descrizione dei passi fondamentali necessari per l’esecuzione della syscall fork() dalla sua invocazione alla esecuzione del nuovo processo
4. Indicare i principali metodi per la comunicazione tra processi (IPC) specificando per ognuno vantaggi e svantaggi
5. Quali sono le principali modalità per abilitare la comunicazione tra processi? Per ognuna di queste indicare il modello architetturale di riferimento ed i contesti tipici di utilizzo, elencandone vantaggi e svantaggi.
6. Descrivere il meccanismo di IPC basato sulle pipe. Indicare le limitazioni che tale tecnica impone
7. Descrivere l’utilizzo della pipe() di Unix per la comunicazione tra processi, indicando tutte le limitazioni di tale tecnica. In particolare illustrare quando il processo che apre la pipe in lettura riceve il carattere EOF
8. Descrivere i meccanismi che un SO offre per consentire la cooperazione tra processi o tra più threads. Mostrare quali sono i modelli architetturali attesi per l’hardware sottostante
9. Descrivere l’operazione di Context Switch quando avviene e cosa comporta a livello di sistema operativo
10. Indicare nel dettaglio come avviene l’operazione di context switch da quando il processo running viene interrotto (per scadenza della time slice) a quando un nuovo processo riprende la sua esecuzione
11. (Non lo so) Scrivere un frammento di codice che mostri due processi concorrenti in grado di cooperare. Fornire una descrizione dettagliata delle problematiche da affrontare e delle soluzione possibili alla luce degli strumenti a disposizione

### Thread
1. Descrivere brevemente il modello di programmazione che utilizza i thread, valutando criticamente le diverse tecniche di implementazione. Quale tecnica deve essere utilizzata su una macchina multicore?
2. Descrivere il concetto di Thread e l’architettura sottesa. Che vantaggi offre?
3. Come possono cooperare due o più processi (secondo la definizione data). Quali sono le differenze tra Processi e Threads? Mostrare mediante esempi in pseudocodice quali sono le possibili opzioni e quali sono i modelli architetturali dell’hardware sotteso.
4. Indicare le principali differenze tra processi e thread fornendo un esempio di utilizzo (snippet in pseudocodice) per programmi “concorrenti” in grado di motivare vantaggi e svantaggi di ognuno