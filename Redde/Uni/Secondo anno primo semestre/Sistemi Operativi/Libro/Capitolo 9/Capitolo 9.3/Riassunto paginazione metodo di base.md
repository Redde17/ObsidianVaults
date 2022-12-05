Bisogna tenere conto che quando si parla di memoria si tiene in considerazione la memoria volatile /RAM di un elaboratore.

Per realizzare la paginazione con il metodo di base dividiamo la memoria in fisica e logica secondo i seguenti criteri:
La **memoria fisica** viene suddivisa in **frame** ovvero blocchi di dimensione fissa.
La **memoria logica** viene suddivisa in **pagine** ovvero blocchi di pari dimensioni.

Quando si deve eseguire un processo le sue **pagine** vengono caricate in memoria nei **frame** liberi.
Le pagine risiedono nella memoria ausiliare o nel file system.
La memoria ausiliare é a sua volta divisa in blocchi di dimensione fissa

Questa metodologia di gestione della memoria permette di separare gli indirizzi logici da quelli fisici e permettere ad esempio, ad un processo di avere uno spazio degli indirizzi logici a 64 bit nonostante il sistema ha meno di $2^{64}$.  