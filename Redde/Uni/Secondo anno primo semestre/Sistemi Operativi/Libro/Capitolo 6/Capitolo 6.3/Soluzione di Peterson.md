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

Per dimostrare la proprietà 1, si osservi come ogni _P__i_ acceda alla propria sezione critica solo se flag[j] == false oppure turn == i. Si noti anche che, se entrambi i processi sono eseguibili in concomitanza nelle rispettive sezioni critiche, allora flag[0] == flag[1] == true. Si desume da queste due osservazioni che _P_0 e _P_1 sono impossibilitati a eseguire con successo le rispettive istruzioni while approssimativamente nello stesso momento: turn, infatti, può valere 0 o 1, ma non entrambi. Pertanto, uno dei processi – poniamo _P__j_ – deve aver eseguito con successo l’istruzione while, mentre _P__i_ aveva da eseguire almeno un’istruzione aggiuntiva (“turn == j”). Tuttavia, poiché in quel momento, e fino al termine della permanenza di _P__j_ nella propria sezione critica, restano valide le asserzioni flag[j] == true e turn == j, ne consegue che la mutua esclusione è preservata.

Per dimostrare le proprietà 2 e 3, osserviamo come l’ingresso di un processo _P__i_ nella propria sezione critica possa essere impedito solo se il processo è bloccato nella sua iterazione while, con le condizioni flag[j] == true e turn == j; questa è l’unica possibilità. Qualora _P__j_ non sia pronto a entrare nella sezione critica, flag[j] == false, e _P__i_ può accedere alla propria sezione critica. Se _P__j_ ha impostato flag[j] a true e sta eseguendo il proprio ciclo while, turn == i, oppure turn == j. Se turn == i, _P__i_ entrerà nella propria sezione critica. Se turn == j, _P__j_ entrerà nella propria sezione critica. Tuttavia, al momento di uscire dalla propria sezione critica, _P__j_ reimposta flag[j] a false, consentendo a _P__i_ di entrarvi. Se _P__j_ reimposta flag[j] a true, deve anche attribuire alla variabile turn il valore i. Poiché tuttavia _P__i_ non modifica il valore della variabile turn durante l’esecuzione dell’istruzione while, _P__i_ entrerà nella sezione critica (progresso) dopo che _P__j_ abbia effettuato non più di un ingresso (attesa limitata).

---------

Come accennato all’inizio di questo paragrafo, non è possibile garantire il funzionamento della soluzione di Peterson su architetture moderne, principalmente perché per migliorare le prestazioni del sistema i processori e/o i compilatori possono riordinare operazioni di lettura e scrittura che non hanno dipendenze. Per un’applicazione con un singolo thread questo riordino è irrilevante per quanto riguarda la correttezza del programma, in quanto i valori finali rimangono coerenti con quanto previsto (come avviene nel calcolo del saldo di un conto corrente: l’ordine effettivo in cui vengono eseguite le operazioni di credito e debito non è importante, perché il saldo finale sarà sempre lo stesso), ma per un’applicazione multithread con dati condivisi il riordino delle istruzioni può portare a risultati incoerenti o inattesi.

Si considerino, per esempio, i seguenti dati condivisi tra due thread:
![[Pasted image 20221108204912.png]]
