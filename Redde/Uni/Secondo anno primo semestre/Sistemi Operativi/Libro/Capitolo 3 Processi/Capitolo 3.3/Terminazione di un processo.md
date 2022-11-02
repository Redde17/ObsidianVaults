Un processo termina quando finisce l’esecuzione della sua ultima istruzione e inoltra la richiesta al sistema operativo di essere cancellato usando la chiamata di sistema exit(); a questo punto, il processo figlio può riportare un’informazione di stato al processo genitore, che la riceve attraverso la chiamata di sistema wait(). Tutte le risorse del processo, incluse la memoria fisica e virtuale, i file aperti e le aree della memoria per l’i/o, sono liberate dal sistema operativo.

La terminazione di un processo si può verificare anche in altri casi. Un processo può causare la terminazione di un altro per mezzo di un’opportuna chiamata di sistema. Generalmente solo il genitore del processo che si vuole terminare può invocare una chiamata di sistema di questo tipo.

Un processo genitore può porre termine all’esecuzione di uno dei suoi processi figli per diversi motivi, tra i quali i seguenti.
-   Il processo figlio ha ecceduto nell’uso di alcune tra le risorse che gli sono state assegnate. Ciò richiede che il processo genitore disponga di un sistema che esamini lo stato dei propri processi figli.
-   Il compito assegnato al processo figlio non è più richiesto.
-   Il processo genitore termina e il sistema operativo non consente a un processo figlio di continuare l’esecuzione in tale circostanza.

In alcuni sistemi, se un processo termina si devono terminare anche i suoi figli, indipendentemente dal fatto che la terminazione del genitore sia stata normale o anormale. Si parla di terminazione a cascata, una procedura avviata di solito dal sistema operativo.

Un processo genitore può attendere la terminazione di un processo figlio utilizzando la chiamata di sistema wait(), a cui viene passato un parametro che permette al genitore di ottenere lo stato di uscita del figlio. Questa chiamata di sistema restituisce anche l’id di processo del figlio terminato in modo che il genitore possa sapere di quale dei suoi figli si tratta:

```
pid_t pid;

int status;

pid = wait(&status);
```

Quando un processo termina, le sue risorse vengono deallocate dal sistema operativo. Tuttavia, la sua voce nella tabella dei processi deve rimanere fino a quando il padre chiama wait(), perché la tabella dei processi contiene lo stato di uscita del processo.

Un processo che è terminato, ma il cui genitore non ha ancora chiamato la wait(), è detto processo zombie. Tutti i processi passano in questo stato quando terminano, ma in genere rimangono zombie solo per breve tempo. Una volta che il genitore chiama la wait() il pid del processo zombie e la sua voce nella tabella dei processi vengono rilasciati.

Consideriamo ora che cosa accadrebbe se un genitore terminasse senza invocare la wait(), lasciando così orfani i suoi figli. Linux e unix affrontano questa situazione assegnando al processo systemd il ruolo di nuovo genitore dei processi orfani. (Ricordiamo dal Paragrafo 3.3.1 che il processo init è la radice della gerarchia dei processi nei sistemi unix). Il processo init invoca periodicamente wait(), consentendo in tal modo di raccogliere lo stato di uscita di qualsiasi processo orfano e rilasciando il suo pid e la relativa voce nella tabella dei processi.

Nonostante la maggior parte dei sistemi Linux abbia sostituito init con systemd, quest’ultimo può assumere lo stesso ruolo, con la differenza che Linux permette anche ad altri processi di ereditare i processi orfani e gestirne la terminazione.