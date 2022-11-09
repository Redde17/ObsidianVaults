Le soluzioni hardware al problema della sezione critica sono complicate e generalmente inaccessibili ai programmatori di applicazioni. 
In alternativa, i progettisti di sistemi operativi implementano strumenti software per risolvere lo stesso problema. 
Il più semplice di questi strumenti è il **lock mutex** (il termine _mutex_ è in realtà l’abbreviazione di _mutual exclusion, cioè mutua esclusione). 

Usiamo il lock mutex per proteggere le regioni critiche e quindi prevenire le race condition. 
In pratica un processo deve acquisire il lock prima di entrare in una sezione critica e rilasciarlo quando esce dalla sezione critica. 
La funzione acquire() acquisisce il lock e la funzione release() lo rilascia, come illustrato nella Figura 6.10.
![[Pasted image 20221109170047.png]]
Un lock mutex ha una variabile booleana available il cui valore indica se il lock è disponibile o meno. 
Se il lock è disponibile la chiamata di acquire() ha successo e il lock viene da questo momento considerato non disponibile. 
Un processo che tenta di acquisire un lock indisponibile viene bloccato fino al rilascio del lock.

La definizione della funzione acquire() è la seguente:
```
acquire() {
	while (!available)
		; /* attesa attiva */
		
	available = false;
}
```

La definizione di release() è la seguente:
```
release() {
	available = true;
}
```

Le chiamate alle funzioni acquire() e release() devono essere eseguite atomicamente. Per questa ragione i lock mutex sono spesso realizzati utilizzando uno dei meccanismi hardware descritti in precedenza.

Il principale svantaggio dell’implementazione che abbiamo fornito è che richiede attesa attiva (_busy waiting_). 
Mentre un processo si trova nella sua sezione critica, ogni altro processo che cerchi di entrare nella sezione critica deve ciclare continuamente effettuando la chiamata acquire(). 
Questo continuo ciclare è chiaramente un problema in un reale sistema multiprogrammato in cui un singolo core della cpu è condiviso tra molti processi. 
L’attesa attiva spreca inoltre cicli di cpu che altri processi potrebbero essere in grado di utilizzare in modo produttivo.

Il tipo di lock mutex che abbiamo descritto è anche chiamato spinlock, perché il processo continua a “girare” (spin) in attesa che il lock diventi disponibile. 
(Osserviamo lo stesso comportamento negli esempi di codice che illustrano l’istruzione compare_and_swap ()). 

Tuttavia, gli spinlock hanno il vantaggio di non rendere necessario alcun cambio di contesto (operazione che può richiedere molto tempo) quando un processo deve attendere un lock e tornano quindi utili quando si prevede che i lock verranno trattenuti per tempi brevi. 
Gli spinlock sono spesso impiegati in sistemi multiprocessore in cui un thread può “girare” su un processore, mentre un altro thread esegue la sua sezione critica su un altro processore.