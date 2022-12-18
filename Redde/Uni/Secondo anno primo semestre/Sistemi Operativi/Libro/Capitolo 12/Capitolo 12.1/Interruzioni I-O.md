Il meccanismo di base dell’interruzione funziona come segue.
L’hardware della cpu ha un input, detto linea di richiesta dell’interruzione, del quale la cpu controlla lo stato dopo l’esecuzione di ogni istruzione.
Quando rileva il segnale di un controllore sulla linea di richiesta dell’interruzione, la cpu salva lo stato corrente e salta alla routine di gestione dell’interruzione (_interrupt-handler routine_), che si trova a un indirizzo prefissato di memoria.
Questa procedura determina le cause dell’interruzione, porta a termine l’elaborazione necessaria, ripristina lo stato ed esegue un’istruzione return from interrupt per far sì che la cpu ritorni nello stato in cui si trovava prima della sua interruzione. Il controllore del dispositivo _genera_ un’interruzione della cpu sulla linea di richiesta delle interruzioni, che la cpu _rileva_ e _recapita_ al gestore delle interruzioni, che a sua volta _gestisce_ l’interruzione corrispondente servendo il dispositivo.
Nella seguente figura è riassunto il ciclo di i/o causato da un’interruzione della cpu.
![[Pasted image 20221217195609.png]]

Il meccanismo di base delle interruzioni che abbiamo appena descritto permette alla cpu di rispondere a un evento asincrono, come quello di un controllore di un dispositivo che divenga pronto per essere servito.
Nei sistemi operativi moderni sono necessarie capacità di gestione delle interruzioni più raffinate.

1.  Si deve poter posporre la gestione delle interruzioni durante le fasi critiche dell’elaborazione.

2.  Si deve disporre di un meccanismo efficiente per passare il controllo all’appropriato gestore delle interruzioni, senza dover esaminare ciclicamente tutti i dispositivi (_polling_) per determinare quale abbia generato l’interruzione.

3.  Si deve disporre di più livelli d’interruzione, di modo che il sistema possa distinguere le interruzioni ad alta priorità da quelle a priorità inferiore, servendo le richieste con la celerità appropriata al caso.

4.  Abbiamo bisogno di un modo per permettere a un’istruzione di ottenere l’attenzione del sistema operativo direttamente (in maniera distinta rispetto alle richieste di i/o), per attività come la gestione di page fault e per errori come, per esempio, la divisione per zero. Come vedremo, questo ruolo è svolto dalle trap.

In un calcolatore moderno queste caratteristiche sono fornite dalla cpu e dal controllore hardware delle interruzioni.

La maggior parte delle cpu ha due linee di richiesta delle interruzioni. 
Una è quella delle **interruzioni non mascherabili,** riservata a eventi quali gli errori di memoria irrecuperabili. 
La seconda linea è quella delle **interruzioni mascherabili**: può essere disattivata dalla cpu prima dell’esecuzione di una sequenza critica di istruzioni che non deve essere interrotta. 
L’interruzione mascherabile è usata dai controllori dei dispositivi per richiedere un servizio.

Il meccanismo delle interruzioni accetta un indirizzo – un numero che seleziona una specifica procedura di gestione delle interruzioni da un insieme ristretto. 
Nella maggior parte delle architetture questo indirizzo è uno scostamento relativo in una tabella detta vettore delle interruzioni, contenente gli indirizzi di memoria degli specifici gestori delle interruzioni. 
Lo scopo di un meccanismo vettorizzato di gestione delle interruzioni è di ridurre la necessità che un singolo gestore debba individuare tutte le possibili fonti d’interruzione per determinare quale di loro abbia richiesto un servizio. 
In pratica, tuttavia, i calcolatori hanno più dispositivi (e quindi, più gestori delle interruzioni) che elementi nel vettore delle interruzioni. 
Una maniera diffusa di risolvere questo problema consiste nel concatenamento delle interruzioni (_interrupt chaining_), in cui ogni elemento del vettore delle interruzioni punta alla testa di una lista di gestori delle interruzioni. 
Quando si verifica un’interruzione, si chiamano uno alla volta i gestori nella lista corrispondente finché non se ne trova uno che può soddisfare la richiesta. Questa struttura è un compromesso fra l’overhead di una tabella delle interruzioni enorme e l’inefficienza dell’uso di un solo gestore delle interruzioni.

Il meccanismo delle interruzioni realizza anche un sistema di livelli di priorità delle interruzioni. Esso permette alla cpu di differire la gestione delle interruzioni di bassa priorità senza mascherare tutte le interruzioni, e permette a un’interruzione di priorità alta di sospendere l’esecuzione della procedura di servizio di un’interruzione di priorità bassa.

Un sistema operativo moderno interagisce con il meccanismo delle interruzioni in vari modi. All’accensione della macchina esamina i bus per determinare quali dispositivi siano presenti, e installa gli indirizzi dei corrispondenti gestori delle interruzioni nel vettore delle interruzioni.
Durante l’i/o, i vari controllori di dispositivi generano le interruzioni della cpu quando sono pronti per un servizio. 
Queste interruzioni significano che è stato completato un output, o che sono disponibili dati in ingresso, o che un’operazione non è andata a buon fine.
Il meccanismo delle interruzioni si usa anche per gestire un’ampia gamma di eccezioni, come la divisione per 0, l’accesso a indirizzi di memoria protetti o inesistenti o il tentativo di eseguire un’istruzione privilegiata in modalità utente. 
Gli eventi che producono le interruzioni hanno una proprietà in comune: inducono il sistema operativo a eseguire urgentemente una procedura autonoma.

La gestione delle interruzioni ha in molti casi vincoli di tempo e risorse ed è quindi complicata da implementare. Per questa ragione, i sistemi suddividono spesso la gestione delle interruzioni tra un gestore di primo livello (flih) e un gestore di secondo livello (slih): il primo esegue un cambio di contesto, memorizza lo stato e accoda un’operazione di gestione, mentre il secondo, schedulato separatamente, esegue la gestione dell’operazione richiesta.

# Da finire
