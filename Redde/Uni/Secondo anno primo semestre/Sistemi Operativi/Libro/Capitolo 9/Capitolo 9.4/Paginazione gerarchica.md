La maggior parte dei moderni calcolatori dispone di uno spazio d’indirizzi logici molto grande (da 232 a 264 elementi). 
In un ambiente di questo tipo la stessa tabella delle pagine diventa eccessivamente grande.
Si consideri, per esempio, un sistema con uno spazio d’indirizzi logici a 32 bit. Se la dimensione di ciascuna pagina è di 4 kb ($2^{12}$), la tabella delle pagine potrebbe arrivare a contenere fino a 1 milione di elementi ($2^{32}$/$2^{12}$). 
Se ogni elemento consiste di 4 byte, ciascun processo potrebbe richiedere fino a 4 mb di spazio fisico d’indirizzi solo per la tabella delle pagine. 
Chiaramente, sarebbe meglio evitare di collocare la tabella delle pagine in modo contiguo in memoria centrale. Una semplice soluzione a questo problema consiste nel suddividere la tabella delle pagine in parti più piccole; questo risultato si può ottenere in molti modi.

Un metodo consiste nell’adottare un algoritmo di paginazione a due livelli, in cui la tabella stessa è paginata. 
![[Pasted image 20221208182636.png]]
Si consideri il precedente esempio di macchina a 32 bit con dimensione delle pagine di 4 kb. Ciascun indirizzo logico è suddiviso in un numero di pagina di 20 bit e in un offset di pagina di 12 bit. Paginando la tabella delle pagine, anche il numero di pagina è a sua volta suddiviso in un numero di pagina di 10 bit e un offset di pagina di 10 bit. 
Quindi, l’indirizzo logico è strutturato come segue:
![[Pasted image 20221208182716.png]]
dove $p_1$ è un indice della tabella delle pagine di primo livello, o tabella esterna delle pagine, e $p_2$ è l’offset all’interno della pagina indicata dalla tabella esterna delle pagine. 
Il metodo di traduzione degli indirizzi seguito da questa architettura è mostrato nella seguente figura. 
![[Pasted image 20221208182819.png]]
Poiché la traduzione degli indirizzi si svolge dalla tabella esterna delle pagine verso l’interno, questo metodo è anche noto come tabella delle pagine ad associazione diretta (_forward-mapped page table_).


Lo schema di paginazione a due livelli non è più adatto nel caso di sistemi con uno spazio di indirizzi logici a 64 bit.
Poiché per evitare di avere tabelle troppo grandi si dovrebbero aggiungere altri livelli di pagine andando a complicare la traduzione dell'indirizzo.
L’Ultrasparc a 64 bit richiederebbe sette livelli di paginazione – con un numero proibitivo di accessi alla memoria – per tradurre ciascun indirizzo logico. 
Da questo esempio è possibile capire perché, per le architetture a 64 bit, le page table gerarchiche sono in genere considerate inappropriate.