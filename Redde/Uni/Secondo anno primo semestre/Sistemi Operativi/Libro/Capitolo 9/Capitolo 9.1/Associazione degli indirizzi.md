In genere un programma risiede in un disco sotto forma di un file binario eseguibile. 
Per essere eseguito, il programma va caricato in memoria e inserito nel contesto di un processo, dove diventa idoneo per l’esecuzione su una cpu disponibile.

Il processo durante l’esecuzione può accedere alle istruzioni e ai dati in memoria. Quando il processo termina, si dichiara disponibile il suo spazio di memoria.

La maggior parte dei sistemi consente ai processi utenti di risiedere in qualsiasi parte della memoria fisica, quindi, anche se lo spazio d’indirizzi del calcolatore comincia all’indirizzo 00000, il primo indirizzo del processo utente non deve necessariamente essere 00000. 
Vedremo più avanti come un programma utente inserisce un processo nella memoria fisica.


Nella maggior parte dei casi un programma utente, prima di essere eseguito, deve passare attraverso vari passi, alcuni dei quali possono essere facoltativi. 
![[Pasted image 20221128162749.png]]
In questi passi gli indirizzi sono rappresentabili in modi diversi. 
Generalmente gli indirizzi del programma sorgente sono simbolici (per esempio, la variabile count). Un compilatore di solito associa (_bind_) questi indirizzi simbolici a indirizzi rilocabili (per esempio, “14 byte dall’inizio di questo modulo”). L’editor dei collegamenti (_linkage editor_), o il caricatore (_loader_), fa corrispondere a sua volta questi indirizzi rilocabili a indirizzi assoluti (per esempio, 74014). Ogni associazione rappresenta una corrispondenza da uno spazio d’indirizzi a un altro.

Generalmente, l’associazione di istruzioni e dati a indirizzi di memoria si può compiere in qualsiasi passo del seguente percorso.
- **Compilazione**. Se nella fase di compilazione si sa dove il processo risiederà in memoria, si può generare codice **assoluto**. Se, per esempio, è noto a priori che un processo utente inizia alla locazione _R_, anche il codice generato dal compilatore comincia da quella locazione. Se, in un momento successivo, la locazione iniziale cambiasse, sarebbe necessario ricompilare il codice.

- **Caricamento**. Se nella fase di compilazione non è possibile sapere in che punto della memoria risiederà il processo, il compilatore deve generare codice **rilocabile**. In questo caso si ritarda l’associazione finale degli indirizzi alla fase del caricamento. Se l’indirizzo iniziale cambia, è sufficiente ricaricare il codice utente per incorporare il valore modificato.

-  **Esecuzione**. Se durante l’esecuzione il processo può essere spostato da un segmento di memoria a un altro, si deve ritardare l’associazione degli indirizzi fino alla fase d’esecuzione. Per realizzare questo schema è necessario disporre di hardware specializzato; questo argomento è trattato nel Paragrafo 9.1.3. La maggior parte dei sistemi operativi general-purpose impiega questo metodo.

Una gran parte di questo capitolo è dedicata alla spiegazione di come i vari tipi di associazione degli indirizzi si possano realizzare efficacemente in un calcolatore e, inoltre, alla discussione dell’appropriato supporto hardware per queste funzioni.