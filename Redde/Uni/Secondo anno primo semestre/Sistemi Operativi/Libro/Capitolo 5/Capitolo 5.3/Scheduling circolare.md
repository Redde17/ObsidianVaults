L’algoritmo di scheduling circolare (_round-robin_, rr) è simile allo scheduling fcfs, ma aggiunge la capacità di prelazione in modo che il sistema possa commutare fra i vari processi.

Ciascun processo riceve una piccola quantità fissata del tempo della cpu, chiamata quanto di tempo o porzione di tempo (_time slice_), che varia generalmente da 10 a 100 millisecondi; la ready queue è trattata come una coda circolare.

Lo scheduler della cpu scorre la ready queue, assegnando la cpu a ciascun processo per un intervallo di tempo della durata massima di un quanto di tempo.

Per implementare lo scheduling rr si gestisce la ready queue come una coda fifo. I nuovi processi si aggiungono alla fine della ready queue. Lo scheduler della cpu prende il primo processo dalla ready queue, imposta un timer in modo che invii un segnale d’interruzione alla scadenza di un intervallo pari a un quanto di tempo, e attiva il dispatcher per eseguire il processo.

A questo punto si può verificare una delle due seguenti situazioni: 
Il processo ha una sequenza di operazioni della cpu di durata minore di un quanto di tempo, quindi il processo stesso rilascia volontariamente la cpu e lo scheduler passa al processo successivo della ready queue;
Oppure la durata della sequenza di operazioni è più lunga di un quanto di tempo; in questo caso il timer scade e invia un segnale d’interruzione al sistema operativo, che esegue un cambio di contesto e mette il processo alla fine della ready queue. Lo scheduler quindi seleziona il processo successivo nella ready queue.

Il tempo d’attesa medio per il criterio di scheduling rr è spesso abbastanza lungo. Si consideri il seguente insieme di processi che si presenta al tempo 0, con la durata delle sequenze di operazioni della cpu espressa in millisecondi:
![[Pasted image 20221105164204.png]]
Se si usa un quanto di tempo di 4 millisecondi, il processo _P1 ottiene i primi 4 millisecondi ma, poiché richiede altri 20 millisecondi, è soggetto a prelazione dopo il primo quanto di tempo e la cpu passa al processo successivo della coda, il processo _P2. 
Poiché il processo _P2 non necessita di 4 millisecondi, termina prima che il suo quanto di tempo si esaurisca, così si assegna immediatamente la cpu al processo successivo, il processo _P3. 
Una volta che tutti i processi hanno ricevuto un quanto di tempo, si assegna nuovamente la cpu al processo _P1 per un ulteriore quanto di tempo. 
Dallo scheduling rr risulta quanto segue.
![[Pasted image 20221105164321.png]]
Calcoliamo ora il tempo di attesa medio per questa sequenza. 
P1 resta in attesa per 6 millisecondi (10 – 4), P2 per 4 millisecondi e P3 per 7 millisecondi. 
**Il tempo d’attesa medio è di 17/3 = 5,66 millisecondi.**

Nell’algoritmo di scheduling rr la cpu si assegna a un processo per non più di un quanto di tempo per volta (a meno che questo sia l’unico processo ready).
Se la durata della sequenza di operazioni della cpu di un processo eccede il quanto di tempo, il processo viene sottoposto a prelazione e riportato nella ready queue. 
**L’algoritmo di scheduling rr è pertanto con prelazione.**

**Le prestazioni dell’algoritmo rr dipendono molto dalla dimensione del quanto di tempo**.
Nel caso limite in cui il quanto di tempo sia molto lungo, il criterio di scheduling rr si riduce al criterio di scheduling fcfs. Se il quanto di tempo è molto breve (per esempio, un millisecondo), il criterio rr può portare a un numero elevato di cambi di contesto. Assumiamo che, per esempio, ci sia un solo processo della durata di 10 unità di tempo, se il quanto di tempo è di 12 unità, il processo impiega meno di un quanto di tempo; se però il quanto di tempo è di 6 unità, il processo richiede 2 quanti di tempo e un cambio di contesto; e se il quanto di tempo è di un’unità di tempo, occorrono nove cambi di contesto, con proporzionale rallentamento dell’esecuzione del processo.
![[Pasted image 20221105164616.png]]

Quindi il quanto di tempo deve essere ampio rispetto alla durata del cambio di contesto; se, per esempio, questa è pari al 10 per cento del quanto di tempo, allora s’impiega in cambi di contesto circa il 10 per cento del tempo d’elaborazione della cpu. In pratica, nella maggior parte dei sistemi moderni un quanto di tempo va dai 10 ai 100 millisecondi. Il tempo richiesto per un cambio di contesto non eccede solitamente i 10 microsecondi, risultando quindi una modesta frazione del quanto di tempo.

Anche il tempo di completamento (_turnaround time_) dipende dalla dimensione del quanto di tempo: com’è evidenziato nella Figura 5.6, il tempo di completamento medio di un insieme di processi non migliora necessariamente con l’aumento della dimensione del quanto di tempo. In generale, il tempo di completamento medio può migliorare se la maggior parte dei processi termina la successiva sequenza di operazioni della cpu in un solo quanto di tempo. Per esempio, dati tre processi della durata di 10 unità di tempo ciascuno e un quanto di una unità di tempo, il tempo di completamento medio è di 29 unità. Se però il quanto di tempo è di 10 unità, il tempo di completamento medio scende a 20 unità. Aggiungendo il tempo del cambio di contesto, con un piccolo quanto di tempo, il tempo di completamento medio aumenta ancora poiché sono richiesti più cambi di contesto.
![[Pasted image 20221105164759.png]]

Benché il quanto di tempo debba essere grande in confronto al tempo necessario al cambio di contesto, non deve essere tuttavia troppo grande. Se il quanto di tempo è molto ampio, il criterio di scheduling rr, come puntualizzato in precedenza, tende al criterio fcfs. Empiricamente si può stabilire che l’80 per cento delle sequenze di operazioni della cpu debba essere più breve del quanto di tempo.