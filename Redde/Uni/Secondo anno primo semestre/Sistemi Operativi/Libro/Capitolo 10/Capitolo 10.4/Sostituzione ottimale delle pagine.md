In seguito alla scoperta dell’anomalia di Belady si è ricercato un algoritmo ottimale di sostituzione delle pagine. 
Tale algoritmo è quello che fra tutti gli algoritmi presenta il tasso minimo di page fault e non presenta mai l’anomalia di Belady. 
Questo algoritmo esiste ed è stato chiamato opt o min. 
Consiste semplicemente nel:
	_sostituire la pagina che non verrà usata per il periodo di tempo più lungo._

L’uso di quest’algoritmo di sostituzione delle pagine assicura il tasso minimo di page fault per un dato numero di frame.

Per esempio, nella successione dei riferimenti d’esempio, l’algoritmo ottimale di sostituzione delle pagine produce nove page fault, come è mostrato nella figura seguente. 
![[Pasted image 20221213171323.png]]
I primi tre riferimenti causano page fault che riempiono i tre blocchi di memoria vuoti. 
Il riferimento alla pagina 2 determina la sostituzione della pagina 7, perché la 7 non è usata fino al riferimento 18, mentre la pagina 0 viene usata al 5 e la pagina 1 al 14. 
Il riferimento alla pagina 3 causa la sostituzione della pagina 1, poiché la pagina 1 è l’ultima delle tre pagine in memoria cui si fa nuovamente riferimento. 
Con sole nove page fault, la sostituzione ottimale risulta assai migliore di quella ottenuta con un algoritmo fifo, dove i page fault erano 15.
Ignorando i primi tre page fault, che si verificano con tutti gli algoritmi, la sostituzione ottimale è due volte migliore rispetto all’algoritmo fifo; nessun algoritmo di sostituzione può gestire questa successione di riferimenti a tre blocchi di memoria con meno di nove page fault.

Sfortunatamente l’algoritmo ottimale di sostituzione delle pagine è difficile da realizzare, perché richiede la conoscenza futura della successione dei riferimenti.
Quindi, l’algoritmo ottimale si impiega soprattutto per studi comparativi.