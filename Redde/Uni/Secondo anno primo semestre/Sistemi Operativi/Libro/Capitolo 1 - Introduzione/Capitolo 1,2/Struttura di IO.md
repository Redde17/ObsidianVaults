# Struttura di I/O
Una percentuale cospicua del codice di un sistema operativo è dedicata alla gestione dell’i/o; ciò è dovuto sia alla sua importanza per il progetto di un sistema affidabile ed efficiente, sia alla differente tipologia dei dispositivi.

*Un calcolatore general-purpose è composto da un insieme di dispositivi connessi mediante un bus comune.*

L’i/o guidato dalle [[Interruzioni]] è adatto al trasferimento di piccole quantità di dati, ma in caso di trasferimenti massicci può generare un **pesante sovraccarico (_overhead_)**; si pensi, per esempio, all’i/o da e verso nvs.
Per risolvere questo problema si utilizza le tecnica dell’accesso **diretto alla memoria (dma)**. Ovverò una volta che sono stati impostati i **buffer**, i **puntatori** e i **contatori** necessati al dispositivo di I/O, il controllore trasferisce un **intero blocco di dati** dal proprio buffer alla memoria centrale o viceversa senza intervento della CPU. **Questa operazione richiede un singolo interrupt per trasferimento piuttosto che per ogni byte** e permette alla CPU di rimanere libera di occuparsi di altri compiti durante l'operazione. 

Alcuni sistemi ad alte prestazioni hanno abbandonato la configurazione basata sul bus per adottare un’architettura incentrata sugli switch, in cui più dispositivi fisici possono interagire con varie parti del sistema concorrentemente, piuttosto che contendersi un unico bus condiviso. In questo caso, il dma risulta ancora più efficace.

![[Pasted image 20221006084443.png]]

