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


### 