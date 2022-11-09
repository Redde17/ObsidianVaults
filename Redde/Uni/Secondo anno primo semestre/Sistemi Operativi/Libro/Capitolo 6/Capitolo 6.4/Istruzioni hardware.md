Molte delle moderne architetture offrono particolari istruzioni che permettono di controllare e modificare il contenuto di una parola di memoria, oppure di scambiare il contenuto di due parole di memoria, in modo atomico – cioè come un’unità non interrompibile.

Queste speciali istruzioni sono utilizzabili per risolvere il problema della sezione critica in modo relativamente semplice. 
Anziché discutere una specifica istruzione di una particolare architettura, è preferibile astrarre i concetti principali descrivendo le istruzioni test_and_set() e compare_and_swap().

L’istruzione **test_and_set()** si può definire come nella seguente figura:
![[Pasted image 20221108205237.png]]
La caratteristica fondamentale di questa istruzione è che viene eseguita atomicamente; quindi, se si eseguono contemporaneamente due istruzioni test_and_set(), ciascuna in un’unità d’elaborazione diversa, queste vengono eseguite in modo sequenziale in un ordine arbitrario. 
Se si dispone dell’istruzione test_and_set(), si può realizzare la mutua esclusione dichiarando una variabile booleana globale lock, inizializzata a false.

La struttura del processo _Pi_ è illustrata nella seguente figura:
![[Pasted image 20221108205426.png]]

-------

L’istruzione **compare_and_swap()** (cas), proprio come l’istruzione test_and_set (), opera su due parole atomicamente, ma utilizza un meccanismo diverso che si basa sullo scambio del contenuto delle parole.

La cas, definita nella seguente figura utilizza tre operandi.
![[Pasted image 20221109153808.png]]
L’operando value viene impostato a new_value solo se l’espressione (*value == expected) è vera. 
A parte in questo caso, la compare_and_swap() restituisce sempre il valore originale della variabile value. 
L’importante caratteristica di questa istruzione è che viene eseguita atomicamente. 
Pertanto, se due istruzioni cas vengono eseguite simultaneamente (ciascuna su un core diverso), verranno eseguite sequenzialmente in un ordine arbitrario.

La mutua esclusione può essere realizzata usando cas come segue. 
Viene dichiarata e inizializzata a 0 una variabile globale (lock). Il primo processo che richiama compare_and_swap() imposterà lock a 1. 
Entrerà poi nella sua sezione critica, poiché il valore originale di lock era pari al valore atteso 0. 
Le chiamate successive di compare_and_swap() non avranno successo, perché ora lock non è uguale al valore atteso 0. 
Quando un processo esce dalla sezione critica, imposta di nuovo lock al valore 0, per permettere a un altro processo di entrare nella propria sezione critica. La struttura del processo _Pi_ è illustrata nella seguente figura.
![[Pasted image 20221109154054.png]]

Questo algoritmo soddisfa il requisito della mutua esclusione, ma non quello dell’attesa limitata. 

La seguente figura mostra un altro algoritmo che sfrutta l’istruzione compare_and_swap() che soddisfare tutti e tre i requisiti desiderati.
![[Pasted image 20221109154442.png]]

 Le strutture dati condivise sono\
```
	boolean waiting[n];
	boolean lock;
```

Gli elementi nell’array waiting vengono inizializzati a false e lock viene inizializzato a 0. Per dimostrare che l’algoritmo soddisfa il requisito di mutua esclusione, si noti che il processo _P__i_ può entrare nella propria sezione critica solo se waiting[i] == false oppure key == 0. Il valore di key può diventare 0 solo se si esegue compare_and_swap(). Il primo processo che esegue compare_and_swap() trova key == 0; tutti gli altri devono attendere. La variabile waiting[i] può diventare false solo se un altro processo esce dalla propria sezione critica; solo una variabile waiting[i] vale false, il che consente di rispettare il requisito di mutua esclusione.

Per dimostrare che l’algoritmo soddisfa il requisito di progresso, basta osservare che le argomentazioni fatte per la mutua esclusione valgono anche in questo caso; infatti un processo che esce dalla sezione critica imposta lock al valore false oppure waiting[j] al valore false; entrambe consentono a un processo in attesa l’ingresso nella propria sezione critica.

Per dimostrare che l’algoritmo soddisfa il requisito di attesa limitata occorre osservare che un processo, quando lascia la propria sezione critica, scandisce il vettore waiting in ordine ciclico (_i_ + 1, _i_ + 2, ..., _n_ – 1, 0, ..., _i_ – 1) e designa il primo processo in questo ordinamento presente nella sezione d’ingresso (waiting[j] == true) come il primo processo che deve entrare nella propria sezione critica. Qualsiasi processo che attende l’ingresso nella propria sezione critica può farlo entro _n_ – 1 turni.

Una descrizione dettagliata dell’implementazione delle istruzioni atomiche test_and_set() e compare_and_swap() è reperibile nei testi di architettura dei calcolatori.