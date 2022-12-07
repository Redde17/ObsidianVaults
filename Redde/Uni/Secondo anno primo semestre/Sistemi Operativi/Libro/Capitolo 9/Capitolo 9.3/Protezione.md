In un ambiente paginato, la protezione della memoria è assicurata dai bit di protezione associati a ogni frame; normalmente tali bit si trovano nella tabella delle pagine.

Un bit può determinare se una pagina si può leggere e scrivere oppure soltanto leggere.
Tutti i riferimenti alla memoria passano attraverso la tabella delle pagine per trovare il numero corretto del frame; quindi mentre si calcola l’indirizzo fisico, si possono controllare i bit di protezione per verificare che non si scriva in una pagina di sola lettura. 
Un tale tentativo causerebbe la generazione di un’eccezione hardware per il sistema operativo, si avrebbe cioè una violazione della protezione della memoria.

Questo metodo si può facilmente estendere per fornire un livello di protezione più perfezionato. 
Si può progettare un hardware che fornisca la protezione di sola lettura, di sola scrittura o di sola esecuzione. 
In alternativa, con bit di protezione distinti per ogni tipo d’accesso, si può ottenere una qualsiasi combinazione di tali tipi d’accesso; i tentativi illegali causano la generazione di un’eccezione per il sistema operativo.

Di solito si associa a ciascun elemento della tabella delle pagine un ulteriore bit, detto bit di validità. Tale bit, impostato a _valido_, indica che la pagina corrispondente è nello spazio d’indirizzi logici del processo, quindi è una pagina valida; impostato a _non valido_, indica che la pagina non è nello spazio d’indirizzi logici del processo.
Il bit di validità consente quindi di riconoscere gli indirizzi illegali e di notificarne la presenza attraverso un’eccezione. Il sistema operativo concede o impedisce l’accesso a una pagina impostando in modo appropriato tale bit.


Per esempio, supponiamo che in un sistema con uno spazio di indirizzi di 14 bit (da 0 a 16.383) si abbia un programma che deve usare soltanto gli indirizzi da 0 a 10.468. 
Con una dimensione delle pagine di 2 kb si ha la situazione mostrata nella seguente figura.
![[Pasted image 20221207173056.png]]

Gli indirizzi nelle pagine 0, 1, 2, 3, 4 e 5 sono tradotti normalmente tramite la tabella delle pagine. D’altra parte, ogni tentativo di generare un indirizzo nelle pagine 6 o 7 trova non valido il bit di validità; in questo caso il calcolatore invia un’eccezione al sistema operativo (riferimento di pagina non valido).
Questo schema ha creato un problema: poiché il programma si estende solo fino all’indirizzo 10.468, ogni riferimento oltre tale indirizzo è illegale; i riferimenti alla pagina 5 sono tuttavia classificati come validi, e ciò rende validi gli accessi sino all’indirizzo 12.287; solo gli indirizzi da 12.288 a 16.383 sono non validi. 
Tale problema è dovuto alla dimensione delle pagine di 2 kb e corrisponde alla frammentazione interna della paginazione.

Capita raramente che un processo faccia uso di tutto il suo intervallo di indirizzi, infatti molti processi utilizzano solo una piccola frazione dello spazio d’indirizzi di cui dispongono. 
In questi casi è un inutile spreco creare una tabella di pagine con elementi per ogni pagina dell’intervallo di indirizzi, poiché una gran parte di questa tabella resta inutilizzata e occupa prezioso spazio di memoria. Alcune architetture dispongono di registri, detti registri di lunghezza della tabella delle pagine (_page-table length register_, ptlr), per indicare le dimensioni della tabella. Questo valore si controlla rispetto a ogni indirizzo logico per verificare che quest’ultimo si trovi nell’intervallo valido per il processo. Un errore causa la generazione di un’eccezione per il sistema operativo.