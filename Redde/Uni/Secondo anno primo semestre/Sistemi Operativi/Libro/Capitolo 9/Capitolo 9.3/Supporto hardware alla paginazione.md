Poiché ogni processo ha la sua tabella delle pagine, un puntatore alla tabella di pagina viene memorizzato insieme ai valori di altri registri nel **_process control block_** di ciascun processo.
Quando lo scheduler della cpu seleziona un processo per l’esecuzione, deve ricaricare i registri utente e i valori appropriati della tabella delle pagine hardware dalla tabella delle pagine utente memorizzata.

L’implementazione hardware della tabella delle pagine si può realizzare in modi diversi. Nel caso più semplice è implementata come un insieme di registri hardware dedicati ad alta velocità, così da rendere la traduzione dell’indirizzo molto efficiente. Tuttavia, questo approccio aumenta il tempo dei cambi di contesto, poiché durante un cambio di contesto ogni registro dovrà essere scambiato.

L’uso di registri per la tabella delle pagine è efficiente se la tabella stessa è ragionevolmente piccola, nell’ordine, per esempio, di 256 elementi. 
Però la maggior parte dei calcolatori contemporanei usa tabelle molto grandi, per esempio di un milione di elementi.
Quindi **non si possono impiegare i registri veloci per realizzare la tabella delle pagine**; quest’ultima viene invece mantenuta nella memoria principale e un registro di base della tabella delle pagine (_page-table base register_, ptbr) punta alla tabella stessa. 
Il cambio della tabelle delle pagine richiede soltanto di modificare questo registro, riducendo considerevolmente il tempo dei cambi di contesto.