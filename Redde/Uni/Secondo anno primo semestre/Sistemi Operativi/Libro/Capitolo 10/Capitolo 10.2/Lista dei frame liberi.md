Quando si verifica un page fault, il sistema operativo deve spostare la pagina desiderata dalla memoria secondaria alla memoria principale.
Per risolvere i page fault la maggior parte dei sistemi operativi mantiene una lista dei frame liberi, ovvero un insieme di frame disponibili e utilizzabili per soddisfare le richieste, come mostrato nella seguente figura.
![[Pasted image 20221212190233.png]]
I sistemi operativi allocano generalmente i frame liberi usando una tecnica nota come **zero-fill-on-demand (“riempimento con zeri su richiesta”):** 
i frame vengono “azzerati” su richiesta prima di essere allocati, cancellando così il loro precedente contenuto

All’avvio di un sistema tutta la memoria disponibile viene inserita nella lista dei frame liberi. 
Man mano che vengono richiesti frame liberi (per esempio, tramite paginazione su richiesta), la dimensione della lista dei frame liberi si riduce. A un certo punto la lista diventa vuota, oppure la sua dimensione scende al di sotto di una certa soglia fissata: quando ciò si verifica la lista deve essere ripopolata.