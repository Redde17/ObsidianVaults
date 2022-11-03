Il modello da molti a uno fa corrispondere molti thread a livello utente a un singolo thread a livello kernel. 

La gestione dei thread risulta efficiente perché viene effettuata da una libreria di thread nello spazio utente.
Tuttavia l’intero processo rimane bloccato se un thread invoca una chiamata di sistema di tipo bloccante. Inoltre, poiché un solo thread alla volta può accedere al kernel, è impossibile eseguire thread multipli in parallelo in sistemi multicore;

Tuttavia, pochissimi sistemi utilizzano ancora questo modello a causa della sua incapacità di trarre vantaggio dalla presenza di più core (che costituisco lo standard nei sistemi elaborativi moderni).

![[Pasted image 20221102170319.png]]