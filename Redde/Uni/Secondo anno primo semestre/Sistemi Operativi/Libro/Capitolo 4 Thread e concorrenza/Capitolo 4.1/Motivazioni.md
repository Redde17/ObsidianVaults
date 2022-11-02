La maggior parte delle applicazioni per i moderni computer è multithread. Di solito, un’applicazione si codifica come un processo a sé stante comprendente più thread di controllo. Alcuni esempi di applicazioni multithread sono i seguenti.
-   Un’applicazione che crea miniature di foto (thumbnails) da una raccolta di immagini può utilizzare un thread distinto per generare una miniatura di ciascuna immagine.
-   Un web browser può avere un thread per rappresentare sullo schermo immagini e testo e un altro thread per scaricare i dati dalla rete.
-   Un word processor può avere un thread per la rappresentazione grafica, uno per la risposta all’input da tastiera e uno per la correzione ortografica e grammaticale eseguita in background.

Le applicazioni possono anche essere progettate per sfruttare le capacità di elaborazione sui sistemi multicore. Tali applicazioni possono eseguire diverse attività che utilizzano intensivamente la cpu in parallelo sui diversi core di elaborazione.