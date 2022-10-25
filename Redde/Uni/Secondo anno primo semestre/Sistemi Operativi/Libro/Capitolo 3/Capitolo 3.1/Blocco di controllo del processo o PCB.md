Ogni processo è rappresentato nel sistema operativo da un blocco di controllo (_process control block_, pcb, o _task control block_, tcb). Un pcb (figura sottostante) contiene molte informazioni connesse a un processo specifico, tra cui le seguenti.
![[Pasted image 20221024170514.png]]
- **Stato del processo**, che puó essere: nuovo, pronto, esecuzione, attesa, arresto, e altro.
- **Contatore di programma**: Contenitore per l'indirizzo della successiva istruzione da eseguire per tale processo.
- **Registri della CPU**: I registri variano in numero e tipo secondo l’architettura del calcolatore. Essi comprendono accumulatori, registri indice, puntatori alla cima dello stack (_stack pointer_), registri d’uso generale e registri contenenti i codici di condizione (_condition codes_). Quando si verifica un’interruzione della cpu si devono salvare tutte queste informazioni insieme con il contatore di programma, in modo da permettere la corretta esecuzione del processo in un momento successivo, quando viene rischedulato.

- **Informazioni sullo scheduling di cpu**: Queste informazioni comprendono la priorità del processo, i puntatori alle code di scheduling e tutti gli altri parametri di scheduling
- **Informazioni sulla gestione della memoria**: Queste informazioni possono includere elementi quali il valore dei registri di base e di limite, le tabelle delle pagine o le tabelle dei segmenti, a seconda del sistema di gestione della memoria usato dal sistema operativo
- **Informazioni di accounting:** Queste informazioni comprendono la quota di uso della cpu e il tempo d’utilizzo della stessa, i limiti di tempo, i numeri dei processi, e così via.
- **Informazioni sullo stato dell’i/o**: Queste informazioni comprendono la lista dei dispositivi di i/o assegnati a un determinato processo, l’elenco dei file aperti, e così via.

In sintesi, il pcb si usa semplicemente come deposito per tutte le informazioni relative ai vari processi.