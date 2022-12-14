I dispositivi nvm stanno acquisendo un’importanza sempre maggiore. In sostanza, questi dispositivi sono elettrici invece che meccanici e, nella maggior parte dei casi, sono composti da un controllore e da diversi chip di memoria a semiconduttore nand flash utilizzati per memorizzare i dati. 
Esistono altre tecnologie nvm, come le dram dotate di una batteria di backup che permette di non perdere il contenuto o altre tecnologie basate su semiconduttori come le 3D XPoint, ma sono molto meno comuni e per questa ragione non verranno trattate in questo libro.

#### 11.1.2.1 Panoramica dei dispositivi NVM
I dispositivi nvm basati su memoria flash vengono spesso inseriti in contenitori simili a unità disco, e per questa ragione sono chiamati dischi a stato solido, o ssd (Figura 11.3). In altri casi, un dispositivo nvm può assumere la forma di un’unità usb (nota anche come _pen drive_ o _unità flash_) o di un modulo dram. In dispositivi come gli smartphone le nvm sono montate sulla superficie delle schede madri come dispositivo principale di archiviazione. In qualunque forma si presenti, un dispositivo nvm si comporta e può essere trattato allo stesso modo. La nostra discussione sui dispositivi nvm si concentra su questa tecnologia di memorizzazione.

I dispositivi nvm possono essere più affidabili dei dischi rigidi, perché non hanno parti mobili, e possono essere più veloci, perché non hanno tempo di posizionamento o latenza di rotazione. Inoltre, consumano meno energia. Per contro, sono più costosi (per megabyte) rispetto ai dischi rigidi tradizionali e hanno una capacità inferiore rispetto ai dischi rigidi più grandi presenti sul mercato. Nel corso del tempo, tuttavia, la capacità dei dispositivi nvm è aumentata più rapidamente rispetto a quella dei dischi rigidi e il loro prezzo è diminuito maggiormente; il loro utilizzo è quindi in continuo aumento e gli ssd, o dispositivi simili, sono ora utilizzati in alcuni computer portatili per renderli più piccoli, più veloci e più efficienti dal punto di vista energetico.

Poiché i dispositivi nvm possono essere molto più veloci rispetto ai dischi fissi, le interfacce bus standard possono costituire un limite importante al throughput e alcuni dispositivi nvm sono progettati per connettersi direttamente al bus di sistema (a un bus pcie, per esempio). La tecnologia nvm sta cambiando anche altri aspetti tradizionali del progetto di un’architettura. Alcuni sistemi usano dispositivi nvm come sostituto diretto delle unità disco, mentre altri li usano come un nuovo livello di cache, spostando i dati tra dischi magnetici, nvm e memoria principale per ottimizzare le prestazioni.

Le caratteristiche dei semiconduttori nand portano alcune nuove sfide che riguardano memorizzazione e affidabilità. 
Per esempio, possono essere letti e scritti a livello di pagina (l’analogo di un settore di un disco), ma i dati non possono essere sovrascritti senza che le celle nand siano prima cancellate. 
La cancellazione, che si verifica a livello di blocchi della dimensione di diverse pagine, richiede molto più tempo di una lettura (l’operazione più veloce) o di una scrittura (più lenta della lettura, ma molto più veloce della cancellazione). Il problema è però alleviato dal fatto che i dispositivi flash nvm sono composti da molte piastrine, dette die, ciascuna con molti percorsi dati (datapath), e le operazioni possono quindi avvenire in parallelo (ciascuna su un percorso dati). 
I semiconduttori nand, inoltre, si deteriorano a ogni ciclo di cancellazione e dopo circa 100.000 cicli (il numero specifico varia a seconda del supporto) le celle non sono più in grado di conservare i dati. 
A causa dell’usura nella scrittura, e poiché non vi sono parti in movimento, la durata delle nvm nand non viene misurata in anni, ma in numero di scritture per giorno sull’unità (dwpd, _Drive Writes per Day_). 
Tale numero indica quante volte al giorno l’intera capacità dell’unità può essere scritta prima che l’unità si guasti. 
Per esempio, su un dispositivo nand da 1 tb con una classificazione di 5 dwpd dovrebbe essere possibile scrivere 5 tb al giorno per tutto il periodo di garanzia senza che si verifichino errori.

Queste limitazioni hanno portato allo sviluppo di diversi algoritmi di miglioramento che, fortunatamente, vengono di solito implementati nel controllore del dispositivo nvm e non sono di interesse per il sistema operativo. Il sistema operativo si limita semplicemente a leggere e scrivere blocchi logici, mentre il dispositivo si occupa dell’effettiva realizzazione delle operazioni. Tuttavia, i dispositivi nvm sono soggetti a variazioni delle prestazioni dovute ai loro algoritmi operativi e sarà quindi indispensabile una breve discussione su ciò che fa il controllore.

#### 11.1.2.2 Algoritmi del controllore delle NAND Flash
Poiché i semiconduttori nand non possono essere sovrascritti, sono di solito presenti pagine che contengono dati non validi. 
Considerate un blocco del file system scritto una volta e in seguito riscritto. Se nel frattempo non si è verificata alcuna cancellazione, la pagina scritta per prima contiene vecchi dati, che ora non sono più validi, mentre la seconda pagina ha la versione attuale e valida del blocco. 
Un blocco nand contenente pagine valide e non valide è mostrato nella seguente figura. 
![[Pasted image 20221214193446.png]]
Per tenere traccia di quali blocchi logici contengono dati validi, il controllore mantiene una tabella di traduzione flash (ftl, _flash translation layer_), che tiene traccia delle pagine fisiche contenenti blocchi logici validi e dello stato del blocco fisico, ovvero dei blocchi che contengono solo pagine non valide e pertanto cancellabili.