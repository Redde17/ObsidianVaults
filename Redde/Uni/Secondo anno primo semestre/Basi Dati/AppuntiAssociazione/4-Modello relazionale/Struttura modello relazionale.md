La maggior parte dei sistemi di basi dati oggi sul mercato si fonda sul modello relazionale che si basa su due concetti: 
- Relazione: 
	proviene dalla matematica, in particolare dalla teoria degli insiemi. Il termine relazione viene utilizzato in 3 circostanze: 
	1. Matematica; 
	2. secondo la definizione del modello relazionale; 
	3. come traduzione di relationship e quindi con riferimento al modello concettuale. 
	
- Tabella: 
	concetto semplice e intuitivo.

### 4.1.1 Relazioni e tabelle
Una relazione matematica di due insiemi è definita come sottoinsieme del prodotto cartesiano di 𝐷1𝑥 𝐷2, (l’insieme delle coppie ordinate (𝑣1, 𝑣2), tali che 𝑣1 è un elemento di 𝐷1 e 𝑣2 è un elemento di 𝐷2) questo perché gli insiemi, e quindi le relazioni, possono essere raggruppati in forma tabellare. 
Ma non tutte le tabelle esprimono una relazione.

Poiché le basi di dati devono essere memorizzate in sistemi di calcolo di dimensioni finite, le relazioni sono finite su domini eventualmente infiniti.

Il numero n di insiemi coinvolti viene detto “grado della relazione”. Il numero di elementi della relazione viene detto “cardinalità della relazione “. Ogni coppia è detta n-upla; scambiando l'ordine delle righe la rappresentazione è la stessa.

Una relazione matematica è un insieme di n-uple ordinate, in particolare: 
- non c'è ordinamento fra le n-uple; 
- le n-uple sono tutte diverse tra loro; 
- ciascuna n-upla è ordinata: l’i-esimo valore proviene dall’i-esimo dominio

Ad ogni colonna viene dato un nome detto attributo che descrive il “ruolo” giocato dal dominio stesso; in questo caso anche l'ordine delle colonne non è più importante. 
Nella rappresentazione tabellare, utilizziamo gli attributi come intestazioni quindi tali attributi devono essere diversi l'uno dall'altro. In questo caso, in una “relazione con attributi”, ogni elemento della rappresentazione è detto tupla. 

Nella relazione matematica abbiamo n-uple i cui elementi sono individuati per posizione, mentre nelle tuple gli elementi sono individuati per mezzo degli attributi, cioè con una tecnica non posizionale.

Il modello relazionale è basato su valori, quindi rappresenta solo ciò che è rilevante: non vi è alcun legame tra livello logico e fisico (basato su puntatori e record) e ciò ha influenzato il successo del modello relazionale.

Una Tabella rappresenta una relazione se: 
- i valori di ogni colonna sono fra loro omogenei; 
- le righe sono diverse fra loro; 
- le intestazioni delle colonne sono diverse tra loro

Una tabella che rappresenta una relazione: 
- l'ordinamento tra le righe è irrilevante; 
- l'ordinamento tra le colonne è irrilevante.

