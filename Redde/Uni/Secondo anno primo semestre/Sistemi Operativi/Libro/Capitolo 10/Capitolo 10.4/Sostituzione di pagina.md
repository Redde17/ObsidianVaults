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