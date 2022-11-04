Il successo dello scheduling della cpu dipende dall’osservazione della seguente proprietà dei processi: l’esecuzione del processo consiste in un ciclo d’elaborazione (svolta dalla cpu) e d’attesa del completamento delle operazioni di i/o. I processi si alternano tra questi due stati. L’esecuzione di un processo comincia con una sequenza di operazioni d’elaborazione svolte dalla cpu (_cpu_ _burst_), seguita da una sequenza di operazioni di i/o (_i/o_ _burst_), quindi un’altra sequenza di operazioni della cpu, di nuovo una sequenza di operazioni di i/o, e così via. L’ultima sequenza di operazioni della cpu si conclude con una richiesta al sistema di terminare l’esecuzione.

![[Pasted image 20221104191707.png]]

Le durate delle sequenze di operazioni della cpu (dette anche “burst della cpu”) sono state misurate in molte sperimentazioni, e sebbene varino molto secondo il processo e secondo il calcolatore, la loro curva di frequenza è simile a quella illustrata nella seguente figura. 

![[Pasted image 20221104191854.png]]

La curva è generalmente di tipo esponenziale o iperesponenziale, con molte brevi sequenze di operazioni della cpu, e poche sequenze di operazioni della cpu molto lunghe. Un programma con prevalenza di i/o (_i/o_ _bound_) produce generalmente molte sequenze di operazioni della cpu di breve durata. Un programma con prevalenza d’elaborazione (_cpu_ _bound_), invece, può produrre varie sequenze di operazioni della cpu molto lunghe. Questa distribuzione può essere utile nella scelta di un appropriato algoritmo di scheduling della cpu.
