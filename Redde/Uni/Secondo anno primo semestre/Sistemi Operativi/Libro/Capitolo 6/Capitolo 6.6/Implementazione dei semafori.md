Ricordiamo che la realizzazione dei lock mutex presentava il problema dell’attesa attiva. 
Le definizioni delle operazioni sui semafori wait() e signal() appena descritte presentano lo stesso problema.

Per superare la necessità dell’attesa attiva si possono modificare le definizioni delle operazioni wait() e signal() come segue: 
quando un processo invoca l’operazione wait() e trova che il valore del semaforo non è positivo, deve attendere, ma anziché restare nell’attesa attiva può _bloccare_ se stesso. L’operazione di _bloccaggio_ pone il processo in una coda d’attesa associata al semaforo e pone lo stato del processo a _waiting_. 
Quindi, si trasferisce il controllo allo scheduler della cpu che sceglie un altro processo pronto per l’esecuzione.

Un processo sospeso, che attende a un semaforo S, sarà riavviato in seguito all’esecuzione di un’operazione signal() su S da parte di qualche altro processo. 
Il processo si riavvia tramite un’operazione wakeup(), che modifica lo stato del processo da _waiting_ a _ready_. 
Il processo entra nella coda dei processi pronti. 
(L’uso della cpu può essere o non essere commutato dal processo in esecuzione al processo appena divenuto pronto, a seconda del criterio di scheduling).

Per realizzare i semafori secondo quel che s’è detto si può definire il semaforo come segue:
```
typedef struct{
	int value;
	struct process *list;
} semaphore
```
A ogni semaforo sono associati un valore intero (value) e una lista di processi (list), contenente i processi in attesa a un semaforo; l’operazione signal() preleva un processo da tale lista e lo attiva.

L’operazione wait() del semaforo si può definire come segue:
```
wait(semaphore *S){
	S->value--;
	if(S->value < 0){
		aggiungi questo processo a S->list;
		sleep();
	}
}
```

L’operazione signal() del semaforo si può definire come segue:
```
signal(semaphore *S){
	S->value++;
	if(S->value <= 0){
		togli un processo P da S->list;
		wakeup(P);
	}
}
```

L’operazione sleep() sospende il processo che la invoca; l’operazione wakeup(P) pone in stato di pronto per l’esecuzione un processo P bloccato. Queste due operazioni sono fornite dal sistema operativo come chiamate di sistema.

Occorre notare che, mentre la definizione classica di semaforo ad attesa attiva è tale che il valore del semaforo non è mai negativo, questa definizione può condurre a valori negativi. 
Se il valore del semaforo è negativo, il suo valore assoluto rappresenta il numero dei processi che attendono a quel semaforo. Ciò è dovuto all’inversione dell’ordine del decremento e della verifica nel codice dell’operazione wait().

La lista dei processi che attendono a un semaforo si può facilmente realizzare con un campo puntatore in ciascun blocco di controllo del processo (pcb). 
Ogni semaforo contiene un valore intero e un puntatore a una lista di pcb. 
Un modo per aggiungere e togliere processi dalla lista assicurando un’attesa limitata è usare una coda fifo, della quale il semaforo contiene i puntatori al primo e all’ultimo elemento. In generale tuttavia si può usare _qualsiasi_ criterio d’accodamento; il corretto uso dei semafori non dipende dal particolare criterio adottato.


Come già abbiamo detto, le operazioni sui semafori devono essere eseguite in modo atomico.
Si deve garantire che nessuna coppia di processi possa eseguire operazioni wait() e signal() contemporaneamente sullo stesso semaforo. 

Si tratta di un problema di accesso alla sezione critica, e in un contesto monoprocessore lo si può risolvere semplicemente inibendo le interruzioni durante l’esecuzione di signal() e wait(). 
Nei sistemi con una sola cpu, infatti, le interruzioni sono i soli elementi di disturbo: non vi sono istruzioni eseguite da altri processori. 
Finché non si riattivino le interruzioni, dando la possibilità allo scheduler di riprendere il controllo della cpu, il processo corrente continua indisturbato la sua esecuzione.

Nei sistemi multicore sarebbe necessario disabilitare le interruzioni di tutti i core, perché altrimenti le istruzioni dei diversi processi in esecuzione su processori distinti potrebbero interferire fra loro. Tuttavia, disabilitare le interruzioni di tutti i processori può essere complesso, e causare un notevole calo delle prestazioni. È per questo che – per garantire l’esecuzione atomica di wait() e signal() – i sistemi smp devono mettere a disposizione altre tecniche di realizzazione dei lock (per esempio, compare_and_swap() e gli spinlock).

È importante rilevare che questa definizione delle operazioni wait() e signal() non consente di eliminare completamente l’attesa attiva, ma piuttosto di rimuoverla dalle sezioni d’ingresso dei programmi applicativi. Inoltre, l’attesa attiva si limita alle sezioni critiche delle operazioni wait() e signal(), che sono abbastanza brevi; se sono convenientemente codificate, non sono più lunghe di 10 istruzioni. 
Quindi, la sezione critica non è quasi mai occupata e l’attesa attiva si presenta raramente e per breve tempo. 
Una situazione completamente diversa si verifica con i programmi applicativi le cui sezioni critiche possono essere lunghe minuti o anche ore, oppure occupate spesso. In questi casi l’attesa attiva è assai inefficiente.