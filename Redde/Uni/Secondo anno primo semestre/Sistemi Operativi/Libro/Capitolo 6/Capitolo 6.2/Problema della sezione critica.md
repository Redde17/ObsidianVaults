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
In questa situazione, due processi _P0 e _P1 creano processi figlio (child) utilizzando la chiamata di sistema fork(). Ricordiamo dal Paragrafo 3.3.1 che fork() restituisce al processo genitore l’identificatore di processo (pid) del processo appena creato. In questo esempio, c’è una race condition sulla variabile del kernel next_available_pid, che contiene il valore del prossimo pid disponibile. In assenza di mutua esclusione è possibile che lo stesso pid venga assegnato a due processi distinti.
