# Struttura di I/O
Una percentuale cospicua del codice di un sistema operativo è dedicata alla gestione dell’i/o; ciò è dovuto sia alla sua importanza per il progetto di un sistema affidabile ed efficiente, sia alla differente tipologia dei dispositivi.

*Un calcolatore general-purpose è composto da un insieme di dispositivi connessi mediante un bus comune.*

L’i/o guidato dalle [[Interruzioni]] è adatto al trasferimento di piccole quantità di dati, ma in caso di trasferimenti massicci può generare un **pesante sovraccarico (_overhead_)**; si pensi, per esempio, all’i/o da e verso nvs.
Per risolvere questo problema si utilizza le tecnica dell’accesso **diretto alla memoria (dma)**