Nelle descrizioni fatte finora sul tasso di page fault abbiamo supposto che ogni pagina poteva dar luogo al massimo a un fault, la prima volta in cui si effettuava un riferimento a essa.
Tale rappresentazione tuttavia non è molto precisa.
Si potrebbe verificare che la memoria viene riempita da processi non caricati interamente in memoria e appena viene richiesto una pagina non caricata si verifica la sovrallocazione.

La sovrallocazione (_over-allocation_) si può illustrare come segue. 
Durante l’esecuzione di un processo utente si verifica un page fault. Il sistema operativo determina la locazione del disco in cui risiede la pagina desiderata, ma poi scopre che la lista dei frame liberi è _vuota_: tutta la memoria è in uso. 
Questa situazione è illustrata nella seguente figura, dove il punto interrogativo indica il fatto che non ci sono frame liberi.
![[Pasted image 20221213153729.png]]
A questo punto il sistema operativo può scegliere tra diverse possibilità, per esempio può terminare il processo utente. (scelta non migliore)
Il sistema operativo può scaricare dalla memoria un intero processo,
oppure combinare lo swapping con la sostituzione di pagina, una tecnica che descriviamo in dettaglio nel resto di questo paragrafo.


### 10.4.1  [[Sostituzione di pagina]]
### 10.4.2 [[Sostituzione delle pagine secondo l’ordine d’arrivo (fifo)]]
### 10.4.3 [[Sostituzione ottimale delle pagine]]
### 10.4.4 [[Sostituzione delle pagine usate meno recentemente (lru)]]
### 10.4.5 [[Sostituzione delle pagine per approssimazione a lru]]
### 10.4.6 [[Sostituzione delle pagine basata su conteggio]]
