La gestione della memoria discussa finora richiedeva che lo spazio di indirizzamento fisico di un processo fosse contiguo. Introduciamo ora la paginazione, uno schema di gestione della memoria che consente allo spazio di indirizzamento fisico di un processo di essere non contiguo. La paginazione evita la frammentazione esterna e la necessità di compattazione, due problemi che affliggono l’allocazione di memoria contigua. Visti i numerosi vantaggi offerti, la paginazione, nelle sue varie forme, viene utilizzata nella maggior parte dei sistemi operativi, da quelli destinati a server di grandi dimensioni a quelli per dispositivi mobili. L’implementazione della paginazione è frutto della cooperazione tra il sistema operativo e l’hardware del computer.

### 9.3.1 [[Metodo di base]]
### 9.3.2 [[Supporto hardware alla paginazione]]
- ##### 9.3.2.1 TLB
### 9.3.3 [[Protezione]]
### 9.3.4 [[Pagine condivise]]