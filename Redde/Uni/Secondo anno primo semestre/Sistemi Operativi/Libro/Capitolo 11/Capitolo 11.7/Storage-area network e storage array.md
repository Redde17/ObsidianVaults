Uno svantaggio dei sistemi di memoria secondaria connessa alla rete è che le operazioni di i/o sulla memoria secondaria impegnano banda della rete e quindi aumentano la latenza della comunicazione nella rete. 
Questo problema può essere particolarmente grave per sistemi client-server di grandi dimensioni: l’ordinaria comunicazione tra i server e i client compete per la banda con la comunicazione tra i server e i dispositivi di memorizzazione.

Una storage-area network (san) è una rete privata (che impiega protocolli specifici per la memorizzazione anziché protocolli di rete) tra i server e le unità di memoria secondaria.
![[Pasted image 20221215202757.png]]
La potenza di una san sta nella sua flessibilità: si possono connettere alla stessa san molte macchine e molti storage array; la memoria può essere allocata alle macchine dinamicamente. Gli storage array possono essere protetti da raid o essere costituiti da unità non protette (jbod, _Just a Bunch of Disks_). Uno switch san permette di consentire o proibire l’accesso degli host allo spazio di archiviazione. Per esempio, la san può essere configurata per allocare più spazio di archiviazione a un host che sta esaurendo lo spazio su disco. Le san consentono ai cluster di server di condividere lo stesso storage e agli storage array di avere più connessioni dirette con gli host. Le san in genere hanno più porte e costano di più rispetto agli storage array. La connettività san avviene a breve distanza e in genere senza routing, quindi un nas può avere molti più host connessi rispetto a una san.

Uno storage array è un dispositivo costruito appositamente che può includere porte san, porte di rete o entrambe. Contiene inoltre unità per memorizzare dati e un controllore (o un set ridondante di controllori) per gestire l’archiviazione e consentire l’accesso storage attraverso le reti. I controllori sono composti da cpu, memoria e software che implementano le funzionalità dell’array, che possono comprendere protocolli di rete, interfacce utente, protezione raid, snapshot, replica, compressione, deduplicazione e crittografia.

Alcuni storage array includono dischi ssd: in alcuni casi sono composti esclusivamente da ssd, con prestazioni massime, ma capacità inferiore di archiviazione, in altri contengono un mix di ssd e hdd, con il software dell’array (o l’amministratore) che seleziona il supporto migliore per un dato utilizzo oppure con l’utilizzo degli ssd come cache e degli hdd come memoria di massa.

La soluzione più comune per il collegamento tramite san è il fc, anche se la diffusione di iscsi è in crescita, grazie alla sua semplicità. Una possibile alternativa è InfiniBand, un’architettura di bus specifica per san, che fornisce supporto hardware e software per reti d’interconnessione ad alta velocità tra server e unità di memoria secondaria.