Un processo durante l'esecuzione é soggetto a cambiamenti del suo stato, definito in parte dall'attivitá corrente del processo stesso. Un processo puó trovarsi in uno tra i seguenti stati.
- **Nuovo:** si crea il processo.
- **Esecuzione (running):** Le istruzioni vengono eseguite.
- **Attesa (waiting):** Il processo attende che si verifichi qualche evento  (come il completamento di un’operazione di i/o o la ricezione di un segnale).
- **Pronto (ready):** Il processo attende di essere asseganto a un unitá d'elaborazione.
- **Terminato:** Il processo ha terminato l'esecuzione

Questi termini sono piuttosto arbitrari e variano secondo il sistema operativo. Gli stati che rappresentano sono in ogni modo presenti in tutti i sistemi, anche se alcuni sistemi operativi introducono ulteriori distinzioni tra gli stati dei processi. È importante capire che in ciascuna unità d’elaborazione può essere in _esecuzione_ solo un processo per volta, sebbene molti processi possano essere _pronti_ o nello stato di _attesa_. Il diagramma di transizione fra questi stati è riportato nella seguente figura.
![[Pasted image 20221024170357.png]]
