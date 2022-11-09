Come abbiamo accennato in precedenza, i lock mutex sono generalmente considerati il più semplice degli strumenti di sincronizzazione. In questo paragrafo esaminiamo uno strumento più robusto in grado di comportarsi in modo simile a un lock mutex, ma capace anche di fornire metodi più complessi per la sincronizzazione delle attività dei processi.

Un semaforo S è una variabile intera cui si può accedere, escludendo l’inizializzazione, solo tramite due operazioni atomiche predefinite: wait() e signal(). 

La definizione di wait() in pseudocodice è la seguente:

```
wait(S){
	while(S <= 0)
	;//atesa attiva
	S--;
}
```

La definizione di signal() in pseudocodice è la seguente:
```
signal(S){
	S++
}
```

Tutte le modifiche al valore del semaforo contenute nelle operazioni wait() e signal() si devono eseguire in modo indivisibile: mentre un processo cambia il valore del semaforo, nessun altro processo può contemporaneamente modificare quello stesso valore. Inoltre, nel caso della wait(S) si devono eseguire senza interruzione anche la verifica del valore intero di S (S ≤ 0) e la sua possibile modifica (S--).

### 6.6.1 [[Uso dei semafori]]
### 6.6.2 [[Implementazione dei semafori]]