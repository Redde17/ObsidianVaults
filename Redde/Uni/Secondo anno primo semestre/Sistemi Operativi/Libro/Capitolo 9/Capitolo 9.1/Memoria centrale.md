In questo capitolo si presentano diversi metodi di gestione della memoria.
Gli algoritmi di gestione della memoria variano dall’approccio più semplice che accede all’hardware della macchina in maniera diretta ai metodi di paginazione e segmentazione. 

Ogni metodo presenta vantaggi e svantaggi. La scelta di un metodo specifico di gestione della memoria dipende da molti fattori, in particolar modo dall’architettura hardware del sistema, infatti molti algoritmi richiedono un supporto hardware. 
Per questa ragione in molti sistemi l’hardware e la gestione della memoria da parte del sistema operativo sono strettamente integrati.

# Introduzione
La memoria è fondamentale nelle operazioni di un moderno sistema di calcolo. 
La memoria consiste in un grande vettore di byte, ciascuno con il proprio indirizzo. La cpu preleva le istruzioni dalla memoria sulla base del contenuto del contatore di programma; tali istruzioni possono determinare ulteriori letture (_load_) e scritture (_store_) in specifici indirizzi di memoria.

Un tipico ciclo d’esecuzione di un’istruzione, per esempio, prevede che l’istruzione sia prelevata dalla memoria; quindi viene decodificata (e ciò può comportare il prelievo di operandi dalla memoria) e poi eseguita sugli eventuali operandi; i risultati si possono scrivere in memoria. 

La memoria vede soltanto un flusso d’indirizzi di memoria, e non sa come sono generati (contatore di programma, indicizzazione, riferimenti indiretti, indirizzamenti immediati e così via), oppure a che cosa servano (istruzioni o dati). 
Di conseguenza, è possibile ignorare _come_ un programma genera un indirizzo di memoria, e prestare attenzione solo alla sequenza degli indirizzi di memoria generati dal programma in esecuzione.

L’analisi che sviluppiamo nel seguito comprende una panoramica degli aspetti basilari della gestione della memoria: l’hardware, la mappatura degli indirizzi simbolici in indirizzi fisici effettivi, e la distinzione fra indirizzamento logico e fisico. 
Concluderemo il paragrafo discutendo il linking dinamico e la condivisione delle librerie.

### 9.1.1 [[Hardware di base]]
### 9.1.2 [[Associazione degli indirizzi]]
### 9.1.3 [[Spazi di indirizzi logici e fisici]]
### 9.1.4 [[Caricamento dinamico]]
### 9.1.5 [[Linking dinamico e librerie condivise]]