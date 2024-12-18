Un **circuito combinatorio** è un circuito in cui gli *output* dipendono esclusivamente dagli *input* attuali (esso non "ricorda" gli *input* precedenti a quelli attuali, infatti un circuito combinatorio è privo di memoria). Dunque, gli *output* vengono ottenuti "combinando" e manipolando i valori presi in *input*. Un esempio basilare di circuito combinatorio può essere una qualsiasi [[Porte logiche|porta logica]].

La specifica di funzione di un circuito combinatorio esprime gli *output* in funzione degli *input*. La specifica di tempo, invece, risulterà in un intervallo di tempo delimitato dal minimo e dal massimo *delay* tra rilevamento degli *input* e restituzione degli *output*.
___
Per costruire un circuito combinatorio, è importante seguire le regole della **composizione combinatoria**. Le principali direttive da tenere a mente sono le seguenti:
- ogni elemento di un circuito combinatorio dev'essere anch'esso combinatorio;
- ogni nodo di un circuito combinatorio o trasporta un *input* nel circuito o è connesso a esattamente un *output* di un elemento del circuito;
- un circuito combinatorio non può contenere cicli, e ogni percorso possibile all'interno del circuito può passare per un nodo del circuito al massimo una volta.
___
Graficamente, un circuito combinatorio viene rappresentato con il rettangolo tipico del circuito generico, e racchiusa al suo interno la dicitura "***CL***" (che sta per "*combinational logic*"), come nel seguente esempio:

![[combinationalcircuit.png]]

A volte, per semplificare la rappresentazione di un circuito combinatorio, si riassumono più *input* o più *output* in una sola linea, attraversata da uno *slash* (`/`) e dotata di un numero che indica l'ammontare di segnali racchiusi nella linea stessa; questo tipo di rappresentazione viene definito "***bus***". Ad esempio, un circuito con un *bus* a 3 segnali in *input* e uno a 2 segnali in *output* può essere rappresentato nel modo seguente:

![[combinationalcircuit_bus.png]]

Se il numero di segnali non è rilevante, o se risulta ovvio per qualche motivo, l'indicatore dello stesso può essere omesso.
___
La specifica di funzione di un circuito combinatorio può essere espressa con una tavola di verità o con un'equazione booleana; analizziamo, in particolare, quest'ultimo metodo.

Un'**equazione booleana** viene espressa mediante variabili binarie, che possono dunque essere `True` o `False` (1 o 0). Per poter approfondire al meglio questo tipo di equazione, è opportuno innanzitutto imparare alcuni termini specifici:
- una variabile priva di negazioni si trova nella sua "forma vera" (***true form***);
- il "**complemento**" di una variabile è il suo inverso;
- una variabile (o il suo complemento) viene definita anche come un "***literal***";
- l'*AND* di uno o più *literals* viene anche detto "**prodotto**" o "**implicante**";
- l'*OR* di uno o più *literals* viene anche detto "**somma**";
- un prodotto che coinvolge tutti gli *input* di un determinato circuito viene detto "**mintermine**" (***minterm***) di quel circuito;
- una somma che coinvolge tutti gli *input* di un determinato circuito viene detto "**maxtermine**" (***maxterm***) di quel circuito.

Avendo stabilito questo glossario, risulta ora cruciale stabilire una **gerarchia** dei vari operatori di un'equazione booleana. In una qualsiasi equazione booleana, l'ordine di precedenza dei tre operatori fondamentali è:
1. NOT
2. AND
3. OR

A partire da una tavola di verità, ci sono principalmente due modi di arrivare a un'equazione booleana che descriva il funzionamento di un circuito combinatorio, a seconda della forma di tale equazione e di come ci si arriva:
- la forma "***sum of products***" (o **SOP**);
- la forma "***product of sums***" (o **POS**).

La forma **SOP** consiste nello scrivere l'equazione booleana relativa a un circuito combinatorio sommando tutti i mintermini (quindi, i prodotti) del circuito stesso per cui l'*output* risulta essere `True`. La forma **POS**, invece, consiste nello scrivere l'equazione booleana relativa a un circuito combinatorio moltiplicando tutti i maxtermini (quindi, le somme) per cui l'*output* risulta essere `False`. Nel fare ciò, è importante ricordare che, in una tavola di verità, a ogni riga viene associato un mintermine che sia `True` per quella riga e un maxtermine che sia `False` per quella riga.

Alternativamente, la forma SOP può essere scritta utilizzando la notazione Σ, che prende in argomento i mintermini da considerare o gli indici delle righe della tavola di verità corrispondenti a tali mintermini; ad esempio:
$$F(A, B) = Σ(m₁, m₃)$$
$$F(A, B) = Σ(1, 3)$$
La forma POS, inoltre, può essere scritta utilizzando la notazione Π, che prende in argomento i maxtermini da considerare o gli indici delle righe della tavola di verità corrispondenti a tali maxtermini; ad esempio:
$$F(A, B) = Π(M₀, M₂)$$
$$F(A, B) = Π(0, 2)$$
