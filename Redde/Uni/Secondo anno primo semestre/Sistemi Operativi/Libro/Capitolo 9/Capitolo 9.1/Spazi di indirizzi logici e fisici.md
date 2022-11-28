Un indirizzo generato dalla cpu è normalmente chiamato **indirizzo logico**, mentre un indirizzo visto dall’unità di memoria, cioè caricato nel registro dell’indirizzo di memoria (_memory address register_, mar) è normalmente chiamato **indirizzo fisico**.

I metodi di associazione degli indirizzi nelle fasi di compilazione e di caricamento producono **indirizzi logici e fisici identici**. 
Con il metodo di associazione nella fase d’esecuzione, invece, gli **indirizzi logici non coincidono con gli indirizzi fisici**. 
In questo caso ci si riferisce, di solito, agli indirizzi logici col termine indirizzi virtuali; in questo testo si usano tali termini in modo intercambiabile. 
L’insieme di tutti gli indirizzi logici generati da un programma è lo spazio degli indirizzi logici; l’insieme degli indirizzi fisici corrispondenti a tali indirizzi logici è lo spazio degli indirizzi fisici. Quindi, con lo schema di associazione degli indirizzi nella fase d’esecuzione, lo spazio degli indirizzi logici differisce dallo spazio degli indirizzi fisici.

L’associazione nella fase d’esecuzione dagli indirizzi virtuali agli indirizzi fisici è svolta da un dispositivo detto unità di gestione della memoria (_memory-management unit_, mmu), come mostrato nella seguente figura.
![[Pasted image 20221128163438.png]]
Come viene discusso nei Paragrafi dal 9.2 al 9.3, si può scegliere tra diversi metodi di realizzazione di tale associazione. 
Per ora illustriamo un semplice schema di associazione degli indirizzi tramite mmu, che è una generalizzazione dello schema con registro di base descritto nel Paragrafo 9.1.1.

Com’è illustrato nella seguente figura
![[Pasted image 20221128163539.png]] 
il registro di base è ora denominato registro di rilocazione: quando un processo utente genera un indirizzo, prima dell’invio all’unità di memoria, si somma a tale indirizzo il valore contenuto nel registro di rilocazione. 
Per esempio, se il registro di rilocazione contiene il valore 14000, un tentativo da parte dell’utente di accedere alla locazione 0 è dinamicamente rilocato alla locazione 14000; un accesso alla locazione 346 è mappato alla locazione 14346.

Il programma utente non vede mai i reali indirizzi fisici. 
Il programma crea un puntatore alla locazione 346, lo memorizza, lo modifica, lo confronta con altri indirizzi, tutto ciò sempre come il numero 346. 
Solo quando assume il ruolo di un indirizzo di memoria (magari in una load o una store indiretta), si riloca il numero sulla base del contenuto del registro di rilocazione. 
Il programma utente tratta indirizzi logici, l’architettura del sistema converte gli indirizzi logici in indirizzi fisici. 
Questa forma di collegamento nella fase d’esecuzione è stata trattata nel Paragrafo 9.1.2. La locazione finale di un riferimento a un indirizzo di memoria non è determinata finché non si compie effettivamente il riferimento.

In questo caso esistono due diversi tipi di indirizzi: gli indirizzi logici (nell’intervallo da 0 a _max_) e gli indirizzi fisici (nell’intervallo da _r_ + 0 a _r_ + _max_ per un valore di base _r_). 
Il programma utente genera solo indirizzi logici e pensa che il processo sia eseguito nelle posizioni da 0 a _max_. 
Tuttavia questi indirizzi logici devono essere mappati in indirizzi fisici prima d’essere usati. 
Il concetto di _spazio d’indirizzi logici_ mappato su uno _spazio d’indirizzi fisici_ separato è fondamentale per una corretta gestione della memoria. 