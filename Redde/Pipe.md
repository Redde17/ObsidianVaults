Una pipe agisce come canale di comunicazione tra processi. Le pipe sono state uno dei primi meccanismi di comunicazione tra processi (ipc) nei primi sistemi unix e generalmente forniscono ai processi uno dei metodi più semplici per comunicare l’uno con l’altro, sebbene con qualche limitazione. Quando si implementa una pipe devono essere prese in considerazione quattro questioni.

1.  La comunicazione permessa dalla pipe è unidirezionale o bidirezionale?
2.  Se è ammessa la comunicazione bidirezionale, essa è di tipo _half duplex_ (i dati possono viaggiare in un’unica direzione alla volta) o _full duplex_ (i dati possono viaggiare contemporaneamente in entrambe le direzioni)?
3.  Deve esistere una relazione (del tipo _padre-figlio_) tra i processi in comunicazione?
4.  Le pipe possono comunicare in rete o i processi comunicanti devono risiedere sulla stessa macchina?

### Pipe convenzionali
Le pipe convenzionali permettono a due processi di comunicare secondo una modalità standard chiamata del produttore-consumatore. Il produttore scrive a una estremità del canale (l’estremità dedicata alla scrittura, o _write-end_) mentre il consumatore legge dall’altra estremità (l’estremità dedicata alla lettura, o _read-end_). Le pipe convenzionali sono quindi unidirezionali, perché permettono la comunicazione in un’unica direzione. Se viene richiesta la comunicazione bidirezionale devono essere utilizzate due _pipe_, ognuna delle quali manda i dati in una direzione. Illustreremo la costruzione di pipe convenzionali sia in unix sia in Windows. In entrambi i programmi di esempio un processo scrive sulla pipe il messaggio Greetings, mentre l’altro lo legge dall’altra estremità della pipe.

Nei sistemi unix le pipe convenzionali sono costruite utilizzando la funzione
```
pipe(int fd[])
```
Essa crea una pipe alla quale si può accedere tramite i descrittori del file int fd[]:fd[0] è l’estremità dedicata alla lettura, mentre fd[1] è l’estremità dedicata alla scrittura. Il sistema unix considera una pipe come un tipo speciale di file; si può così accedere alle pipe tramite le usuali chiamate di sistema read() e write().

Non si può accedere a una pipe al di fuori del processo che la crea. Solitamente un processo padre crea una pipe e la utilizza per comunicare con un processo figlio generato con il comando fork().

Dal momento che la pipe è un tipo speciale di file, il figlio eredita la pipe dal proprio processo padre.

![[Pasted image 20221031171251.png]]
Come mostrato, ogni scrittura del padre sull’estremità dedicata alla scrittura della pipe, fd[1], può essere letta dal figlio sull’estremità dedicata alla lettura, fd[0].

Nel programma unix mostrato di seguito il processo padre crea una pipe e in seguito esegue una chiamata fork(), generando un processo figlio. Ciò che succede dopo la chiamata fork() dipende da come i dati devono fluire nel canale. In questo caso, il padre scrive sulla pipe e il figlio legge da essa. È importante sottolineare come sia il processo padre sia il processo figlio chiudano inizialmente le estremità inutilizzate del canale. Sebbene il programma mostrato nella Figura 3.21 non richieda questa azione è importante assicurare che un processo che legge dalla pipe possa rilevare l’end-of-file (read() restituisce 0) quando chi scrive ha chiuso la sua estremità della pipe.


```
#include <sys/types.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>

#define_BUFFER_SIZE 25
#define_READ_END 0
#define_WRITE_END 1

int main(void){
	char write_msg[BUFFER_SIZE] = “Greetings”;
	char read_msg[BUFFER_SIZE];
	int fd[2];
	pid_t pid;
	
	/* crea la pipe */
	if (pipe(fd) == -1) {
		fprintf(stderr,”Pipe failed”);
		return 1;
	}

	/* crea tramite fork un processo figlio */
	pid = fork();
	if (pid < 0) { /* errore */
		fprintf(stderr, “Fork Failed”);
		return 1;
	}

	if (pid > 0) { /* processo padre */
		/* chiude l’estremità inutilizzata della pipe */
		close(fd[READ_END]);
		
		/* scrive sulla pipe */
		write(fd[WRITE_END], write_msg, strlen(write_msg)+1);
		
		/* chiude l’estremità della pipe dedicata alla scrittura */
		close(fd[WRITE_END]);
	}
	
	else { /* processo figlio */
		/* chiude l’estremità inutilizzata della pipe */
		close(fd[WRITE_END]);
		
		/* legge dalla pipe */
		read(fd[READ_END], read_msg, BUFFER_SIZE);
		printf(“read %s”,read_msg);
		
		/* chiude l’estremità della pipe dedicata alla lettura */
		close(fd[READ_END]);
	}
	
	return 0;
}
```

Nei sistemi Windows le pipe convenzionali sono denominate pipe anonime e si comportano analogamente alle loro equivalenti in unix: sono unidirezionali e utilizzano relazioni del tipo padre-figlio tra i processi coinvolti nella comunicazione.

