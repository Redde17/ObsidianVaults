Molte delle moderne architetture offrono particolari istruzioni che permettono di controllare e modificare il contenuto di una parola di memoria, oppure di scambiare il contenuto di due parole di memoria, in modo atomico – cioè come un’unità non interrompibile.

Queste speciali istruzioni sono utilizzabili per risolvere il problema della sezione critica in modo relativamente semplice. 
Anziché discutere una specifica istruzione di una particolare architettura, è preferibile astrarre i concetti principali descrivendo le istruzioni test_and_set() e compare_and_swap().

L’istruzione **test_and_set()** si può definire come nella seguente figura:
![[Pasted image 20221108205237.png]]
La caratteristica fondamentale di questa istruzione è che viene eseguita atomicamente; quindi, se si eseguono contemporaneamente due istruzioni test_and_set(), ciascuna in un’unità d’elaborazione diversa, queste vengono eseguite in modo sequenziale in un ordine arbitrario. 
Se si dispone dell’istruzione test_and_set(), si può realizzare la mutua esclusione dichiarando una variabile booleana globale lock, inizializzata a false.

La struttura del processo _Pi_ è illustrata nella seguente figura:
![[Pasted image 20221108205426.png]]


L’istruzione **compare_and_swap()** (cas), proprio come l’istruzione test_and_set (), opera su due parole atomicamente, ma utilizza un meccanismo diverso che si basa sullo scambio del contenuto delle parole.
