Per il sistema operativo la localizzazione di un offset all’interno di un file può essere complicata. 
I dischi hanno una dimensione dei blocchi ben definita, determinata dalla dimensione di un settore. Tutti gli i/o su disco si eseguono in unità di un blocco (record fisico), e tutti i blocchi hanno la stessa dimensione.
È improbabile che la dimensione del record fisico corrisponda esattamente alla lunghezza del record logico desiderato, che può anche essere variabile. Una soluzione diffusa per questo tipo di problema consiste nell’impaccamento di un certo numero di record logici in blocchi fisici.

Il sistema operativo unix, per esempio, definisce tutti i file semplicemente come un flusso di byte. A ciascun byte si può accedere in modo individuale tramite il suo offset a partire dall’inizio, o dalla fine, del file.
In questo caso il record logico è un byte. Il file system _impacca_ automaticamente i byte in blocchi fisici (per esempio 512 byte per blocco) com’è necessario.

La dimensione dei record logici, quella dei blocchi fisici e la tecnica d’impaccamento determinano il numero dei record logici all’interno di ogni blocco fisico. L’impaccamento può essere fatto dal programma applicativo dell’utente oppure dal sistema operativo.

In entrambi i casi il file si può considerare come una sequenza di blocchi. Tutte le funzioni di i/o di base operano in termini di blocchi. La conversione da record logici a blocchi fisici è un problema di programmazione relativamente semplice.

Poiché lo spazio del disco è sempre assegnato in blocchi, una parte dell’ultimo blocco di ogni file in genere è sprecata. Se ogni blocco è composto di 512 byte, a un file di 1949 byte si assegnano quattro blocchi (2048 byte); gli ultimi 99 byte sono sprecati. I byte sprecati, a causa della gestione in multipli di blocchi invece che di ­byte, costituiscono la frammentazione interna. Tutti i file system ne soffrono; maggiore è la dimensione dei blocchi, maggiore sarà la frammentazione interna.