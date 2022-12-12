Si consideri il caricamento in memoria di un eseguibile residente su disco.
Una possibilità è quella di caricare l’intero programma nella memoria fisica al momento dell’esecuzione. 

Il problema, però, è che all’inizio non è detto che serva avere tutto il programma in memoria: se il programma, per esempio, fornisce all’avvio una lista di opzioni all’utente, è inutile caricare il codice per l’esecuzione di _tutte_ le opzioni previste, senza tener conto di quella effettivamente scelta dall’utente.

Una strategia alternativa consiste nel caricare le pagine nel momento in cui servono realmente; si tratta di una tecnica, detta **paginazione su richiesta**, comunemente adottata dai sistemi con memoria virtuale.
Secondo questo schema, le pagine sono caricate in memoria solo quando richieste durante l’esecuzione del programma: ne consegue che le pagine cui non si accede mai non sono mai caricate nella memoria fisica.

I processi risiedono in memoria secondaria.
La paginazione su richiesta mostra uno dei principali vantaggi della memoria virtuale: 
**caricando solo le parti necessarie dei programmi la memoria viene utilizzata in modo più efficiente**.

### 10.2.1 [[Concetti fondamentali]]
### 10.2.2 [[Lista dei frame liberi]]
### 10.2.3 [[Prestazioni della paginazione su richiesta]]