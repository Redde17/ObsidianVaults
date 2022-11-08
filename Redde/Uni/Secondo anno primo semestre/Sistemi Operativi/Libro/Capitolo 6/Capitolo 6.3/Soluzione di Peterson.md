Illustriamo adesso una classica soluzione software al problema della sezione critica, nota come soluzione di Peterson.

 A causa del modo in cui i moderni elaboratori eseguono le istruzioni elementari del linguaggio macchina, quali load e store, non è affatto certo che la soluzione di Peterson funzioni correttamente su tali sistemi.
 Tuttavia si è scelto di presentarla ugualmente perché rappresenta un buon algoritmo per il problema della sezione critica che illustra alcune complessità legate alla progettazione di programmi che soddisfino i tre requisiti di mutua esclusione, progresso e attesa limitata.
 
La soluzione di Peterson è limitata a due processi, _P0 e _P1, ognuno dei quali esegue alternativamente la propria sezione critica e la sezione non critica. Per il seguito, è utile convenire che se Pi_ denota uno dei due processi, Pj_ denoti l’altro; ossia, che _j_ = 1 – _i_.

La soluzione di Peterson richiede che i processi condividano i seguenti dati:
```
int turn;
boolean flag[2]
```

La variabile turn segnala, per l’appunto, di chi sia il turno d’accesso alla sezione critica; 
quindi, se turn == i, il processo _Pi_ è autorizzato a eseguire la propria sezione critica. 

L’array flag, invece, indica se un processo _sia pronto_ a entrare nella sezione critica. 
Per esempio, se flag\[i\] è true, _Pi_ è pronto a entrare nella propria sezione critica. 

![[Pasted image 20221108190639.png]]
Per accedere alla sezione critica, il processo _Pi_ assegna innanzitutto a flag\[i\] il valore true; quindi attribuisce a turn il valore j, conferendo così all’altro processo la facoltà di entrare nella sezione critica.

Qualora entrambi i processi tentino l’accesso contemporaneo, all’incirca nello stesso momento sarà assegnato a turno sia il valore i sia il valore j. Soltanto uno dei due permane: l’altro sarà immediatamente sovrascritto. Il valore definitivo di turn stabilisce quale dei due processi sia autorizzato a entrare per primo nella propria sezione critica.

Dimostriamo ora la correttezza di questa soluzione. Dobbiamo provare che:
1.  la mutua esclusione sia preservata;
2.  il requisito del progresso sia soddisfatto;
3.  il requisito dell’attesa limitata sia rispettato.

