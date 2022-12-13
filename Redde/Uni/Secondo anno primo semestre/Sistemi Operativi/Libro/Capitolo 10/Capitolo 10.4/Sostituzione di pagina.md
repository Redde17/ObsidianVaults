La sostituzione delle pagine segue il seguente criterio: se nessun frame è libero, ne viene liberato uno attualmente inutilizzato.
È possibile liberarlo scrivendo il suo contenuto nell’area di swap e modificando la tabella delle pagine (e tutte le altre tabelle) per indicare che la pagina non si trova più in memoria.
![[Pasted image 20221213154006.png]]
Il frame liberato si può usare per memorizzare la pagina che ha causato il fault. Si modifica la procedura di servizio dell’eccezione di page fault in modo da includere la sostituzione della pagina:

1.  s’individua la locazione su disco della pagina richiesta;
2.  si cerca un frame libero:
    a. se esiste, lo si usa;
    b. altrimenti si impiega un algoritmo di sostituzione delle pagine per scegliere un frame vittima;
    c. si scrive la pagina “vittima” nel disco; si di conseguenza le tabelle delle pagine e quelle dei frame;
3.  si scrive la pagina richiesta nel frame appena liberato; si modificano le tabelle delle pagine e dei frame;
4.  si riprende il processo dal punto in cui si è verificato il page fault.

Occorre notare che, se non esiste alcun frame libero sono necessari _due_ trasferimenti di pagine, uno fuori e uno dentro la memoria. Questa situazione raddoppia il tempo di servizio del page fault e aumenta di conseguenza anche il tempo effettivo d’accesso.

Questo sovraccarico si può ridurre usando un bit di modifica (_modify bit_ o _dirty bit_). In questo caso l’hardware del calcolatore dispone di un bit di modifica, associato a ogni pagina (o frame), che viene posto a 1 ogni volta che nella pagina si scrive un byte, indicando che la pagina è stata modificata.
Quando si sceglie una pagina da sostituire si esamina il suo bit di modifica; se è a 1, significa che quella pagina è stata modificata rispetto a quando era stata letta dal disco; in questo caso la pagina deve essere scritta nel disco. Se il bit di modifica è rimasto a 0, significa che la pagina _non_ è stata modificata da quando è stata caricata in memoria, quindi non è necessario scrivere nel disco la pagina di memoria: c’è già. 
Questa tecnica vale anche per le pagine di sola lettura, per esempio pagine di codice binario. Queste pagine non possono essere modificate, quindi si possono rimuovere in ogni momento. Questo schema può ridurre in modo considerevole il tempo per il servizio del page fault, poiché dimezza il tempo di i/o, _se_ la pagina non è stata modificata.

La sostituzione di una pagina è fondamentale al fine della paginazione su richiesta, perché completa la separazione tra memoria logica e memoria fisica.
Con questo meccanismo si può mettere a disposizione dei programmatori una memoria virtuale enorme con una memoria fisica più piccola. 
Senza la paginazione su richiesta, gli indirizzi utente si fanno corrispondere a indirizzi fisici e i due insiemi di indirizzi possono essere diversi. Tuttavia tutte le pagine di un processo devono ancora essere in memoria fisica.
Con la paginazione su richiesta la dimensione dello spazio degli indirizzi logici non è più limitata dalla memoria fisica. Per esempio, un processo utente formato da 20 pagine si può eseguire in 10 frame semplicemente usando la paginazione su richiesta e un algoritmo di sostituzione per localizzare un frame libero ogni qual volta sia necessario. Se una pagina modificata deve essere sostituita, si copia nel disco il suo contenuto. Un successivo riferimento a quella pagina causa un’eccezione di page fault. In quel momento, la pagina viene riportata in memoria, eventualmente sostituendo un’altra pagina.


Per realizzare la paginazione su richiesta è necessario risolvere due problemi principali: 
occorre sviluppare **un algoritmo di allocazione dei frame** e un **algoritmo di sostituzione delle pagine**.

Esistono molti algoritmi di sostituzione delle pagine; probabilmente ogni sistema operativo ha il proprio schema di sostituzione. È quindi necessario stabilire un criterio per selezionare un algoritmo di sostituzione particolare; comunemente si sceglie quello con il minimo tasso di page fault.