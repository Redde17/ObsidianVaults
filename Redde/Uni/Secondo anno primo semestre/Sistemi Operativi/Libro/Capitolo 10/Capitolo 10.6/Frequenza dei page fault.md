Il modello del working set ha avuto successo, e la sua conoscenza può servire per la prepaginazione, ma appare un modo alquanto goffo per controllare il thrashing. 
La strategia basata sulla frequenza dei page fault (_page fault frequency_, pff) è più diretta.

Il problema specifico è la prevenzione del thrashing. 
La frequenza dei page fault in tale situazione è alta, ed è proprio questa che si deve controllare. Se la frequenza è eccessiva, significa che il processo necessita di più frame. Analogamente, se la frequenza dei page fault è molto bassa, il processo potrebbe disporre di troppi frame. 
Si può fissare un limite inferiore e un limite superiore per la frequenza desiderata dei page fault. 
![[Pasted image 20221214180242.png]]
Se la frequenza effettiva dei page fault per un processo oltrepassa il limite superiore, occorre allocare a quel processo un altro frame; se la frequenza scende sotto il limite inferiore, si sottrae un frame a quel processo. Quindi, per prevenire il thrashing, si può misurare e controllare direttamente la frequenza dei page fault.

Come nel caso della strategia del working set, può essere necessaria lo swapping di un processo. Se la frequenza dei page fault aumenta e non ci sono frame disponibili, occorre selezionare un processo e spostarlo sul backing store. 
I frame liberati si distribuiscono ai processi con elevate frequenze di page fault.