Durante la propria esecuzione, un processo può creare numerosi nuovi processi. Come menzionato in precedenza, il processo creante si chiama processo genitore (o padre), mentre il nuovo processo si chiama processo figlio. Ciascuno di questi nuovi processi può creare a sua volta altri processi, formando un albero di processi.

La maggior parte dei sistemi operativi (compresi unix, Linux e Windows) identifica un processo per mezzo di un numero univoco, solitamente un intero, detto identificatore del processo o pid (_process identifier_). Il pid fornisce un valore univoco per ogni processo del sistema e può essere usato come indice per accedere a vari attributi di un processo all’interno del kernel.

*Tipico albero dei processi del sistema operativo Linux.*
![[Pasted image 20221027170625.png]]


Nei sistemi unix e Linux si può ottenere l’elenco dei processi tramite il comando ps. Per esempio, digitando
```
ps –el
```
si otterranno informazioni complete su tutti i processi attualmente attivi nel sistema; 

In generale, quando un processo crea un processo figlio, quest’ultimo avrà bisogno di determinate risorse (tempo d’elaborazione, memoria, file, dispositivi di i/o) per eseguire il proprio compito. Un processo figlio può essere in grado di ottenere le proprie risorse direttamente dal sistema operativo, oppure può essere vincolato a un sottoinsieme delle risorse del processo genitore. Il processo genitore può avere la necessità di spartire le proprie risorse tra i suoi processi figli, oppure può essere in grado di condividerne alcune, come la memoria o i file, tra più processi figli. Limitando le risorse di un processo figlio a un sottoinsieme di risorse del processo genitore si può evitare che un processo sovraccarichi il sistema creando troppi processi figlio.

Oltre alle varie risorse fisiche e logiche, il processo genitore può passare al processo figlio i dati di inizializzazione.
Per esempio si consideri un processo che serva a mostrare i contenuti di un file, il processo filgio puó rivecere dal genitore il nome del file di ingresso e potrà anche ricevere il nome del dispositivo al quale inviare i dati in uscita. 
In alternativa, alcuni sistemi operativi passano risorse ai processi figli, nel qual caso il nostro processo potrebbe ottenere come risorse direttamente i due file aperti.

Quando un processo ne crea uno nuovo, per quel che riguarda l’esecuzione ci sono due possibilità:
1.  il processo genitore **continua** l’esecuzione in modo concorrente con i propri processi figli;
2.  il processo genitore **attende** che alcuni o tutti i suoi processi figli terminino.
    
Ci sono due possibilità anche per quel che riguarda lo spazio d’indirizzi del nuovo processo:
1.  il processo figlio è un duplicato del processo genitore (ha gli stessi programma e dati del genitore);
2.  nel processo figlio si carica un nuovo programma.

Funzionamento del comando fork() nei sistemi unix
![[Pasted image 20221027171701.png]]
La chiamata fork() genera un processo figlio copiando il processo padre restituendo 
a chiamata di sistema fork() il valore zero nel nuovo processo (il figlio), ma riporta l’identificatore del processo figlio (il pid diverso da zero) nel processo genitore, una volta fatto ció il processo figlio esegue il comando exec() iniziando a svolgere i suoi comandi.
