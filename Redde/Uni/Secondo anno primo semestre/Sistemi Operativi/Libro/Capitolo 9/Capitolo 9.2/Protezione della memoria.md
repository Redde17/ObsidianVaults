Prima di trattare l’allocazione della memoria, dobbiamo soffermarci sul problema della protezione della memoria. Possiamo evitare che un processo acceda alla memoria che non gli appartiene combinando due idee discusse in precedenza. 
Se abbiamo un sistema con un registro di rilocazione (Paragrafo 9.1.3) e un registro limite (Paragrafo 9.1.1) abbiamo già raggiunto il nostro obiettivo. 
Il registro di rilocazione contiene il valore dell’indirizzo fisico minore; il registro limite contiene l’intervallo di indirizzi logici, per esempio, _rilocazione_ = 100.040 e _limite_ = 74.600. Ogni indirizzo logico deve cadere nell’intervallo specificato dal registro limite; la mmu fa corrispondere _dinamicamente_ l’indirizzo fisico all’indirizzo logico sommando a quest’ultimo il valore contenuto nel registro di rilocazione, e invia l’indirizzo risultante alla memoria.
![[Pasted image 20221130162346.png]]

Quando lo scheduler della cpu seleziona un processo per l’esecuzione, il dispatcher, durante l’esecuzione del cambio di contesto, carica il registro di rilocazione e il registro limite con i valori corretti. 
Poiché si confronta ogni indirizzo generato dalla cpu con i valori contenuti in questi registri, si possono proteggere il sistema operativo, i programmi e i dati di altri utenti da tentativi di modifiche da parte del processo in esecuzione.

Lo schema con registro di rilocazione consente al sistema operativo di cambiare dinamicamente le proprie dimensioni. 
Tale flessibilità è utile in molte situazioni; il sistema operativo, per esempio, contiene codice e spazio di memoria per i driver dei dispositivi. Se un driver di periferica non è attualmente in uso, ha poco senso mantenerlo in memoria. 
È meglio, invece, caricarlo in memoria solo quando è necessario e rimuoverlo quando non lo è più, destinando la sua memoria ad altre esigenze.