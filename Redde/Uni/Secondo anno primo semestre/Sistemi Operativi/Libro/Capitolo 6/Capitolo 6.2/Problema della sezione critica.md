Iniziamo la nostra discussione sui processi di sincronizzazione illustrando il problema della sezione critica.

Si consideri un sistema composto di _n_ processi {_P_0, _P_1, …, _P__n_–1} ciascuno avente un segmento di codice, chiamato sezione critica (detto anche _regione critica_), in cui il processo può modificare variabili comuni, aggiornare una tabella, scrivere in un file e così via.
La caratteristica fondamentale del sistema è che, quando un processo è in esecuzione nella propria sezione critica, non si consente ad alcun altro processo di essere in esecuzione nella propria sezione critica. Il problema della _sezione critica_ consiste nel progettare un protocollo che i processi possano usare per cooperare.
Ogni processo deve chiedere il permesso per entrare nella propria sezione critica.

La sezione di codice che realizza questa richiesta è la sezione d’ingresso.
La sezione critica può essere seguita da una sezione d’uscita, e la restante parte del codice è detta sezione non critica. 

La seguente figura mostra la struttura generale di un tipico processo. 
La sezione d’ingresso e quella d’uscita sono state inserite nei riquadri per evidenziare questi importanti segmenti di codice.
![[Pasted image 20221108182336.png]]

Una soluzione del problema della sezione critica deve soddisfare i tre seguenti requisiti.
1.  **Mutua esclusione**. Se il processo _Pi_ è in esecuzione nella sua sezione critica, nessun altro processo può essere in esecuzione nella propria sezione critica.
2.  **Progresso**. Se nessun processo è in esecuzione nella sua sezione critica e qualche processo desidera entrare nella propria sezione critica, solo i processi che si trovano fuori dalle rispettive sezioni non critiche possono partecipare alla decisione riguardante la scelta del processo che può entrare per primo nella propria sezione critica; questa scelta non si può rimandare indefinitamente.
3.  **Attesa limitata**. Se un processo ha già richiesto l’ingresso nella sua sezione critica, esiste un limite al numero di volte che si consente ad altri processi di entrare nelle rispettive sezioni critiche prima che si accordi la richiesta del primo processo.

Si suppone che ogni processo sia eseguito a una velocità diversa da zero. Tuttavia, non si può fare alcuna ipotesi sulla velocità relativa degli _n_ processi.

In un dato momento, numerosi processi in modalità kernel possono essere attivi nel sistema operativo. Se ciò si verifica, il codice del kernel, che implementa il sistema operativo, è soggetto a molte possibili race condition. Si consideri per esempio una struttura dati del kernel che mantenga una lista di tutti i file aperti nel sistema. Tale lista deve essere modificata quando un nuovo file è aperto, e quindi aggiunto all’elenco, oppure chiuso, e quindi tolto dall’elenco. Se due o più processi dovessero aprire dei file simultaneamente, potrebbero ingenerare nel sistema una race condition legata ai necessari aggiornamenti della lista.

Un altro esempio è illustrato nella seguente figura.
![[Pasted image 20221108183404.png]]
In questa situazione, due processi _P0 e _P1 creano processi figlio (child) utilizzando la chiamata di sistema fork(). 
Ricordiamo che fork() restituisce al processo genitore l’identificatore di processo (pid) del processo appena creato. 
In questo esempio, c’è una race condition sulla variabile del kernel next_available_pid, che contiene il valore del prossimo pid disponibile. In assenza di mutua esclusione è possibile che lo stesso pid venga assegnato a due processi distinti.

Altre strutture dati del kernel soggette a problemi analoghi sono quelle per l’allocazione della memoria, per la gestione delle interruzioni e le liste dei processi. La responsabilità di preservare il sistema operativo da simili problemi compete a chi sviluppa il kernel.

Il problema della sezione critica può essere risolto in maniera semplice in un ambiente single-core, impedendo che si verifichino interruzioni durante la modifica di una variabile condivisa. 
In questo modo, saremmo sicuri che l’attuale sequenza di istruzioni sia eseguita in ordine, senza prelazione. 
Visto che non verranno eseguite altre istruzioni sarà impossibile apportare modifiche inaspettate a una variabile condivisa.

Sfortunatamente questa soluzione non è praticabile in un ambiente multiprocessore. 
Disabilitare gli interrupt su un multiprocessore può richiedere infatti molto tempo, poiché il messaggio viene passato a tutti i processori. 
Questo invio di messaggi ritarda l’ingresso in ciascuna sezione critica e l’efficienza del sistema diminuisce. 
Va inoltre tenuto in considerazione l’effetto sul clock di sistema nel caso in cui il clock venga aggiornato dalle interruzioni.

La due strategie principali per la gestione delle sezioni critiche nei sistemi operativi sono: **kernel con diritto di prelazione e kernel senza diritto di prelazione**.
	Un **kernel con diritto di prelazione** consente che un processo funzionante in modalità di sistema sia sottoposto a prelazione, rinviandone in tal modo l’esecuzione.
	Un **kernel senza diritto di prelazione** non consente di applicare la prelazione a un processo attivo in modalità di sistema.
	
Ovviamente, i kernel senza diritto di prelazione sono immuni da race condition sulle strutture dati del kernel, visto che un solo processo per volta impegna il kernel.
Altrettanto non si può dire dei kernel con diritto di prelazione, motivo per cui bisogna avere cura, nella progettazione, di mantenerli al riparo dai problemi nell’accesso alle strutture dati del kernel. 

I kernel con diritto di prelazione presentano particolari difficoltà di progettazione quando sono destinati ad architetture smp, poiché in tali ambienti due processi nella modalità di sistema possono essere eseguiti in contemporanea su core differenti.

### Riassuntino:
Il problema della sezione critica consiste nelle incoerenze che si vanno a creare quando una memoria viene condivisa da due o piú processi.
La lettura e la scrittura di questa memoria da parte di due processi che lavorano in parallelo puó causare problemi di sincronizzazione se avviene nello stesso istante.
Per esempio la creazione di processi con la chiamata di sistema fork(), se due processi eseguono questa chiamata nello stesso tempo, e fanno richiesta di un pid libero allo stesso tempo si puó verificare che i due processi figli abbiano lo stesso pid.
Quando piú processi vogliono accedere ad una risorsa contemporanemanete si vengono a generare delle race condition.

Nei sistemi a singolo core, singola CPU, il problema critico non sussiste poiché si possono disabilitare le interrupt in sezioni di codice dove avviene la lettura o scrittura di memoria condivisa.
Nei sistemi multiprocessore il problema sussiste e non puó essere risolto disabilitando le interruzioni durante le sezioni critiche poiché ció andrebbe a generare latenza e problemi.

Per risolvere il problema della sezione critica si devono soddisfare tre requisiti:
Mutua esclusione
Progresso
Attesa limitata

Mutua esclusione: Se un processo é in esecuzione nella sua zona critica nessun altro processo puó essere in esecuzione nella sua zona critica.

Progresso: Se 