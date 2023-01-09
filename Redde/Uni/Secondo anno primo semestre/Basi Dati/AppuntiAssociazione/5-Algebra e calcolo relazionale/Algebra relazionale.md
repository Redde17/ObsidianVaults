L'algebra relazionale è un linguaggio procedurale, basato su concetti di tipo algebrico. 
E’ costituito da un insieme di operatori, definiti su relazioni che producono ancora relazioni come risultati e tali relazioni possono essere composti. 
L’algebra relazionale produce tabelle eliminando le tuple ripetute al contrario di SQL che le mantiene.
E’ possibile costruire espressioni che coinvolgono più operatori, in modo da formulare interrogazioni anche complesse. 
I vari operatori si distinguono in: 
- quell’insiemistici tradizionali: unione, intersezione, differenza; 
- quelli più specifici: ridenominazione, selezione, proiezione; 
- il più importante, quello di join, in varie forme, join naturale, prodotto cartesiano e theta join.

### 5.2.1 Operatori insiemistici
Le relazioni sono insiemi, per questo motivo possiamo definire su di essi gli operatori insiemistici di unione, differenza e intersezione. Una relazione è un insieme di tuple omogenee, definite sugli stessi attributi. Pertanto, gli operatori devono essere definiti su relazioni con attributi uguali.

1. l’unione di due relazioni 𝑟1 e 𝑟2 definite sullo stesso insieme di attributi X è ancora una relazione su X contenente le tuple che appartengono a 𝑟1 oppure a 𝑟2, oppure a entrambe; 
2. l’intersezione tra due relazioni su un insieme X è ancora una relazione su X contenente le tuple che appartengono sia a 𝑟1 sia a 𝑟2; 
3. la differenza tra due relazioni su un insieme X è ancora una relazione su X contenente le tuple che appartengono a 𝑟1 ma non a 𝑟2.

L'operazione di unione e intersezione è un'operazione commutativa mentre la differenza non lo è. L’unione e la differenza sono operatori fondamentali mentre l’intersezione è un operatore derivabile (dalla differenza).

### 5.2.2 Ridenominazione
La ridenominazione è un operatore unario ed ha come unico obbiettivo quello di modificare i nomi degli attributi in modo da facilitare le operazioni insiemistiche che possono essere effettuate solo su attributi uguali. La ridenominazione "modifica il nome degli attributi" lasciando inalterato il contenuto delle relazioni: cambia solo l’intestazione, mentre il corpo rimane invariato. Il simbolo che viene utilizzato è 𝝆.
![[Pasted image 20230109171417.png]]

### 5.2.3 Selezione
Gli operatori che permettono di manipolare le relazioni sono: la selezione, la proiezione e join (quest’ultimo con diverse varianti). La selezione e la proiezione sono operatori unari e producono come risultato una porzione dell’operando.
La selezione produce un sottoinsieme delle n-uple, su tutti gli attributi, mentre la proiezione dà un risultato in cui contribuiscono tutte le tuple, ma su un sottoinsieme degli attributi.
La selezione genera “decomposizioni orizzontali” e la proiezione “decomposizioni verticali”. Inoltre, la selezione può prevedere confronti fra attributi tramite connettivi logici: ∨, ∧ , ¬ . Il simbolo della selezione è : 𝝈𝑪𝒐𝒏𝒅𝒊𝒛𝒊𝒐𝒏𝒆 (𝑶𝒑𝒆𝒓𝒂𝒏𝒅𝒐).
![[Pasted image 20230109171553.png]]

