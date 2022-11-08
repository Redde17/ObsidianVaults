Illustriamo adesso una classica soluzione software al problema della sezione critica, nota come soluzione di Peterson.

 A causa del modo in cui i moderni elaboratori eseguono le istruzioni elementari del linguaggio macchina, quali load e store, non è affatto certo che la soluzione di Peterson funzioni correttamente su tali sistemi.
 Tuttavia si è scelto di presentarla ugualmente perché rappresenta un buon algoritmo per il problema della sezione critica che illustra alcune complessità legate alla progettazione di programmi che soddisfino i tre requisiti di mutua esclusione, progresso e attesa limitata.
 
La soluzione di Peterson è limitata a due processi, _P0 e _P1, ognuno dei quali esegue alternativamente la propria sezione critica e la sezione non critica. Per il seguito, è utile convenire che se Pi_ denota uno dei due processi, Pj_ denoti l’altro; ossia, che _j_ = 1 – _i_.

La soluzione di Peterson richiede che i processi condividano i seguenti dati:
```
int turn;
boolean
```