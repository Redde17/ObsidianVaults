Nel Paragrafo 1.10.5 è stato trattato il cloud computing. Una delle offerte dei fornitori di servizi cloud è lo spazio di archiviazione su cloud (_cloud storage_). Come nel caso della memoria secondaria collegata alla rete, quella su cloud offre accesso allo spazio di archiviazione attraverso una rete ma, a differenza dei nas, l’accesso allo spazio di archiviazione avviene tramite Internet o tramite un’altra wan verso un data center remoto che fornisce spazio a pagamento (o talvolta gratuitamente).

Un’altra differenza tra nas e cloud storage è il modo in cui lo spazio di archiviazione è accessibile e presentato agli utenti. Utilizzando i protocolli cifs o nfs è possibile accedere a un nas come si accede a un qualsiasi altro file system, mentre se viene utilizzato il protocollo iscsi vi si accede come a una unità di memoria a blocchi. La maggior parte dei sistemi operativi integra questi protocolli e presenta lo storage nas allo stesso modo degli altri sistemi di memorizzazione. Il cloud storage è invece basato su api, e i programmi utilizzano le api per accedere allo spazio di memorizzazione. Amazon S3 è un’offerta leader di cloud storage, Dropbox, un esempio di azienda che fornisce app per connettersi allo storage, Microsoft OneDrive e Apple iCloud sono altri esempi di archiviazione su cloud.

Uno dei motivi per cui vengono utilizzate le api al posto dei protocolli esistenti è la latenza e gli scenari di errore di una wan. 
I protocolli nas sono stati progettati per essere utilizzati nelle reti lan, che hanno una latenza inferiore rispetto alle wan e sono meno soggette alla perdita di connettività tra l’utente e il dispositivo di memorizzazione.
Se una connessione lan viene interrotta, un sistema che utilizza nfs o cifs potrebbe bloccarsi fino alla ripresa del normale funzionamento. Quando si utilizzano servizi cloud errori del genere sono più probabili e un’applicazione interrompe semplicemente l’accesso fino al ripristino della connettività.