Come già accennato, il modello del working set è basato sull’ipotesi di località. Questo modello usa un parametro, D, per definire la finestra del working set. L’idea consiste nell’esaminare i più recenti D riferimenti alle pagine. L’insieme di pagine nei più recenti D riferimenti è il working set.
![[Pasted image 20221214175054.png]]
Se una pagina è in uso attivo si trova nel working set; se non è più usata esce dal working set D unità di tempo dopo il suo ultimo riferimento. 
Quindi, il working set non è altro che un’approssimazione della località del programma.

Per esempio, data la successione di riferimenti alla memoria mostrata nella Figura 10.22, se D = 10 riferimenti alla memoria, il working set all’istante $t_1$ è {1, 2, 5, 6, 7}. All’istante $t_2$ il working set è diventato {3, 4}.

La precisione del working set dipende dalla scelta del valore di D. 
Se D è troppo piccolo non include l’intera località, se è troppo grande può sovrapporre più località. Al limite, se D è infinito il working set coincide con l’insieme di pagine cui il processo fa riferimento durante la sua esecuzione.

La caratteristica più importante del working set è la sua dimensione. Calcolandone la dimensione $wss_i$, per ciascun processo $p_i$ del sistema, si può determinare la richiesta totale di frame, cioè _D_:
$D = Σ wss_i.$

Ogni processo usa attivamente le pagine del proprio working set. 
Quindi, il processo $i$ necessita di $wss_i$ frame. 
Se la richiesta totale è maggiore del numero totale di frame liberi (_D_ > _m_), si avrà thrashing, poiché alcuni processi non dispongono di un numero sufficiente di frame.

Una volta scelto D, l’uso del modello del working set è abbastanza semplice. Il sistema operativo controlla il working set di ogni processo e gli assegna un numero di frame sufficiente, rispetto alle dimensioni del suo working set. Se i frame ancora liberi sono in numero sufficiente, si può iniziare un altro processo. Se la somma delle dimensioni dei working set aumenta, superando il numero totale dei frame disponibili, il sistema operativo individua un processo da sospendere. Scrive in memoria secondaria le pagine di quel processo e assegna i suoi frame ad altri processi. Il processo sospeso può essere ripreso successivamente.

Questa strategia impedisce il thrashing, mantenendo il grado di multiprogrammazione più alto possibile, quindi ottimizza l’utilizzo della cpu.

Poiché la finestra del working set è una finestra dinamica, la difficoltà insita in questo modello consiste nel tener traccia degli elementi che compongono il working set stesso. A ogni riferimento alla memoria, a un’estremità appare un riferimento nuovo e il riferimento più vecchio fuoriesce dall’altra estremità. Una pagina si trova nel working set se esiste un riferimento a essa in qualsiasi punto della finestra del working set.

Si può approssimare il modello con un interrupt da timer a intervalli fissi e un bit di riferimento.
Si supponga, per esempio, che D sia pari a 10.000 riferimenti e che sia possibile ottenere un segnale d’interruzione dal timer ogni 5000 riferimenti. Quando si verifica uno di tali segnali d’interruzione, i valori dei bit di riferimento di ciascuna pagina vengono copiati in memoria e poi azzerati. Così, quando si verifica un page fault è possibile esaminare il bit di riferimento corrente e 2 bit in memoria per stabilire se una pagina sia stata usata entro gli ultimi 10.000-15.000 riferimenti. Se lo è stata, almeno uno di questi bit è attivo. Se non lo è stata, questi bit sono tutti inattivi. Le pagine con almeno un bit attivo si considerano appartenenti al working set. Occorre notare che questo schema non è del tutto preciso, poiché non è possibile stabilire dove si è verificato un riferimento entro un intervallo di 5000. L’incertezza si può ridurre aumentando il numero dei bit di cronologia e la frequenza dei segnali d’interruzione, per esempio, 10 bit e un’interruzione ogni 1000 riferimenti. Tuttavia, il costo per servire questi segnali d’interruzione più frequenti aumenta in modo corrispondente.