### Copia del testo dal libro sulle pipe in windows
Inoltre, l’attività di lettura e scrittura sulla pipe può essere eseguita con le usuali funzioni ReadFile() e WriteFile(). L’api Windows per creare le pipe è la funzione CreatePipe(), che riceve in ingresso quattro parametri. I parametri forniscono handle distinti per (1) leggere e (2) scrivere sulla pipe, oltre a (3) una istanza della struttura STARTUPINFO, usata per specificare che il processo figlio erediti gli handle della pipe. Inoltre, può essere specificata (4) la dimensione della pipe (in byte).

La Figura 3.23 (che prosegue nella Figura 3.24) illustra un processo padre che crea una pipe anonima per comunicare con il proprio figlio. A differenza dei sistemi unix, dove un processo figlio eredita automaticamente una pipe creata dal proprio padre, Windows richiede al programmatore di specificare quali attributi saranno ereditati dal processo figlio. Ciò avviene innanzitutto inizializzando la struttura ­SECURITY_ATTRIBUTES per permettere che gli handle siano ereditati e poi reindirizzando lo standard input o lo standard output del processo figlio verso l’handle di scrittura o di lettura della pipe, rispettivamente. Dato che il figlio leggerà dalla pipe, il padre deve reindirizzare lo standard input del figlio verso l’handle di lettura della pipe stessa. Inoltre, dal momento che le pipe sono half duplex, è necessario proibire al figlio di ereditare l’handle di scrittura della pipe. La creazione del processo figlio avviene come nel programma nella Figura 3.10, fatta eccezione per il quinto parametro che in questo caso viene impostato al valore true per indicare che il processo figlio eredita degli handle specifici dal proprio padre. Prima di scrivere sulla pipe, il padre ne chiude l’estremità di lettura, che è inutilizzata. Il processo figlio che legge dalla pipe è mostrato nella Figura 3.25. Prima di leggere dalla pipe, questo programma ottiene l’handle di lettura invocando GetStdHandle().

**Processo padre**
```
#include <stdio.h>

#include <stdlib.h>

#include <windows.h>

#define BUFFER_SIZE 25

int main(VOID){
	HANDLE ReadHandle, WriteHandle;
	STARTUPINFO si;
	PROCESS_INFORMATION pi;
	char message[BUFFER_SIZE] = “Greetings”;
	DWORD written;
	
	/* imposta gli attributi di sicurezza in modo che le pipe siano ereditate */
	SECURITY_ATTRIBUTES sa = {sizeof(SECURITY_ATTRIBUTES),NULL,TRUE};
	
	/* alloca la memoria */
	ZeroMemory(&pi, sizeof(pi));
	
	/* crea la pipe */
	if (!CreatePipe(&ReadHandle, &WriteHandle, &sa, 0)) {
		fprintf(stderr, “Create Pipe Failed”);
		return 1;
	}
	
	/* prepara la struttura START_INFO per il processo figlio */
	GetStartupInfo(&si);
	si.hStdOutput = GetStdHandle(STD_OUTPUT_HANDLE);
	
	/* reindirizza lo standard input verso l’estremità della pipe dedicata alla lettura */
	si.hStdInput = ReadHandle;
	si.dwFlags = STARTF_USESTDHANDLES;
	
	/* non permette al processo figlio di ereditare l’estremità della pipe dedicata alla scrittura */
	SetHandleInformation(WriteHandle, HANDLE_FLAG_INHERIT, 0);
	
	/* crea il processo figlio */
	CreateProcess(NULL, “child.exe”, NULL, NULL,
	TRUE, /* inherit handles */
	0, NULL, NULL, &si, &pi);
	
	/* chiude l’estremità inutilizzata della pipe */
	CloseHandle(ReadHandle);
	
	/* il padre scrive sulla pipe */
	if (!WriteFile(WriteHandle, message,BUFFER_SIZE,&written,NULL))
		fprintf(stderr, “Error writing to pipe.”);
		
	/* chiude l’estremità della pipe dedicata alla scrittura */
	CloseHandle(WriteHandle);
	
	/* attende la terminazione del processo figlio */
	WaitForSingleObject(pi.hProcess, INFINITE);
	CloseHandle(pi.hProcess);
	CloseHandle(pi.hThread);
	
	return 0;

}
```

**Processo figlio**
```
#include <stdio.h>
#include <windows.h>
#define BUFFER_SIZE 25

int main(VOID){
	HANDLE Readhandle;
	CHAR buffer[BUFFER_SIZE];
	DWORD read;
	
	/* riceve l’handle di lettura della pipe */
	ReadHandle = GetStdHandle(STD_INPUT_HANDLE);
	
	/* il figlio legge dalla pipe */
	if (ReadFile(ReadHandle, buffer, BUFFER_SIZE, &read, NULL))
		printf(“child read %s”,buffer);
	else
		fprintf(stderr, “Error reading from pipe”);
	
	return 0;
}
```


Si noti bene che le pipe convenzionali richiedono una relazione di parentela padre-figlio tra i processi comunicanti, sia in unix sia in Windows. Ciò significa che queste pipe possono essere utilizzate soltanto per la comunicazione tra processi in esecuzione sulla stessa macchina.