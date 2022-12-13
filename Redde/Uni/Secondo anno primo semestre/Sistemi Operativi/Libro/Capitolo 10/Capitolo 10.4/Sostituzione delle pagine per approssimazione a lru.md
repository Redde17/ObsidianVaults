Sono pochi i sistemi di calcolo che dispongono del supporto hardware per una vera sostituzione lru delle pagine. 
Nei sistemi che non offrono alcun supporto hardware si devono impiegare altri algoritmi di sostituzione delle pagine, per esempio l’algoritmo fifo. 
Molti sistemi tuttavia possono fornire un aiuto: **un bit di riferimento.** 
Il bit di riferimento a una pagina è impostato automaticamente dall’hardware del sistema ogni volta che si fa un riferimento a quella pagina, che sia una lettura o una scrittura su qualsiasi byte della pagina. I bit di riferimento sono associati a ciascun elemento della tabella delle pagine.

Inizialmente, il sistema operativo azzera tutti i bit. Quando s’inizia l’esecuzione di un processo utente, l’hardware imposta a 1 il bit associato a ciascuna pagina cui si fa riferimento. Dopo qualche tempo è possibile stabilire quali pagine sono state usate semplicemente esaminando i bit di riferimento. Non è però possibile conoscere l’_ordine_ d’uso. Questa informazione è alla base di molti algoritmi per la sostituzione delle pagine che approssimano lru.

#### 10.4.5.1 Algoritmo con bit supplementari di riferimento
Ulteriori informazioni sull’ordinamento si possono ottenere registrando i bit di riferimento a intervalli regolari. 
È possibile conservare in una tabella in memoria con, per esempio, un byte per ogni pagina. A intervalli regolari, per esempio di 100 millisecondi, un segnale d’interruzione del timer trasferisce il controllo al sistema operativo. Questo inserisce il bit di riferimento per ciascuna pagina nel bit più significativo del byte, shiftando gli altri bit a destra di 1 bit e scartando il bit meno significativo. Questi registri a scorrimento di 8 bit contengono la storia dell’utilizzo delle pagine relativo agli ultimi otto periodi di tempo. 
Se il registro a scorrimento contiene la successione di bit 00000000, significa che la pagina associata non è stata usata da otto periodi di tempo; a una pagina usata almeno una volta per ogni periodo corrisponde la successione 11111111 nel registro a scorrimento. Una pagina cui corrisponde la successione 11000100, è stata usata più recentemente di una pagina a cui corrisponde 01110111. 
Interpretando queste successioni di bit come interi senza segno, la pagina cui è associato il numero minore è la pagina lru, e può essere sostituita. Si noti che l’unicità dei numeri non è garantita. Si possono sostituire tutte le pagine con il valore minore, oppure si può ricorrere a una selezione fifo.

Il numero dei bit può ovviamente essere variato: si sceglie secondo l’hardware disponibile per accelerarne al massimo la modifica. Nel caso limite tale numero si riduce a zero, lasciando soltanto il bit di riferimento. In questo caso l’algoritmo è noto come algoritmo di sostituzione delle pagine con seconda chance.

#### 10.4.5.2 Algoritmo con seconda chance
L’algoritmo di base per la sostituzione con seconda chance è un algoritmo di sostituzione di tipo fifo. 
Tuttavia, dopo aver selezionato una pagina, si controlla il bit di riferimento: se il suo valore è 0, si sostituisce la pagina; se il bit di riferimento è impostato a 1, si dà una seconda chance alla pagina e si passa alla successiva pagina fifo. 
Quando una pagina riceve la seconda chance, si azzera il suo bit di riferimento e si aggiorna il suo istante d’arrivo al momento attuale. 
In questo modo, una pagina cui si offre una seconda chance non viene mai sostituita finché tutte le altre pagine non siano state sostituite, oppure non sia stata data loro una seconda chance. Inoltre, se una pagina è usata abbastanza spesso, da mantenere il suo bit di riferimento impostato a 1, non viene mai sostituita.

Un metodo per implementare l’algoritmo con seconda chance, detto anche a orologio (_clock_), è basato sull’uso di una coda circolare, in cui un puntatore (lancetta) indica qual è la prima pagina da sostituire. Quando serve un frame, si fa avanzare il puntatore finché non si trovi in corrispondenza di una pagina con il bit di riferimento 0; a ogni passo si azzera il bit di riferimento appena esaminato.
![[Pasted image 20221213204017.png]]
Una volta trovata una pagina “vittima”, la si sostituisce e si inserisce la nuova pagina nella coda circolare nella posizione corrispondente. Si noti che nel caso peggiore, quando tutti i bit sono impostati a 1, il puntatore percorre un ciclo su tutta la coda, dando a ogni pagina una seconda chance. Prima di selezionare la pagina da sostituire, azzera tutti i bit di riferimento. Se tutti i bit sono a 1, la sostituzione con seconda chance si riduce a una sostituzione fifo.

#### 10.4.5.3 Algoritmo con seconda chance migliorato
L’algoritmo con seconda chance descritto precedentemente si può migliorare considerando i bit di riferimento e di modifica come una coppia ordinata, con cui si possono ottenere le seguenti quattro classi:
1.  (0, 0) né recentemente usato né modificato – migliore pagina da sostituire;
2.  (0, 1) non usato recentemente, ma modificato – la pagina non così buona poiché prima di essere sostituita deve essere scritta in memoria secondaria;
3.  (1, 0) usato recentemente ma non modificato – probabilmente la pagina sarà presto usata nuovamente;
4.  (1, 1) usato recentemente e modificato – probabilmente la pagina sarà presto ancora usata e dovrà essere scritta in memoria secondaria prima di essere sostituita.
Ogni pagina rientra in una di queste quattro classi. Alla richiesta di una sostituzione di pagina, si usa lo stesso schema impiegato nell’algoritmo a orologio, ma anziché controllare se la pagina puntata ha il bit di riferimento impostato a 1, si esamina la classe a cui la pagina appartiene e si sostituisce la prima pagina che si trova nella classe minima non vuota. Si noti che si può dover scandire la coda circolare più volte prima di trovare una pagina da sostituire.

La differenza principale tra questo algoritmo e il più semplice algoritmo a orologio è che qui si dà la preferenza alle pagine non modificate, al fine di ridurre il numero di i/o richiesti.