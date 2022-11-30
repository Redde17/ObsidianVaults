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