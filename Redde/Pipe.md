Una pipe agisce come canale di comunicazione tra processi. Le pipe sono state uno dei primi meccanismi di comunicazione tra processi (ipc) nei primi sistemi unix e generalmente forniscono ai processi uno dei metodi più semplici per comunicare l’uno con l’altro, sebbene con qualche limitazione. Quando si implementa una pipe devono essere prese in considerazione quattro questioni.

1.  La comunicazione permessa dalla pipe è unidirezionale o bidirezionale?
2.  Se è ammessa la comunicazione bidirezionale, essa è di tipo _half duplex_ (i dati possono viaggiare in un’unica direzione alla volta) o _full duplex_ (i dati possono viaggiare contemporaneamente in entrambe le direzioni)?
3.  Deve esistere una relazione (del tipo _padre-figlio_) tra i processi in comunicazione?
4.  Le pipe possono comunicare in rete o i processi comunicanti devono risiedere sulla stessa macchina?

### Pipe convenzionali
Le pipe convenzionali permettono a due processi di comunicare secondo una modalità standard chiamata del produttore-consumatore. Il produttore scrive a una estremità del canale (l’estremità dedicata alla scrittura, o _write-end_) mentre il consumatore legge dall’altra estremità (l’estremità dedicata alla lettura, o _read-end_). Le pipe convenzionali sono quindi unidirezionali, perché permettono la comunicazione in un’unica direzione. Se viene richiesta la comunicazione bidirezionale devono essere utilizzate due _pipe_, ognuna delle quali manda i dati in una direzione. Illustreremo la costruzione di pipe convenzionali sia in unix sia in Windows. In entrambi i programmi di esempio un processo scrive sulla pipe il messaggio Greetings, mentre l’altro lo legge dall’altra estremità della pipe.

Nei sistemi unix le pipe convenzionali sono costruite utilizzando la funzione
```
pipe(int fd[])
```
Essa crea una pipe alla quale si può accedere tramite i descrittori del file int fd[]:fd[0] è l’estremità dedicata alla lettura, mentre fd[1] è l’estremità dedicata alla scrittura. Il sistema unix considera una pipe come un tipo speciale di file; si può così accedere alle pipe tramite le usuali chiamate di sistema read() e write().

Non si può accedere a una pipe al di fuori del processo che la crea. Solitamente un processo padre crea una pipe e la utilizza per comunicare con un processo figlio generato con il comando fork().

Dal momento che la pipe è un tipo speciale di file, il figlio eredita la pipe dal proprio processo padre.

![[Pasted image 20221031171251.png]]
Come mostrato, ogni scrittura del padre sull’estremità dedicata alla scrittura della pipe, fd[1], può essere letta dal figlio sull’estremità dedicata alla lettura, fd[0].

