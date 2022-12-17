I calcolatori fanno funzionare un gran numero di tipi di dispositivi.
La maggior parte rientra nella categoria dei dispositivi di memorizzazione (dischi, nastri), dispositivi di trasmissione (connessioni di rete, Bluetooth), interfacce uomo-macchina (schermi, tastiere, mouse, ingressi e uscite audio). 
Altri dispositivi sono più specializzati, come i dispositivi di pilotaggio di un caccia a reazione.

Un dispositivo comunica con un sistema elaborativo inviando segnali attraverso un cavo o attraverso l’etere e comunica con il calcolatore tramite un punto di connessione (porta), per esempio una porta seriale. 
Se più dispositivi condividono un insieme di fili, la connessione è detta _bus_. Un bus è un insieme di fili e un protocollo rigorosamente definito che specifica l’insieme dei messaggi che si possono inviare attraverso i fili. 
In termini elettronici, i messaggi si inviano tramite configurazioni di livelli di tensione elettrica applicate ai fili con una definita scansione temporale. 
Quando un dispositivo _A_ ha un cavo che si connette a un dispositivo _B_ e il dispositivo _B_ ha un cavo che si connette a un dispositivo _C_ che a sua volta è collegato a una porta di un calcolatore, si ottiene il cosiddetto collegamento in daisy chain, che di solito funziona come un bus.

I bus sono ampiamente usati nell’architettura dei calcolatori e differiscono tra loro per formato dei segnali, velocità, throughput e metodo di connessione. 
La seguente figura mostra una tipica struttura di bus di pc; si tratta di un bus pcie (il comune bus di sistema dei pc) che connette il sottosistema cpu-memoria ai dispositivi veloci, e di un bus d’espansione cui si connettono i dispositivi relativamente lenti come la tastiera e le porte seriali e usb.
![[Pasted image 20221217194802.png]]
Nella parte inferiore sinistra della figura quattro dischi sono collegati a un bus sas (_serial-attached_ _scsi_) inserito nel relativo controllore. 
Il bus pcie è un bus flessibile che invia i dati su uno o più canali, ciascuno composto da due coppie di fili, una coppia per la ricezione dei dati e l’altra per la trasmissione. 
Ogni canale è quindi formato da quattro fili e viene utilizzato come flusso di byte full duplex, che trasporta pacchetti di dati a gruppi di otto bit contemporaneamente in entrambe le direzioni. Fisicamente, i collegamenti pcie possono contenere 1, 2, 4, 8, 12, 16 o 32 canali e il numero di canali viene indicato col prefisso “x”. 
Per esempio, una scheda o un connettore pcie che utilizza 8 canali viene indicato con x8. Inoltre, il bus pcie ha attraversato più “generazioni”, e nuove generazioni del bus arriveranno in futuro. Quindi, per esempio, una scheda potrebbe essere denominata “pcie gen3 x8”, per indicare che funziona con la generazione 3 di pcie e utilizza 8 canali. 
Un dispositivo del genere ha un throughput massimo di 8 gigabyte al secondo.

Un controllore è un insieme di componenti elettronici che può far funzionare una porta, un bus o un dispositivo. 
Un controllore di porta seriale è un semplice controllore di dispositivo; si tratta di un singolo circuito integrato (o di una sua parte) nel calcolatore che controlla i segnali presenti nei fili della porta seriale. 
Per contro un controllore fc (_fibre channel_) non è semplice; poiché il protocollo fc è complesso e utilizzato nei data center anziché nei pc, il controllore del bus fc è spesso realizzato come una scheda hardware separata o come un adattatore bus-host (hba, _host bus adapter_) che si collega a un bus nel computer. 
Esso contiene generalmente un’unità d’elaborazione, microcodice, e memoria privata che gli consentono di elaborare i messaggi del protocollo fc. 
Alcuni dispositivi sono dotati di propri controllori incorporati. Osservando un’unità a disco si vede, da un lato, una scheda elettronica a essa agganciata; si tratta del controllore che attua la parte lato disco del protocollo di qualche tipo di connessione, per esempio sas o sata (_serial advanced technology attachment_). Ha un’unità d’elaborazione e microcodice per l’esecuzione di molti compiti, come localizzazione dei settori difettosi, prelievo anticipato (_prefetching_), gestione del buffer e della cache.