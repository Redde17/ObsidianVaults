I dischi costituiscono la maggior parte della memoria secondaria in cui si conservano i file system. Hanno due caratteristiche importanti che ne fanno un mezzo adatto a questo scopo:
1.  si possono riscrivere localmente; si può leggere un blocco dal disco, modificarlo e quindi scriverlo nella stessa posizione;
2.  è possibile accedere direttamente a qualsiasi blocco di informazioni del disco, quindi risulta semplice accedere a qualsiasi file, sia in modo sequenziale sia in modo diretto, e passare da un file all’altro spostando le testine di lettura e scrittura e attendendo la rotazione del disco.

I dispositivi nvm sono sempre più utilizzati per l’archiviazione dei file e su di essi vengono quindi creati dei file system.
Questi dispositivi differiscono dagli hard disk, in quanto non possono essere riscritti direttamente e presentano differenti performance.

Per migliorare l’efficienza dell’i/o, i trasferimenti tra memoria centrale e dischi si eseguono per blocchi. Ciascun blocco è composto da uno o più settori. A seconda dell’unità a disco, la dimensione dei settori è compresa tra 32 byte e 4096 byte; di solito è pari a 512 byte o 4096 byte. I dispositivi nvm hanno normalmente blocchi di 4096 byte e utilizzano metodi di trasferimento simili a quelli delle unità disco.

Per fornire un efficiente e conveniente accesso al disco, il sistema operativo fa uso di uno o più file system che consentono di memorizzare, individuare e recuperare facilmente i dati. 
Un file system presenta due problemi di progettazione molto diversi.
Il primo riguarda la definizione dell’aspetto del file system agli occhi dell’utente. Questo compito implica la definizione di un file e dei suoi attributi, delle operazioni permesse su un file e della struttura delle directory per l’organizzazione dei file. 
Il secondo riguarda la creazione di algoritmi e strutture dati che permettano di far corrispondere il file system logico ai dispositivi fisici di memoria secondaria.

Lo stesso file system è generalmente composto da molti livelli distinti. La struttura illustrata nella seguente figura è un esempio di struttura stratificata. Ogni livello si serve delle funzioni dei livelli inferiori per crearne di nuove impiegate dai livelli superiori.
![[Pasted image 20221219190559.png]]

- Il livello più basso, **il controllo dell’i/o**,
	costituito dai driver dei dispositivi e dai gestori dei segnali d’interruzione, si occupa del trasferimento delle informazioni tra memoria centrale e memoria secondaria. Un driver di dispositivo si può concepire come un traduttore che riceva comandi ad alto livello, come “recupera il blocco 123”, e che emette istruzioni di basso livello dipendenti dall’hardware, usate dal controllore che fa da interfaccia tra i dispositivi di i/o e il resto del sistema. Un driver di dispositivo di solito scrive specifiche configurazioni di bit in specifiche locazioni della memoria del controllore di i/o per indicare quali azioni il dispositivo di i/o debba compiere, e su quali locazioni.