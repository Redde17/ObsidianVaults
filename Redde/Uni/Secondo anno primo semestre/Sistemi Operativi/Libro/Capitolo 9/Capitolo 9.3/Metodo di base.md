Il metodo di base per implementare la paginazione consiste nel suddividere la memoria fisica in blocchi di dimensione fissa, detti frame, e nel suddividere la memoria logica in blocchi di pari dimensione, detti pagine. 
Quando si deve eseguire un processo, si caricano le sue pagine nei frame disponibili, prendendole dalla memoria ausiliaria o dal file system. 
La memoria ausiliaria è divisa in blocchi di dimensione fissa, uguale a quella dei frame della memoria o di blocchi composti da più frame.
![[Pasted image 20221130164532.png]]

Questa idea piuttosto semplice fornisce grandi funzionalità e ha diverse ramificazioni. 
Per esempio, ora lo spazio degli indirizzi logici è totalmente separato dallo spazio degli indirizzi fisici e dunque un processo può avere uno spazio degli indirizzi logici a 64 bit anche se il sistema ha meno di 2^64 byte di memoria fisica.

Ogni indirizzo generato dalla cpu è diviso in due parti: un **numero di pagina** (_p_), e un **offset di pagina** (_d_):

Il numero di pagina serve come indice per la tabella delle pagine relativa al processo.
![[Pasted image 20221130164727.png]]

La tabella delle pagine contiene l’indirizzo di base di ciascun frame nella memoria fisica e l’offset è la posizione nel frame a cui viene fatto riferimento. 
Pertanto, l’indirizzo di base del frame viene combinato con l’offset della pagina per definire l’indirizzo di memoria fisica. Il modello di paginazione della memoria è mostrato nella seguente figura.
![[Pasted image 20221130164829.png]]

Descriviamo di seguito i passaggi adottati dalla mmu per tradurre un indirizzo logico generato dalla cpu in un indirizzo fisico.
1.  Estrarre il numero di pagina _p_ e utilizzarlo come indice nella tabella delle pagine.
2.  Estrarre il numero di frame _f_ corrispondente dalla tabella delle pagine.
3.  Sostituire il numero di pagina _p_ nell’indirizzo logico con il numero di frame _f_.
L’offset _d_ non cambia e pertanto non viene sostituito; il numero di frame e l’offset determinano insieme l’indirizzo fisico.


La dimensione di una pagina, così come quella di un frame, è definita dall’hardware ed è, in genere, una potenza di 2 compresa tra 4 kb e 1 gb, a seconda dell’architettura. 
La scelta di una potenza di 2 come dimensione della pagina facilita notevolmente la traduzione di un indirizzo logico nei corrispondenti numero di pagina e offset di pagina. 
Se la dimensione dello spazio degli indirizzi logici è $2^m$ e la dimensione di una pagina è di $2^n$ byte, allora gli $m – n$ bit più significativi di un indirizzo logico indicano il numero di pagina, e gli _n_ bit meno significativi indicano l’offset di pagina. 
L’indirizzo logico ha quindi la forma seguente:
![[Pasted image 20221130165817.png]]
dove _p_ è un indice della tabella delle pagine e _d_ è l’offset all’interno della pagina indicata da _p_.


Come esempio concreto, anche se minimo, si consideri la memoria illustrata nella seguente figura;
![[Pasted image 20221130170158.png]]
qui, nell’indirizzo logico, $n = 2$ e $m = 4$. 
Utilizzando pagine di 4 byte e una memoria fisica di 32 byte (8 pagine), vediamo come si fa corrispondere la memoria vista dal programmatore alla memoria fisica. 
L’indirizzo logico 0 è la pagina 0 con offset 0. 
Secondo la tabella delle pagine, la pagina 0 si trova nel frame 5. 
Quindi all’indirizzo logico 0 corrisponde l’indirizzo fisico $20 [= (5 × 4) + 0]$. 
All’indirizzo logico 3 (pagina 0, offset 3) corrisponde l’indirizzo fisico 23 [= (5 × 4) + 3]. Per quel che riguarda l’indirizzo logico 4 (pagina 1, offset 0), secondo la tabella delle pagine, alla pagina 1 corrisponde il frame 6, quindi, all’indirizzo logico 4 corrisponde l’indirizzo fisico 24 [= (6 × 4) + 0]. All’indirizzo logico 13 corrisponde l’indirizzo fisico 9.

Il lettore può aver notato che la paginazione non è altro che una forma di rilocazione dinamica: a ogni indirizzo logico l’architettura di paginazione fa corrispondere un indirizzo fisico. L’uso della tabella delle pagine è simile all’uso di una tabella di registri base (o di rilocazione), uno per ciascun frame.

