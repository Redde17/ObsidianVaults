Il concetto generale alla base della paginazione su richiesta, come è stato detto, è di caricare una pagina in memoria solo quando è necessaria. Di conseguenza, mentre un processo è in esecuzione, alcune pagine saranno in memoria e altre si troveranno nella memoria secondaria.

È dunque necessaria una forma di supporto hardware per distinguere tra i due casi. 
A tale scopo si può utilizzare lo schema basato sul bit di validità. (9.3.3)

In questo caso, però, 
il bit impostato come “valido” significa che la pagina corrispondente è valida ed è presente in memoria; 
il bit impostato come “non valido” indica che la pagina non è valida (cioè non appartiene allo spazio d’indirizzi logici del processo) oppure è valida, ma è attualmente nella memoria secondaria.

L’elemento della tabella delle pagine corrispondente a una pagina caricata in memoria s’imposta come al solito, mentre l’elemento della tabella delle pagine corrispondente a una pagina che attualmente non è in memoria è semplicemente contrassegnato come non valido.

Occorre notare che indicare una pagina come non valida non sortisce alcun effetto se il processo non tenta mai di accedervi.

![[Pasted image 20221212184145.png]]

L’accesso a una pagina contrassegnata come non valida causa un evento o **eccezione di page fault (_pagina mancante_).**
L’hardware di paginazione, traducendo l’indirizzo attraverso la tabella delle pagine, nota che il bit è non valido e genera una trap per il sistema operativo; tale eccezione è dovuta a un “insuccesso” del sistema operativo nella scelta delle pagine da caricare in memoria. 
La procedura di gestione dell’eccezione di page fault è lineare

*Fasi di gestione di un page fault:*
![[Pasted image 20221212184426.png]]
1. Si controlla una tabella interna per questo processo allo scopo di stabilire se il riferimento fosse un accesso alla memoria valido o non valido.
2. Se il riferimento non era valido, si termina il processo. Se era un riferimento valido, ma la pagina non era ancora stata portata in memoria, se ne effettua il caricamento.
3. Si individua un frame libero, per esempio prelevandone uno dalla lista dei frame liberi.
4. Si programma un’operazione sui dischi per trasferire la pagina desiderata nel frame appena assegnato.
5. Quando la lettura dal disco è completata, si modificano la tabella interna, conservata con il processo, e la tabella delle pagine per indicare che la pagina si trova attualmente in memoria.
6. Si riavvia l’istruzione interrotta dall’eccezione. A questo punto il processo può accedere alla pagina come se questa fosse stata sempre presente in memoria.

Come caso estremo, è possibile avviare l’esecuzione di un processo _senza_ pagine in memoria.
In un caso del genere il programma generea page fault dalla prima istruzione e il programma viene caricato mentre si esegue.

Lo schema descritto è una paginazione su richiesta pura, vale a dire che una pagina non si trasferisce mai in memoria se non viene richiesta.

L’hardware di supporto alla paginazione su richiesta è lo stesso che è richiesto per la paginazione e l’avvicendamento dei processi in memoria:
- Tabella delle pagine con bit di validitá.
- Memoria secondaria per le pagine non in memoria centrale.

Uno dei requisiti cruciali della paginazione su richiesta è la possibilità di rieseguire una qualunque istruzione dopo un page fault.
Avendo salvato lo stato del processo interrotto al momento del page fault, occorrerà riavviare il processo _esattamente_ dallo stesso punto e con lo stesso stato, eccezion fatta per la presenza della pagina desiderata in memoria.
Nella maggior parte dei casi questo requisito è facile da soddisfare.
Un page fault si può verificare per qualsiasi riferimento alla memoria.
Se si verifica durante la fase di fetch (prelievo) di un’istruzione, l’esecuzione si può riavviare effettuando nuovamente il fetch.
Se si verifica durante il fetch di un operando, bisogna effettuare nuovamente fetch e decode dell’istruzione, quindi si può prelevare l’operando.

La difficoltà maggiore si presenta quando un’istruzione può modificare parecchie locazioni diverse.
(libro)

Il sistema di paginazione si colloca tra la cpu e la memoria di un calcolatore e deve essere completamente trasparente al processo utente.

