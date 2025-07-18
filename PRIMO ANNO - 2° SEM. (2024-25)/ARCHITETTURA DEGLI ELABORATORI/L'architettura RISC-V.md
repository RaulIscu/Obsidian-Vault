### Cos'è una CPU?

Un **calcolatore** è composto da una miriade di vari componenti, suddivisibili in varie categorie e che interagiscono tutti tra loro. Uno dei più importanti componenti di un calcolatore, se non il più importante, è la sua CPU.

La **CPU** (o **Central Processing Unit**), detta anche "processore" di un calcolatore, rappresenta la parte attiva di quest'ultimo, la componente che esegue fedelmente le istruzioni di un programma. È in grado di effettuare operazioni aritmetiche, compiere dei controlli su di esse, inviare segnali per attivare i dispositivi di I/O (input/output), e altro ancora.

Tendenzialmente, un processore comprende due componenti principali:
- un'**unità di elaborazione dati** (o **datapath**), che provvede ad eseguire concretamente le operazioni da eseguire;
- un'**unità di controllo**, che indica al datapath, alla memoria e ai dispositivi di I/O che cosa fare con i dati ottenuti dalle varie operazioni, in base alle istruzioni fornite dal programma che sta venendo eseguito.

All'interno di un processore, poi, è possibile trovare un tipo particolare di memoria, la cosiddetta **memoria cache**, che consiste in una memoria di modeste dimensioni ma particolarmente veloce; essa è costruita utilizzando la tecnologia di memoria **SRAM**, o "**Static Random Access Memory**", più veloce ma più costosa delle memorie di tipo **DRAM**, o "**Dynamic Random Access Memory**".
___
### Cosa si intende per "architettura"?

Per facilitare la progettazione, la configurazione e l'utilizzo di un calcolatore, uno dei concetti più importanti da tenere a mente è quello dell'**astrazione**, e uno dei gradi più importanti di astrazione è l'**interfaccia tra l'hardware e il software di più basso livello**. Questa comunicazione tra le due parti avviene attraverso una sorta di "vocabolario", le cui parole sono dette "**istruzioni**"; l'insieme di queste istruzioni, e quindi il vocabolario stesso, viene detto **ISA** (**Instruction Set Architecture**), ossia "architettura dell'insieme di istruzioni", o più semplicemente "**architettura**" del calcolatore.

L'architettura di un determinato tipo di calcolatore comprende, quindi, tutto ciò che un programmatore dovrebbe sapere per scrivere un programma in **linguaggio macchina** (il linguaggio binario comprensibile direttamente dal calcolatore) correttamente funzionante. Tipicamente, comunque, il sistema operativo va ad **incapsulare** i dettagli sui dispositivi di I/O, sull'allocazione di memoria e su altre informazioni di basso livello, evitando al programmatore di dover gestire questi dettagli.

Una particolare architettura permette, così, di descrivere le funzionalità di un calcolatore in maniera completamente indipendente dall'hardware che la implementa. In genere, infatti, i progettisti distinguono tra **architettura** e **implementazione di un'architettura**: un'architettura è sostanzialmente una descrizione astratta del funzionamento di un calcolatore, mentre un'implementazione di tale architettura è un hardware che va a realizzare concretamente quest'ultima.
___
### L'architettura RISC-V

Si potrebbe pensare che i linguaggi utilizzati dai calcolatori siano molti e diversi tra loro, ma in realtà sono tutti relativamente **simili**, quasi come un insieme di dialetti che hanno radici nella stessa lingua originaria. Ciò comporta che, una volta appreso uno di questi linguaggi, sarà relativamente facile approcciarsi anche agli altri.

In questo corso, il linguaggio che verrà maggiormente approfondito è l'**architettura RISC-V** (dove la prima parte dell'acronimo sta per "**Reduced Instruction Set Computer**"), sviluppata nell'università di Berkeley a partire dal 2010. Per comprendere le sue peculiarità e i motivi per cui sta venendo utilizzato sempre più, confrontiamolo con un'altra architettura molto in voga prima della sua comparsa ed evoluzione, ossia l'**architettura CISC**, o "**Complex Instruction Set Computer**". Le differenze principali sono le seguenti:
- la CISC prevede istruzioni di dimensione e formato variabile, che necessitano di vari passaggi di decodifica, mentre la RISC-V lavora su **istruzioni di dimensione fissa**, permettendo così di passare alla successiva senza decodificare la precedente, o generalmente di effettuare delle decodifiche più semplici;
- la CISC lavora accedendo ad operandi salvati in memoria, necessitando quindi di molti accessi a quest'ultima per eseguire le istruzioni, mentre la RISC-V **effettua le operazioni tramite ALU e registri *in loco***, velocizzando il tutto e omettendo completamente l'accesso ad essa in vari casi;
- generalmente, la CISC opera con una pipeline più complessa, essendo anche le istruzioni previste più complicate e di dimensioni variabili, mentre la RISC-V, lavorando su istruzioni "fisse" e più semplici, permette anche di avere una **pipeline più veloce**.

Approfondendo il secondo punto, l'architettura RISC-V, in un'implementazione a 32 bit, prevede **32 registri da 32 bit** (o una parola) **ciascuno**, indicizzati da `x0` a `x31` (il registro `x0` conterrà sempre il valore 0). La presenza di questi registri, che saranno destinati a contenere gli operandi delle varie operazioni che si vogliono eseguire, permette un accesso molto più veloce ai dati stessi. Nominare i vari registri come `x0`, `x1`, `x2` e così via è una convenzione dell'architettura RISC-V; questa convenzione vale per tutti i registri ad eccezione di alcuni particolari, che hanno un nome personalizzato.

Inoltre, in tale tipo di architettura, si potranno accedere a un massimo di **$2^{30}$ parole di memoria indirizzate al byte**: per questo motivo, due variabili successive in memoria avranno indirizzi a distanza 4. Alla memoria si può accedere solamente attraverso istruzioni di **[[Assembly e RARS#Istruzioni di trasferimento dati|trasferimento dati]]**.

