Si consideri un qualsiasi processo che non disponga di un numero di frame “sufficiente”. Se non vi sono abbastanza frame per ospitare le pagine del working set, il processo incorre rapidamente in un page fault.

A questo punto si deve sostituire qualche pagina; ma, poiché tutte le sue pagine sono attive, si deve sostituire una pagina che sarà subito necessaria, e di conseguenza si verificano parecchi page fault poiché si sostituiscono pagine che saranno immediatamente riportate in memoria.

Questa intensa paginazione è nota come _thrashing._ Un processo in thrashing spende più tempo per la paginazione che per l’esecuzione dei processi. Com’è immaginabile, il thrashing causa gravi problemi di prestazioni.

### 10.6.1 [[Cause del thrashing]]
### 10.6.2 [[Modello del working set]]
### 10.6.3 [[Frequenza dei page fault]]
### 10.6.4 [[Regole correntemente adottate]]