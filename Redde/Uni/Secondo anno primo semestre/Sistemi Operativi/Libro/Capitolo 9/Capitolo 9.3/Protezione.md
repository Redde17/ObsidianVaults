In un ambiente paginato, la protezione della memoria è assicurata dai bit di protezione associati a ogni frame; normalmente tali bit si trovano nella tabella delle pagine.

Un bit può determinare se una pagina si può leggere e scrivere oppure soltanto leggere.
Tutti i riferimenti alla memoria passano attraverso la tabella delle pagine per trovare il numero corretto del frame; quindi mentre si calcola l’indirizzo fisico, si possono controllare i bit di protezione per verificare che non si scriva in una pagina di sola lettura. 
Un tale tentativo causerebbe la generazione di un’eccezione hardware per il sistema operativo, si avrebbe cioè una violazione della protezione della memoria.

Questo metodo si può facilmente estendere per fornire un livello di protezione più perfezionato. 
Si può progettare un hardware che fornisca la protezione di sola lettura, di sola scrittura o di sola esecuzione. 
In alternativa, con bit di protezione distinti per ogni tipo d’accesso, si può ottenere una qualsiasi combinazione di tali tipi d’accesso; i tentativi illegali causano la generazione di un’eccezione per il sistema operativo.

Di solito si associa a ciascun elemento della tabella delle pagine un ulteriore bit, detto bit di validità. Tale bit, impostato a _valido_, indica che la pagina corrispondente è nello spazio d’indirizzi logici del processo, quindi è una pagina valida; impostato a _non valido_, indica che la pagina non è nello spazio d’indirizzi logici del processo.
Il bit di validità consente quindi di riconoscere gli indirizzi illegali e di notificarne la presenza attraverso un’eccezione. Il sistema operativo concede o impedisce l’accesso a una pagina impostando in modo appropriato tale bit.