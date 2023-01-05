I dati vengono controllati dal DBMS e dall’applicazione, ma in genere le regole sui dati vengono controllate solo dal DBMS. Queste regole prendono il nome di vincolo di integrità, che devono essere rispettate da tutte le righe (tuple) di una tabella. Tra questi vincoli vi sono quelli per la definizione delle chiavi, tra cui la chiave primaria, e quelli che impongono delle regole sui valori assunti da due o più colonne. 
Ogni vincolo può essere visto come un predicato che associa ad ogni istanza il valore vero o falso. Se il predicato assume il valore vero, allora diciamo che l’istanza soddisfa il vincolo.

Abbiamo diversi tipi di vincoli: 
- Vincolo intrarelazionale: 
	è un vincolo che definisce una singola relazione, ad esempio se ho una tabella “STUDENTE” ed inserisco una matricola, devo assicurarmi che nessun altro ha la stessa matricola scorrendo tutta la tabella. 
	- vincolo di tupla: 
		è un vincolo che può essere valutato su ciascuna tupla indipendentemente dalle altre; ad esempio se devo inserire una lode, vado a guardare semplicemente la tupla voto. La sintassi permette di definire espressioni booleane (AND, OR, NOT) che confrontano con gli operatori di uguaglianza, disuguaglianza e ordinamento, valori di attributo o espressioni aritmetiche su valori di attributo. 
		
	- vincolo di chiave: 
		sono i più importanti vincoli intrarelazionali, alla base del modello. Ad esempio, matricola non esistono due studenti con lo stesso numero di matricola. 
		
- Vincolo interrelazionale: 
	è un vincolo che coinvolge due o più relazioni. Per vedere se una regola è soddisfatta (all'interno di una tabella) bisogna andare ad analizzare un'altra tabella.


### 4.4.1 Chiavi
I vincoli di chiave sono i più importanti del modello relazionale. Una chiave è un insieme di attributi che identificano univocamente una tupla di una relazione. Ciascuna relazione e ciascuno schema di relazione ha sempre una chiave: in ogni relazione deve esistere una ed una sola chiave primaria (primary key), ovvero una chiave che non contiene valori nulli (NULL).

In una tabella possono esserci molte chiavi ma soltanto una è anche una chiave primaria. Tutte le altre chiavi sono dette chiavi secondarie (foreign key).
- Un insieme di attributi K si dice “superchiave” per la relazione r se r non contiene due tuple 𝑡1 e 𝑡2 tali che 𝑡1[𝑘] = 𝑡2[𝑘]. Un insieme di attributi è una superchiave se e solo se non contiene tuple duplicate al suo interno. 
- Un insieme di attributi si dice chiave se è una “superchiave minimale”, ossia se non contiene altre superchiavi al suo interno.

### 4.4.2 Chiavi e valori nulli 
Bisogna evitare di creare valori nulli sulle chiavi o sarebbe impossibile distinguere due righe di una tabella. Gli attributi che costituiscono la chiave primaria vengono spesso evidenziate attraverso la sottolineatura.

### 4.4.3 Vincoli di integrità referenziali 
Un vincolo di integrità referenziale è la classe più importante tra i vincoli interrelazionali. 
Coinvolgono le relazioni esistenti tra le tabelle di base dello schema logico.
Questo tipo di vincolo può essere applicato sia a una relazione uno a molti, dichiarando esplicitamente la chiave esterna nella tabella esterna (lato molti) sia a una relazione uno a uno, considerata come caso particolare di quella uno a molti, in cui una delle due chiavi primarie è anche la chiave esterna. 
Sia un insieme di attributi X su 𝑅1 e su 𝑅2, un vincolo referenziale è verificato se i valori di X di ogni tupla 𝑅1 compaiono come valori di Y di 𝑅2, in genere Y è la chiave primaria di 𝑅2. 
Questo vincolo si rappresenta come una freccia che va dalla tabella interna verso la tabella esterna