## Capitolo 1
**1.1 Quali sono i tre scopi principali di un sistema operativo?**
I tre scopi principali di un sistema operativo sono:
- Esecuzione di programmi presenti in memoria di massa.
- Gestione delle risorse disponibili.
- Supervisionare l'esecuzione di programmi e garantire l'utilizzo corretto della macchina.

**1.2 Abbiamo sottolineato la necessità di un sistema operativo per utilizzare efficientemente l'hardware di calcolo. Quando è opportuno che il sistema operativo rinunci a questo principio e “sprechi” risorse? Perché un tale sistema non è davvero uno spreco?**
I sistemi a utente singolo con interfaccia grafica al posto di massimizzare l'utilizzo di risorse massimizzano l'utilizzo del sisatema da parte dell'utente, quindi una GUI potrebbe sprecare cicli di CPU ma ottimizza l'interazione con l'utente.

**1.3 Qual è la principale difficoltà che un programmatore deve superare nella scrittura di un sistema operativo per un ambiente real-time?**
La principale difficoltà è mantenere il sistema operativo entro i vincoli temporali fissi di un sistema in tempo reale. Se il sistema non completa un'attività in un determinato intervallo di tempo, potrebbe causare un guasto dell'intero sistema.

**1.5 Come funziona la distinzione tra modalità kernel e modalità utente**
Nella modalitá utente la CPU é nettamente limitata nelle azioni che puó eseguire cosí da impedire l'accesso diretto alle risorse base da parte dell'utente, risorse accessibili solo in modalitá kernel. Ció permette di aumentare la sicurezza del sistema escludendo risorse critiche in modalitá utente.

**1.6 Quale delle seguenti istruzioni dovrebbe essere privilegiata?**

	a. Impostare il timer.
	b. Leggere il clock.
	c. Cancellare la memoria.
	d. Invocare un’istruzione trap.
	e. Disattivare le interruzioni.
	f. Modificare le informazioni nella tabella che indica lo status dei dispositivi.
	g. Passare da modalità utente a modalità di sistema.
	h. Accedere a un dispositivo i/o.

(risposta presa da appunti)
È necessario privilegiare le seguenti operazioni: impostare il valore del timer, cancellare la memoria, disattivare gli interrupt, modificare le voci nella tabella dello stato del dispositivo, accedere al dispositivo I/O . Il resto può essere eseguito in modalità utente.

Capitolo 2
