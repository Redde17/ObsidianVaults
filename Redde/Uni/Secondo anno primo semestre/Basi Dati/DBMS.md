# DBMS
Il **DBMS** (**D**ata**B**ase **M**anagement **S**ystem) è un sistema software per gestire collezioni di dati (basi di dati), che siano grandi, condivise e persistenti. I **DBMS** assicurano **affidabilità** (resistenza ai malfunzionamenti), **privatezza**, **efficienza** (risorse e tempi), ed **efficacia** (produttività).

## Basi di dati
Le [basi di dati o banca dati](https://it.wikipedia.org/wiki/Base_di_dati) , sono un insieme di dati strutturati, ovvero omogenei per contenuto e formato, memorizzati in un computer, rappresentando di fatto la versione digitale di un archivio dati o schedario.

### Caratteristiche delle basi di dati

#### Dimensione
Le basi di dati sono di dimensioni nettamente maggiori della memoria centrale dei sistemi di calcolco utilizzati e il limite deve essere solo quello fisico dei dispositivi utilizzati.

#### Condivisione 
Ogni organizzazione, specie se grande, è divisa in settori o comunque svolge diverse attività, ciascun settore/attività ha un sottosistema informativo non necessariamente disgiunto.

#### Persistenza
Le basi di dati hanno un tempo di vita indipendente dalle singole esecuzioni dei programmi che le utilizzano.

## DBMS - file system
La gestione di insiemi di dati grandi e persistenti è possibile anche attraverso sistemi più semplici come gli ordinari file system dei sistemi operativi.
I file system prevedono forme rudimentali di condivisione: "tutto o niente".
I DBMS estendo le funzionalità dei file system fornendo più servizi ed in maniera integrata.

Nei programmi tradizionali che accedono a file, ogni programma contiene una descrizione della struttura del file stesso, con i conseguenti rischi di incoerenza fra le descrizioni fra le descrizioni e i file stessi.
![[Pasted image 20220930095939.png]]

Nei DBMS esiste una porzione della base di dati che contiene una descrizione centralizzata dei dati, chiamata catalogo o dizionario, che può essere utilizzata dai vari programmi.
![[Pasted image 20220930095946.png]]

## I modelli di dati
I modelli di dati sono un insieme di concetti per organizzare i dati che permette di :
- Rappresentare dei dati a livelli diversi
- Formalismo matematico per esprimere meccanismi di strutturazione

I modelli di dati si dividono in :
- Modello concettuale 
- Modello logico 