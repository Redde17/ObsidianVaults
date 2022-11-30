La memoria centrale deve contenere sia il sistema operativo sia i vari processi utenti; perciò è necessario assegnare le diverse parti della memoria centrale nel modo più efficiente. In questo paragrafo si tratta il primo metodo di allocazione della memoria, **l’allocazione contigua.**

La memoria centrale di solito si divide in due partizioni, una per il sistema operativo residente e una per i processi utente. 
Il sistema operativo si può collocare sia nella parte bassa sia nella parte alta della memoria. Questa decisione dipende da molti fattori, per esempio dalla posizione del vettore delle interruzioni. 
Visto però che molti sistemi operativi (inclusi Linux e Windows) collocano il sistema operativo in memoria alta, discutiamo solo questa situazione.

Generalmente si vuole che più processi utenti risiedano contemporaneamente in memoria centrale. Perciò è necessario considerare come assegnare la memoria disponibile ai processi presenti nella coda d’ingresso che attendono di essere caricati in memoria. 
Con l’allocazione contigua della memoria, ciascun processo è contenuto in una singola sezione di memoria contigua a quella che contiene il processo successivo. Prima di discutere ulteriormente questo schema di allocazione della memoria dobbiamo affrontare il problema della protezione della memoria.

### 9.2.1 [[Protezione della memoria]]
### 9.2.2 [[Allocazione della memoria]]
### 9.2.3 [[Frammentazione]]