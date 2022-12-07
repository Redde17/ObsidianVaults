Un vantaggio della paginazione risiede nella possibilità di _condividere_ codice comune, il che è particolarmente importante in un ambiente con più processi.

Si consideri la libreria standard del C, che fornisce parte dell’interfaccia alla chiamata di sistema in molte versioni di unix e Linux. 
Su un tipico sistema Linux, la maggior parte dei processi utente richiede la libreria standard del C libc. 
Un’opzione percorribile è che ogni processo carichi la propria copia di libc nel proprio spazio di indirizzamento. Se un sistema ha 40 processi utente e la libreria libc è di 2 mb, ciò richiederebbe 80 mb di memoria.

Se il codice è rientrante può però essere condiviso, come illustrato nella seguente figura:
![[Pasted image 20221207173618.png]]
si osservano tre processi che condividono le pagine della libreria libc (anche se la figura mostra che la libreria libc occupa quattro pagine, nella realtà ne occuperebbe di più).

Il codice rientrante è un codice non auto-modificante: non cambia mai durante l’esecuzione. Due o più processi possono quindi eseguire lo stesso codice allo stesso tempo.

Ogni processo dispone di una propria copia dei registri e di una memoria dove conserva i dati necessari per la propria esecuzione. I dati per due diversi processi saranno, ovviamente, diversi. Solo una copia della libreria standard del C deve essere conservata nella memoria fisica e la tabella delle pagine di ogni processo utente viene mappata sulla stessa copia fisica di libc. Quindi, per supportare 40 processi, abbiamo bisogno di una sola copia della libreria, e lo spazio totale ora richiesto è di 2 mb anziché di 80 mb: un risparmio significativo!


Oltre alle librerie di run-time come libc, altri programmi d’uso frequente possono essere condivisi: compilatori, interfacce a finestre, sistemi di database e così via. Le librerie condivise discusse nel Paragrafo 9.1.5 sono in genere implementate con pagine condivise. Per poter essere condiviso, il codice deve essere rientrante. La natura di sola lettura del codice condiviso non deve essere lasciata alla correttezza intrinseca del codice, ma deve essere fatta rispettare dal sistema operativo.