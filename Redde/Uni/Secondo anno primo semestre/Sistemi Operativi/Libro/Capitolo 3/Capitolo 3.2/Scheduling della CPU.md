Nel corso della sua esistenza, un processo si sposta ripetutamente tra la coda dei processi pronti e diverse code di attesa. Il ruolo dello scheduler della cpu è selezionare un processo nella coda dei processi pronti e allocarlo a un core della cpu. Questa selezione deve essere effettuata frequentemente. Un processo i/o bound può restare in esecuzione solo per pochi millisecondi prima di attendere una richiesta di i/o. Un processo cpu bound, d’altro canto, richiede un core della cpu per tempi più lunghi, ma è improbabile che lo scheduler della cpu garantisca il core a un processo per un periodo prolungato. È invece probabile che lo scheduler sia progettato per togliere forzatamente la cpu a un processo in esecuzione e schedulare un altro processo da eseguire. Lo scheduling della cpu viene dunque eseguito almeno una volta ogni 100 millisecondi, anche se generalmente ciò avviene molto più frequentemente.

Alcuni sistemi operativi hanno una forma intermedia di scheduling, nota come swapping, la cui idea chiave è che a volte possa essere vantaggioso eliminare processi dalla memoria (e dalla contesa per la cpu), riducendo il grado di multiprogrammazione del sistema. In seguito, il processo può essere reintrodotto in memoria, in modo che la sua esecuzione riprenda da dove era stata interrotta.

Questo schema si chiama avvicendamento dei processi in memoria (_swapping_), perché un processo può essere rimosso dalla memoria e collocato su disco (_swapped out_), dove viene salvato il suo stato corrente, e successivamente ricaricato in memoria da disco (_swapped in_), con il ripristino del suo stato. L’avvicendamento dei processi in memoria è in genere necessario solo quando la memoria è sovrautilizzata e deve essere liberata.

Lo swapping è illustrato nel Capitolo 9.