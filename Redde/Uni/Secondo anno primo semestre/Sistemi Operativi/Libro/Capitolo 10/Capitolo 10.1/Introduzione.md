Nel Capitolo 9 sono state esaminate varie strategie di gestione della memoria impiegate nei calcolatori(Allocazione contigua e paginazione).

La condizione che le istruzioni debbano essere nella memoria fisica sembra tanto necessaria quanto ragionevole, ma purtroppo riduce le dimensioni dei programmi a valori strettamente correlati alle dimensioni della memoria fisica.
La possibilità di eseguire un programma che si trova solo parzialmente in memoria porterebbe molti benefici sia al sistema sia all’utente..

La memoria virtuale si fonda sulla separazione della memoria logica percepita dall’utente dalla memoria fisica.
Questa separazione permette di offrire ai programmatori una memoria virtuale molto ampia, anche se la memoria fisica disponibile è più piccola.
![[Pasted image 20221212182557.png]]
La memoria virtuale facilita la programmazione, poiché il programmatore non deve preoccuparsi della quantità di memoria fisica disponibile, ma può concentrarsi sul problema da risolvere con il programma.

![[Pasted image 20221212182914.png]]
In un processo, l’ampio spazio vuoto (o buco) che separa lo heap dallo stack è parte dello spazio degli indirizzi virtuali, ma richiede pagine fisiche reali solo nel caso che lo heap o lo stack crescano. Uno spazio degli indirizzi virtuali che contiene buchi si definisce sparso. Un simile spazio degli indirizzi è utile, poiché i buchi possono essere riempiti grazie all’espansione dei segmenti heap o stack, oppure se vogliamo collegare dinamicamente delle librerie (o altri oggetti condivisi) durante l’esecuzione del programma.

Oltre a separare la memoria logica da quella fisica, la memoria virtuale offre il vantaggio di condividere i file e la memoria fra duo o più processi, mediante la condivisione delle pagine.
![[Pasted image 20221212183012.png]]
Ciò comporta i seguenti vantaggi.
- Le librerie di sistema sono condivisibili da diversi processi associando (“mappando”) l’oggetto di memoria condiviso a uno spazio degli indirizzi virtuali.
- In maniera analoga, la memoria può essere condivisa tra processi distinti.
- Le pagine possono essere condivise durante la creazione di un processo mediante la chiamata di sistema fork(), così da velocizzare la generazione dei processi.