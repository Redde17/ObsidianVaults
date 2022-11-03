I thread possono essere **distinti in thread a livello utente e thread a livello kernel**: i primi sono gestiti sopra il livello del kernel e senza il suo supporto; i secondi, invece, sono gestiti direttamente dal sistema operativo. 
Praticamente tutti i sistemi operativi moderni supportano i thread nel kernel, compresi Windows, Linux e macos.

In ogni caso, deve esistere una relazione tra i thread a livello utente e i thread a livello kernel, come mostrato nella figura seguente. In questo paragrafo analizziamo tre opzioni comuni: 
### 4.3.1 [[Modello da molti a uno]]
### 4.3.2 [[Modello da uno a uno]]
### 4.3.3 [[Modello da molti a molti]]

![[Pasted image 20221102170026.png]]

