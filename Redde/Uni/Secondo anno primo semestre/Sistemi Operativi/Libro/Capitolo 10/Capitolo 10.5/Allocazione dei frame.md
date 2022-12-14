Consideriamo ora il problema dell’allocazione. Occorre stabilire un criterio per l’allocazione della memoria libera ai diversi processi. Come esempio, se abbiamo 93 frame liberi e due processi, quanti frame assegnamo a ciascuno?

Si consideri un sistema che disponga di 128 frame. 
Complessivamente sono presenti 128 frame. Il sistema operativo può occuparne 35, lasciando 93 frame per il processo utente. 
In condizioni di paginazione su richiesta pura, tutti i 93 sono inizialmente posti nella lista dei frame liberi. Quando comincia l’esecuzione, il processo utente genera una sequenza di page fault. I primi 93 page fault ricevono i frame liberi dalla lista. 
Una volta esaurita quest’ultima, per stabilire quale tra le 93 pagine presenti in memoria si debba sostituire con la novantaquattresima, si può usare un algoritmo di sostituzione delle pagine. Terminato il processo, si reinseriscono i 93 frame nella lista dei frame liberi.
### 10.5.3 [[Allocazione globale e allocazione locale]]
### 10.5.4 [[Accesso non uniforme alla memoria]]