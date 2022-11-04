Un altro elemento coinvolto nella funzione di scheduling della cpu è il dispatcher; si tratta del modulo che passa effettivamente il controllo della cpu al processo scelto dallo scheduler a breve termine. Questa funzione comprende:
-   il cambio di contesto da un processo a un altro;
-   il passaggio alla modalità utente;
-   il salto alla giusta posizione del programma utente per riavviarne l’esecuzione.

Poiché si attiva a ogni cambio di contesto, il dispatcher dovrebbe essere quanto più rapido è possibile. Il tempo richiesto dal dispatcher per fermare un processo e avviare l’esecuzione di un altro è noto come latenza di dispatch ed è mostrato nella seguente figura.
![[Pasted image 20221104193300.png]]

