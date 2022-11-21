Abbiamo appena descritto una soluzione software al problema della sezione critica. Parliamo in questo casi di _soluzione basata sul software_, perché l’algoritmo garantisce la mutua esclusione senza richiedere alcun supporto speciale dal sistema operativo né istruzioni hardware specifiche. Tuttavia, come già detto, soluzioni basate sul software come quella di Peterson non garantiscono il loro funzionamento su architetture elaborative moderne. In questo paragrafo presentiamo tre istruzioni hardware che forniscono supporto per risolvere il problema della sezione critica. Queste primitive possono essere utilizzate direttamente come strumenti di sincronizzazione, oppure come basi per costruire meccanismi di sincronizzazione più astratti.

### 6.4.2 [[Istruzioni hardware]]