### 5.2.4 Proiezione
La proiezione è anch’essa un operatore unario. Produce come risultato tante tuple quante l’operando, definite però solo su una parte degli attributi. Essendo le relazioni definite come insiemi, non possono comparire in esse più tuple uguali fra loro: i contributi uguali “collassano” in una sola tupla. In generale, possiamo dire che il risultato di una proiezione contiene al più tante tuple quante l’operando, ma può contenerne anche di meno. Esiste un legame fra i vincoli di chiave e le proiezioni:
- se X è una superchiave di R, allora 𝜋𝑋(𝑅) contiene esattamente tante n-uple quante R.
Il simbolo della proiezione è 𝝅𝑳𝒊𝒔𝒕𝒂𝑨𝒕𝒕𝒓𝒊𝒃𝒖𝒕𝒊(𝑶𝒑𝒆𝒓𝒂𝒏𝒅𝒐).
![[Pasted image 20230109171707.png]]

### 5.2.5 Prodotto cartesiano
Il prodotto cartesiano è un’operazione binaria: contiene sempre un numero di n-uple pari al prodotto delle cardinalità degli operandi (le n-uple sono tutte combinabili).
![[Pasted image 20230109171829.png]]

### 5.2.6 Join
Il join è l’operatore più interessante dell’algebra relazionale, in quanto permette di operare su dati contenuti in relazioni diverse. Esistono due versioni dell’operatore: la prima (join naturale) utile per riflessioni di tipo astratto e la seconda (theta-join) usata dal punto di vista pratico.

#### Join naturale
Il join naturale è un operatore binario che correla dati in relazioni diverse. Il risultato del join è costituito da una relazione sull’unione degli attributi degli operandi e le sue tuple sono ottenute combinando le tuple degli operandi con valori uguali sugli attributi comuni. Il grado della relazione ottenuta dal join è ≤ della somma dei gradi dei due operandi, perché gli attributi omonimi degli operandi compaiono una sola volta nel risultato. Inoltre, il join naturale è commutativo e associativo. Il simbolo del join è ⊳⊲.
Quando ogni tupla di ciascuno degli operandi contribuisce ad almeno una tupla del risultato, il join si dice completo (in questo caso l’esempio 1 è un join completo).
![[Pasted image 20230109172010.png]]

E’ possibile che nessuna tupla degli operandi sia combinabile, e allora si avrà un join vuoto.
![[Pasted image 20230109172032.png]]

Quando alcune tuple degli operandi non contribuiscono al risultato, allora tali tuple verranno chiamate dangling e si avrà un join incompleto (in questo caso l’esempio 3 è un join incompleto).
![[Pasted image 20230109172051.png]]

##### Cardinalità del join
Il join di R1 e R2 contiene un numero di n-uple compreso fra 0 e il prodotto di |R1| e |R2|
- Se il join coinvolge una chiave di R2, allora il numero di n-uple è compreso fra 0 e |R1|; 
- Se il join coinvolge una chiave di R2 e un vincolo di integrità referenziale, allora il numero di n-uple è pari a |R1|.

#### Join esterno e interno
Il join esterno (outer join) estende, con valori nulli, le n-uple che verrebbero tagliate fuori da un join interno (inner join). 
Esistono tre varianti dello join esterno:
- Sinistro: estende, con valori nulli se necessario, solo le tuple del primo operando; 
- Destro: che estende solo le tuple del secondo operando; 
- Completo: estende tutte le tuple di entrambi gli operandi;
![[Pasted image 20230109172307.png]]
Se due insiemi 𝑋1 = 𝑋2, l’operazione di join coincide con l’intersezione. Se 𝑋1𝑒 𝑋2 sono disgiunti l’operazione di join coincide con il prodotto cartesiano.

#### Theta-join
Il theta-join è un operatore derivato (cioè esprimibile per mezzo di altri operatori), come prodotto cartesiano seguito da una selezione: la condizione F è spesso una congiunzione (AND) di atomi di confronto A1 ϑ A2 dove ϑ è uno degli operatori di confronto (=, >, <, …).
𝑹𝟏 ⊳⊲𝑭 𝑹𝟐 = 𝝈𝑭( 𝑹𝟏 ⊳⊲ 𝑹𝟐)
Se l'operatore è sempre l'uguaglianza (=) allora si parla di equi-join.

![[Pasted image 20230109172428.png]]