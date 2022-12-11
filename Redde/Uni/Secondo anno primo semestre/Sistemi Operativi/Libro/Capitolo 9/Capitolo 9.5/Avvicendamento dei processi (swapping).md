Le istruzioni di un processo e i dati su cui operano per essere eseguiti devono essere in memoria. Tuttavia, un processo, o una sua parte, può essere rimosso temporaneamente dalla memoria centrale (mediante un’operazione detta di _swap out_, scaricamento), spostato in una memoria ausiliaria (_backing store_) e in seguito riportato in memoria (_swap in_, caricamento) per continuare la sua esecuzione. 
![[Pasted image 20221209185106.png]]
Grazie a questo procedimento, detto avvicendamento dei processi o swapping, lo spazio totale degli indirizzi fisici di tutti i processi può eccedere la reale dimensione della memoria fisica del sistema, aumentando così il grado di multiprogrammazione possibile.

### 9.5.1 [[Avvicendamento standard]]