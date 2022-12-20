## Memoria
Il candidato descriva un algoritmo, a sua scelta, per la sostituzione di pagine che fornisca una approssimazione del LRU
	I tre possibili algoritmi che forniscono un approssimazione del LRU sono
	Approssimazione con bit supplementari di riferimento
	Seconda chance 
	Seconda chance migliorato
	Il primo approssima l'LRU leggendo i bit di rifermento ad intervalli per estrarne informazioni riguardanti l'ultimo utilizzo della pagina. Questo bit puó formare una tabella che puó indicare da quanto tempo non viene utilizzato
	Il secondo algoritmo consiste nello scorrere la lista di pagine in memoria come se fossero una lista concatenata e usufruire di un bit di validitá per vedere se la pagina é stata usata di recente o meno, se il bit é impostato a 0 la pagina viene sostituita, se il bit é impostato a 1 allora alla pagina si da una seconda chance e si resetta il valore del bit a 0. Questa tecnica permette alle pagine usate di recente di rimanere in memoria e se vengono usate spesso da mantere il bit di verifica ad 1 non verranó mai tolte dalla memoria
	La sostituzione per seconda chance migliorata prevede di unire al bit di verifica e uno di modifica e considerarli entrambi per decidere la migliore pagina da scaricare dalla memoria, di conseguenza la miglior pagina da scaricare sarebbe una che non é stata ne modificata e ne utilizzata nell'ultimo ciclo di lista, poi segue le pagine o solo utilizzate o solo modificate e per ultimo una pagina sia modificata che usata