Con la paginazione si evita la frammentazione esterna: _qualsiasi_ frame libero si può assegnare a un processo che ne abbia bisogno; tuttavia si può avere la frammentazione interna. 
I frame si assegnano come unità. Poiché in generale lo spazio di memoria richiesto da un processo non è un multiplo delle dimensioni delle pagine, l’_ultimo_ frame assegnato può non essere completamente pieno.
Il caso peggiore si ha con un processo che necessita di _n_ pagine più un byte: si assegnano _n_ + 1 frame, quindi si ha una frammentazione interna di quasi un intero frame.

Se la dimensione del processo è indipendente dalla dimensione della pagina, si deve prevedere una frammentazione interna media di mezza pagina per processo. 
Questa considerazione suggerisce che conviene usare pagine di piccole dimensioni; tuttavia, a ogni elemento della tabella delle pagine è associato un overhead che si riduce all’aumentare delle dimensioni delle pagine. Inoltre, con un maggior numero di dati da trasferire, l’i/o su disco è più efficiente.
Generalmente, nel tempo la dimensione delle pagine è cresciuta col crescere dei processi, dei dati e della memoria centrale; attualmente la dimensione tipica delle pagine è compresa tra 4 kb e 8 kb; in alcuni sistemi può essere anche maggiore. 
Per esempio, su sistemi x86-64, Windows 10 supporta dimensioni di pagina di 4 kb e 2 mb, mentre Linux supporta una dimensione di pagina predefinita, in genere di 4 kb, e pagine più grandi la cui dimensione dipende dall’architettura, chiamate pagine enormi (_huge page_).

Una cpu a 32 bit utilizza indirizzi a 32 bit, il che significa che lo spazio di memoria di un processo può essere al massimo di 232 byte (4 gb).
La paginazione ci consente di utilizzare una memoria fisica che è decisamente più grande rispetto a quella che potrebbe essere indirizzata dalla lunghezza del puntatore agli indirizzi della cpu.

Quando si deve eseguire un processo, il sistema esamina la sua dimensione espressa in pagine. Poiché ogni pagina del processo necessita di un frame, se il processo richiede _n_ pagine, devono essere disponibili almeno _n_ frame che, se ci sono, vengono assegnate al processo. Si carica la prima pagina in uno dei frame assegnati e s’inserisce il numero del frame nella tabella delle pagine relativa al processo in questione. La pagina successiva si carica in un altro frame e, anche in questo caso, s’inserisce il numero del frame nella tabella delle pagine, e così via.
![[Pasted image 20221205183632.png]]

Un aspetto importante della paginazione è la netta distinzione tra la memoria vista dal programmatore e l’effettiva memoria fisica: il programmatore vede la memoria come un unico spazio contiguo, contenente solo il programma stesso; in realtà, il programma utente è sparso in una memoria fisica contenente anche altri programmi. La differenza tra la memoria vista dal programmatore e la memoria fisica è colmata dall’hardware di traduzione degli indirizzi, che fa corrispondere gli indirizzi fisici agli indirizzi logici generati dai processi utenti. Questa corrispondenza non è visibile ai programmatori ed è controllata dal sistema operativo. Si noti che un processo utente, per definizione, non può accedere alle zone di memoria che non gli appartengono. Non ha modo di accedere alla memoria oltre quel che è previsto dalla sua tabella delle pagine, e tale tabella contiene soltanto le pagine che appartengono al processo.

Poiché il sistema operativo gestisce la memoria fisica, deve essere informato dei dettagli della allocazione: quali frame sono assegnati, quali sono disponibili, il loro numero totale, e così via. In genere queste informazioni sono contenute in una struttura dati chiamata tabella dei frame, contenente un elemento per ogni frame, indicante se sia libero oppure assegnato e, se è assegnato, a quale pagina di quale processo o di quali processi.

Inoltre, il sistema operativo deve sapere che i processi utenti operano nello spazio utente, e tutti gli indirizzi logici si devono far corrispondere a indirizzi fisici. Se un utente usa una chiamata di sistema (per esempio per eseguire un’operazione di i/o) e fornisce un indirizzo come parametro (per esempio l’indirizzo di un buffer), si deve tradurre questo indirizzo nell’indirizzo fisico corretto. Il sistema operativo conserva una copia della tabella delle pagine per ciascun processo, così come conserva una copia dei valori contenuti nel contatore di programma e nei registri. Questa copia si usa per tradurre gli indirizzi logici in indirizzi fisici ogni volta che il sistema operativo deve associare esplicitamente un indirizzo fisico a un indirizzo logico. La stessa copia è usata anche dal dispatcher della cpu per impostare l’hardware di paginazione quando a un processo sta per essere assegnata la cpu. La paginazione fa quindi aumentare la durata dei cambi di contesto.