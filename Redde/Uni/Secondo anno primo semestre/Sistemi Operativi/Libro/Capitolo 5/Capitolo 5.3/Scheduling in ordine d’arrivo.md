Il più semplice algoritmo di scheduling della cpu è **l’algoritmo di scheduling in ordine d’arrivo (_scheduling first-come, first-served_ o fcfs**). 

Con questo schema la cpu si assegna al processo che la richiede per primo. La realizzazione del criterio fcfs si basa su una coda fifo. Quando un processo entra nella ready queue, si collega il suo pcb all’ultimo elemento della coda. Quando la cpu è libera, viene assegnata al processo che si trova alla testa della coda, rimuovendolo da essa. Il codice per lo scheduling fcfs è semplice sia da scrivere sia da capire.

Un aspetto negativo è che il tempo medio d’attesa per l’algoritmo fcfs è spesso abbastanza lungo.
Si consideri il seguente insieme di processi, che si presenta al momento 0, con la durata della sequenza di operazioni della cpu espressa in millisecondi:
![[Pasted image 20221105162503.png]]
Se i processi arrivano nell’ordine P1, P2, P3 e sono serviti in ordine **fcfs**, si ottiene il risultato illustrato nel seguente diagramma di Gantt, un diagramma a barre che illustra una data pianificazione includendo i tempi d’inizio e fine di ogni processo partecipante.
![[Pasted image 20221105162548.png]]
Il tempo d’attesa è 0 millisecondi per il processo P1, 24 millisecondi per il processo P2 e 27 millisecondi per il processo P3. Quindi, il tempo d’attesa medio è **(0 + 24 + 27)/3 = 17 millisecondi.** 

Se i processi arrivassero nell’ordine P2, P3, P1, i risultati sarebbero quelli illustrati nel seguente diagramma di Gantt:
![[Pasted image 20221105162734.png]]
Il **tempo di attesa medio è ora di (6 + 0 + 3)/3 = 3 millisecondi**.

Si tratta di una notevole riduzione. Quindi, il tempo medio d’attesa in condizioni di fcfs non è in genere minimo, e può variare grandemente all’aumentare della variabilità dei cpu burst dei vari processi.

Si considerino inoltre le prestazioni dello scheduling fcfs in una situazione dinamica. Si supponga di avere un processo con prevalenza d’elaborazione e molti processi con prevalenza di i/o. Via via che i processi fluiscono nel sistema si può verificare la seguente situazione. Il processo con prevalenza d’elaborazione occupa la cpu. Durante questo periodo tutti gli altri processi terminano le proprie operazioni di i/o e si spostano nella ready queue, nell’attesa della cpu. Mentre i processi si trovano nella ready queue, i dispositivi di i/o sono inattivi. Successivamente il processo con prevalenza d’elaborazione termina la propria sequenza di operazioni della cpu e passa a una fase di i/o. Tutti i processi con prevalenza di i/o, caratterizzati da sequenze di operazioni della cpu molto brevi, sono eseguiti rapidamente e tornano alle code di i/o, lasciando inattiva la cpu. Il processo con prevalenza d’elaborazione torna nella ready queue e riceve il controllo della cpu; così, finché non termina l’esecuzione del processo con prevalenza d’elaborazione, tutti i processi con prevalenza di i/o si trovano nuovamente ad attendere nella ready queue. Si ha un effetto convoglio, tutti i processi attendono che un lungo processo liberi la cpu, il che causa una riduzione dell’utilizzo della cpu e dei dispositivi rispetto a quella che si avrebbe se si eseguissero per primi i processi più brevi.

**L’algoritmo di scheduling fcfs è senza prelazione;**
una volta che la cpu è assegnata a un processo, questo la trattiene fino al momento del rilascio, che può essere dovuto al termine dell’esecuzione o alla richiesta di un’operazione di i/o.

L’algoritmo fcfs risulta particolarmente problematico nei sistemi in time-sharing, dove è importante che ogni utente disponga della cpu a intervalli regolari. Permettere a un solo processo di occupare la cpu per un lungo periodo condurrebbe a risultati disastrosi.