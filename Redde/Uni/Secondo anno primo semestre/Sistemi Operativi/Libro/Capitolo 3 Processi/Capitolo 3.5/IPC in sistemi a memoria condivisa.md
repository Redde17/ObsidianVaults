La comunicazione tra processi basata sulla condivisione della memoria richiede che i processi comunicanti allochino una zona di memoria condivisa, di solito residente nello spazio degli indirizzi del processo che la alloca: gli altri processi che desiderano usarla per comunicare dovranno annetterla al loro spazio degli indirizzi. Si ricordi che, normalmente, il sistema operativo tenta di impedire a un processo l’accesso alla memoria di altri processi. La condivisione della memoria richiede che due o più processi raggiungano un accordo per superare questo limite, in modo da poter comunicare tramite scritture e letture dell’area condivisa. Il tipo e la collocazione dei dati sono determinati dai processi, e rimangono al di fuori del controllo del sistema operativo. I processi hanno anche la responsabilità di non scrivere nella stessa locazione simultaneamente.

Per illustrare il concetto di cooperazione tra processi si consideri il problema del produttore/consumatore e una sua possibile soluzione, ovveró l'implementazione di un buffer che viene riempito dal produttore e svuotato dal consumatore. 
I due processi devono essere sincronizzati in modo tale che il consumatore non tenti di consumare un’unità non ancora prodotta.

Si possono utilizzare due tipi di buffer.
Quello illimitato e quello limitato.
Quello illimitato permette al produttore di produrre senza restrizioni.

Il buffer condiviso è realizzato come un array circolare.