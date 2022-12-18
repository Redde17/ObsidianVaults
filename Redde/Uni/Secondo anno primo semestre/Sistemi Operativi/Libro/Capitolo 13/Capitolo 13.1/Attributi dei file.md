Per comodità degli utenti, ogni file ha un nome che si usa come riferimento. Un nome, di solito, è una sequenza di caratteri come esempio.c. 
Alcuni sistemi, per quel che riguarda i nomi, distinguono le lettere maiuscole dalle minuscole, altri le considerano equivalenti. Una volta ricevuto il nome, il file diviene indipendente dal processo, dall’utente, e anche dal sistema da cui è stato creato. Per esempio, un utente potrebbe creare il file esempio.c e un altro utente potrebbe modificarlo specificandone il nome. Il proprietario del file potrebbe registrare il file in una chiavetta usb, inviarlo per posta elettronica come allegato o copiarlo attraverso la rete, ed esso potrebbe ancora chiamarsi esempio.c nel sistema di destinazione. A meno che non ci sia un metodo di condivisione e sincronizzazione, questa seconda copia è ora indipendente dalla prima e può essere modificata separatamente.

Un file ha attributi che possono variare secondo il sistema operativo, ma che tipicamente comprendono i seguenti.
-   Nome. 
	Il nome simbolico del file è l’unica informazione in forma umanamente leggibile.
-   Identificatore. 
	Si tratta di un’etichetta unica, di solito un numero, che identifica il file all’interno del file system; è il nome impiegato dal sistema per il file.
-   Tipo. 
	Questa informazione è necessaria ai sistemi che gestiscono tipi di file diversi.
-   Locazione. 
	Si tratta di un puntatore al dispositivo e alla locazione del file in tale dispositivo.
-   Dimensione. 
	Si tratta della dimensione corrente del file (in byte, parole o blocchi) ed eventualmente della massima dimensione consentita.
-   Protezione. 
	Le informazioni di controllo degli accessi controllano chi può leggere, scrivere o eseguire il file.
-   Ora, data e identificazione dell’utente. 
	Queste informazioni possono essere relative alla creazione, l’ultima modifica e l’ultimo uso. Questi dati possono essere utili ai fini della protezione, della sicurezza e del monitoraggio del suo utilizzo.

Alcuni file system più recenti supportano anche gli attributi estesi dei file, tra cui la codifica dei caratteri del file e funzioni di sicurezza come la checksum.

Le informazioni sui file sono conservate nella struttura della directory, che risiede sullo stesso dispositivo dove sono memorizzati i file. 
Di solito un elemento di directory consiste di un nome di file e di un identificatore unico, che a sua volta individua gli altri attributi del file.
Un elemento di directory può richiedere più di un kilobyte per contenere queste informazioni per ciascun file. In un sistema con molti file, la dimensione della stessa directory può essere dell’ordine dei megabyte o dei gigabyte. 
Poiché le directory, come i file, devono essere non volatili, si devono registrare sul dispositivo di memorizzazione di massa e caricare in memoria centrale un po’ per volta, secondo le necessità.