Un altro importante fattore che riguarda il modo in cui si assegnano i frame ai vari processi è la sostituzione delle pagine. 
Nei casi in cui vi siano più processi in competizione per i frame, gli algoritmi di sostituzione delle pagine si possono classificare in due categorie generali: 
sostituzione globale e sostituzione locale. 
La sostituzione globale permette che per un processo si scelga un frame per la sostituzione dall’insieme di tutti i frame, anche se quel frame è al momento allocato a un altro processo; un processo può dunque sottrarre un frame a un altro processo. 
La sostituzione locale richiede invece che per ogni processo si scelga un frame solo dal proprio insieme di frame.

Si consideri per esempio uno schema di allocazione che, per una sostituzione a favore dei processi ad alta priorità, permetta di sottrarre frame ai processi a bassa priorità. 
Un processo può scegliere per la sostituzione uno dei suoi frame o uno di quelli di qualsiasi processo con priorità minore. Questo metodo permette a un processo ad alta priorità di aumentare il proprio livello di allocazione dei frame a discapito dei processi a bassa priorità.

Con la strategia di sostituzione locale, il numero di blocchi di memoria assegnati a un processo non cambia. Con la sostituzione globale, invece, può accadere che per un certo processo si selezionino solo frame allocati ad altri processi, aumentando così il numero di frame assegnati a quel processo, purché altri non scelgano per la sostituzione i _suoi_ frame.

L’algoritmo di sostituzione globale risente di un problema: 
un processo non può controllare il proprio tasso di page fault, infatti l’insieme di pagine che si trova in memoria per un processo non dipende solo dal comportamento di paginazione di quel processo, ma anche dal comportamento di paginazione di altri processi. 
Quindi, lo stesso processo può comportarsi in modi molto diversi, per esempio impiegando 0,5 secondi per un’esecuzione e 4,3 secondi per quella successiva, a causa di circostanze del tutto esterne. 
Con l’algoritmo di sostituzione locale questo problema non si presenta. Infatti l’insieme di pagine in memoria per un processo subisce l’effetto del comportamento di paginazione di quel solo processo. Tuttavia la sostituzione locale può penalizzare un processo, non rendendogli disponibili altre pagine di memoria meno usate. 
Generalmente, la sostituzione globale genera una maggiore produttività del sistema, e perciò è il metodo più usato.

Ci soffermeremo ora su una possibile strategia per implementare una politica globale di sostituzione delle pagine. 
In questo approccio soddisfiamo tutte le richieste di memoria mediante la lista dei frame liberi, ma piuttosto che aspettare che la lista si svuoti prima di iniziare a selezionare le pagine per la sostituzione, attiviamo la sostituzione delle pagine quando la dimensione della lista scende al di sotto di una certa soglia. Questa strategia cerca di garantire che ci sia sempre sufficiente memoria libera per soddisfare nuove richieste.

La strategia è illustrata nella seguente figura. 
![[Pasted image 20221214172547.png]]
Come accennato, lo scopo è di mantenere la quantità di memoria libera al di sopra di una soglia minima: quando si scende al di sotto di questa soglia, viene avviata una routine del kernel che inizia a recuperare pagine da tutti i processi nel sistema (in genere escludendo il kernel). 
Queste routine del kernel sono note come reaper (“mietitrici”) e possono applicare qualsiasi algoritmo di sostituzione delle pagine tra quelli trattati nel Paragrafo 10.4. 
Quando la quantità di memoria libera raggiunge la soglia massima, la routine reaper viene sospesa, per poi essere riavviata quando la memoria libera scende nuovamente al di sotto della soglia minima.