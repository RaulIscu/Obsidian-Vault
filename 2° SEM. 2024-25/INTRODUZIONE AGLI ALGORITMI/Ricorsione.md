### Cos'è la ricorsione

Finora sono stati trattati algoritmi basati prevalentemente su cicli iterativi, come il ciclo *for* o il ciclo *while*; spesso, tuttavia, algoritmi iterativi possono essere riformulati sfruttando la "**ricorsione**". Un algoritmo ricorsivo è un algoritmo che risolve un determinato problema riapplicando sé stesso su versioni via via più semplici dello stesso problema.

Per comprendere meglio questa tecnica, riformuliamo un algoritmo già visto in forma ricorsiva. L'algoritmo di [[Ricerca|ricerca binaria]] si presta particolarmente a questa riformulazione; i passaggi di una ricerca binaria ricorsiva sarebbero i seguenti:
- ispezionare l'elemento centrale dell'*array*;
- se l'elemento in questione è uguale all'elemento cercato v, restituire il suo indice;
- se l'elemento in questione è maggiore di v, ridurre l'*array* alla sua metà inferiore e rieseguire la ricerca binaria su di essa;
- se l'elemento in questione è minore di v, ridurre l'*array* alla sua metà superiore e rieseguire la ricerca binaria su di essa.

Le funzioni ricorsive, in realtà, sono più comuni di quanto si possa pensare. Le troviamo anche in matematica, dove un tipico esempio di ciò è il **fattoriale**:
$$n! = \begin{cases}n ⋅ (n - 1)! & \mbox{se } n > 0 \\ 1 & \mbox{se } n = 0 \end{cases}$$
Analizzando questo esempio, possiamo riconoscere *n = 0* come il "**caso base**" del problema, ossia il suo sotto-problema minimo, corrispondente dunque alla versione più semplice possibile del problema stesso.

All'interno della risoluzione di un problema ricorsivo, **la catena di ricorsione viene ripetuta finché non viene raggiunto il caso base del problema**. Per questo motivo, nella giusta costruzione di un algoritmo ricorsivo è necessario avere almeno un caso base al suo interno, in quanto la sua assenza causerebbe l'algoritmo a continuare all'infinito.

Arriviamo, quindi, alla seguente definizione di algoritmo ricorsivo:

> Un algoritmo è detto **ricorsivo** quando è espresso in termini di sé stesso. Un algoritmo ricorsivo ha le seguenti proprietà:
> - la soluzione del problema complessivo è costruita risolvendo ricorsivamente uno o più sotto-problemi di dimensione minore, e combinando le soluzioni ottenute;
> - la successione dei sotto-problemi deve sempre convergere ad un sotto-problema che costituisca il caso base, il quale termina la ricorsione.

___
### Esempi di ricorsione

Di seguito, sono esposti alcuni **esempi** (in pseudocodice) di **algoritmi ricorsivi**:

```
def fattoriale(n):
	if n == 0:
		return 1
	return n * fattoriale(n - 1)
```

```
def ricerca_sequenziale_ric(A, v, n = len(A) - 1):
	if A[n] == v:
		return n

	if n == 0:
		return -1
	return ricerca_sequenziale_ric(A, v, n - 1)
```

```
def ricerca_binaria_ric(A, v, i_min = 0, i_max = len(A)):
	if i_min > i_max:
		return -1

	m = (i_min + i_max) // 2

	if A[m] == v:
		return m
	elif A[m] > v:
		return ricerca_binaria_ric(A, v, i_min, m - 1)
	else:
		return ricerca_binaria_ric(A, v, m + 1, i_max)
```

___
### Iterazione vs. Ricorsione

Qualsiasi problema risolvibile con un algoritmo ricorsivo può essere risolto anche con un algoritmo iterativo. Viene allora da chiedersi perché si dovrebbe considerare l'opzione della ricorsione, e in quali contesti (se ce ne sono) questa risulti più vantaggiosa.

Tendenzialmente, si preferisce utilizzare la **ricorsione** quando è possibile formulare la soluzione di un problema in modo aderente alla natura del problema stesso, o banalmente quando la versione iterativa della soluzione è molto più complessa. Invece, conviene generalmente utilizzare l'**iterazione** quando essa risulta implementabile in maniera altrettanto semplice e chiara rispetto alla ricorsione, o quando è importante tener conto dell'efficienza dell'algoritmo.

L'ultimo punto è forse il più importante. Infatti, ogni algoritmo richiede, per essere eseguito, una determinata **quantità di memoria**, necessaria per:
- conservare il codice che ne definisce il funzionamento;
- passare i parametri in *input* e restituire valori in *output*;
- memorizzare i valori delle sue variabili locali.

Per natura di un algoritmo ricorsivo, che richiama sé stesso un elevato numero di volte, esso richiederà solitamente molta più memoria rispetto a un normale algoritmo iterativo. Quindi, a grandi linee, **si tende a preferire l'iterazione alla ricorsione**, a meno che il problema posto non sia risolvibile in maniera veloce e intuitiva con quest'ultima.
___
### Equazioni di ricorrenza

Nel calcolo del **[[Costo computazionale|costo computazionale]]**, gli algoritmi ricorsivi danno vita a funzioni matematiche anch'esse ricorsive; le funzioni matematiche che esprimono il costo computazionale di algoritmi ricorsivi vengono anche dette "**equazioni di ricorrenza**".

Per comprendere meglio questo concetto, torniamo all'esempio del **fattoriale**. Il costo computazionale di tale algoritmo risulta essere:
$$ T = \begin{cases} T(n) = θ(1) + T(n - 1)& \mbox{se } n > 0 \\ T(0) = θ(1) & \mbox{se } n = 0 \end{cases}$$
La parte generica dell'equazione di ricorrenza che definisce *T(n)* contiene sempre almeno due addendi, di cui almeno uno contiene la parte ricorsiva (nell'esempio, *T(n - 1)*), mentre uno rappresenta il costo computazionale di ciò che viene eseguito fuori dalla parte ricorsiva (nell'esempio, *θ(1)*). Inoltre, così come per la definizione di algoritmi ricorsivi, anche l'equazione di ricorrenza deve necessariamente presentare un caso base (nell'esempio, *T(0)*).

Per sviluppare l'equazione di ricorrenza e quantificare più precisamente il costo computazionale di un algoritmo ricorsivo, si utilizzano diversi **metodi**:
- metodo **iterativo**;
- metodo di **sostituzione**;
- metodo dell'**albero**;
- metodo **principale**.
___
### Metodo iterativo

L'idea alla base del **metodo iterativo** è quella di sviluppare l'equazione di ricorrenza in modo da essere espressa come **somma di termini dipendenti dal caso generico e dal caso base**. Tuttavia, per l'elevato numero di calcoli da effettuare, esso risulta spesso inefficiente.

Consideriamo, ad esempio, la seguente equazione di ricorrenza:
$$T = \begin{cases} T(n) = θ(1) + T(n - 1) \\ T(1) = θ(1) \end{cases}$$
Proviamo a sviluppare il termine *T(n)* come somma dei suoi sotto-termini: se *T(n)* è definito come *θ(1) + T(n - 1)*, allora *T(n - 1)* sarà definito come *θ(1) + T(n - 2)*, e così via. Sviluppando *T(n)* in sotto-termini *k* volte, si ottiene:
$$T(n) = T(n - k) + \underbrace{θ(1) + θ(1) + \cdots + θ(1)}_{k \mbox{ volte}} = T(n - k) + k ⋅ θ(1)$$
Dopo un determinato numero di ricorsioni, però, l'equazione di ricorrenza raggiungerà il suo caso base, in questo caso *T(1)*. La catena, dunque, procederà finché *n - k = 1*, in modo che *T(n - k)* corrisponda a *T(1)*. Ne segue, dunque, che il numero di ricorsioni sarà:
$$k = n - 1$$
Una volta trovato *k*, basterà sostituirlo nell'equazione precedentemente trovata per calcolare il **costo computazionale generico** dell'algoritmo dell'esempio:
$$\begin{align} T(n) &= T(n - k) + k ⋅ θ(1) \\ &= T(n - (n - 1)) + (n - 1) ⋅ θ(1) \\ &= T(1) + θ(n) \\ &= θ(1) + θ(n) \\ &= θ(n) \end{align}$$

Vediamo un altro esempio, considerando la seguente equazione di ricorrenza:
$$T = \begin{cases} T(n) = T(\frac{n}{2}) + θ(1) \\ T(1) = θ(1) \end{cases}$$
Sviluppando *T(n)*, stavolta, si ottiene la seguente equazione generalizzata:
$$T(n) = T\left(\frac{n}{2^k} \right) + k ⋅ θ(1)$$
Sappiamo che il caso base è *T(1)*, che viene quindi raggiunto quando
$$\frac{n}{2^k} = 1$$
ossia quando il numero di ricorsioni è pari a:
$$k = log_2(n)$$
Risostituiamo *k* all'interno dell'equazione generalizzata, e facendo i calcoli si otterrà il costo computazionale generico dell'algoritmo:
$$\begin{align} T(n) &= T\left(\frac{n}{2^k} \right) + k ⋅ θ(1) \\ &= T(1) + log_2(n) ⋅ θ(1) \\ &= θ(1) + θ(log_2(n)) \\ &= θ(log_2(n)) \end{align}$$
___
### Metodo di sostituzione

L'idea alla base del **metodo di sostituzione** consiste nell'**ipotizzare una soluzione per l'equazione di ricorrenza**, e dimostrare poi tale ipotesi tramite l'**induzione**. Lo svantaggio, piuttosto evidente, di tale metodo, è quello di poter procedere solo per tentativi. 

Inoltre, si punta a cercare la funzione più piccola possibile se si sta cercando O, e quella più grande possibile se si sta cercando Ω, in quanto tutte le funzioni più grandi nel primo caso, o più piccole nel secondo, sarebbero soluzioni valide pur essendo potenzialmente molto imprecise nella loro approssimazione.

Consideriamo, ad esempio, la seguente equazione di ricorrenza:
$$T = \begin{cases} T(n) = T(n - 1) + θ(1) \\ T(1) = θ(1) \end{cases}$$
Ipotizziamo la soluzione "T(n) = O(n)", ossia che *T(n) ≤ kn* per una certa costante *k*. Per semplicità, conviene **sostituire le notazioni asintotiche** presenti all'interno dell'equazione con due costanti, riscrivendola come segue:
$$T = \begin{cases} T(n) = T(n - 1) + c \\ T(1) = d \end{cases}$$
Analizziamo ora il **caso base**, che si verifica in questo caso quando *n = 1*; per ipotesi, affermiamo che:
$$T(1) ≤ k ⋅ 1 \Rightarrow T(1) ≤ k \Rightarrow d ≤ k$$
Dunque, la disuguaglianza ipotizzata sarà vera se e solo se varrà che *d ≤ k*.

A questo punto, consideriamo il **passo induttivo**. Vogliamo verificare che l'ipotesi *T(n) ≤ kn* valga per un *n* generico; sapendo che *T(n) = T(n - 1) + c* (dall'equazione di ricorrenza), possiamo affermare che:
$$T(n - 1) + c ≤ kn$$
Per ipotesi, *T(n - 1) ≤ k(n - 1)*, dunque sostituendo nella disequazione si ottiene che:
$$k(n - 1) + c ≤ kn \Rightarrow kn - k + c ≤ kn \Rightarrow c ≤ k$$
L'ipotesi è corretta solo se vengono rispettate sia *d ≤ k* che *c ≤ k*; esistendo sicuramente almeno un tale valore di *k*, si può affermare che T(n) è in O(n).

Ipotizziamo, adesso, la soluzione "T(n) = Ω(n)", ossia che *T(n) ≥ hn* per una certa costante *h*. Applicando passaggi perfettamente analoghi a quelli utilizzati per verificare la prima ipotesi, si ottiene che:
$$\begin{align} c ≥ h \\ d ≥ h \end{align}$$
L'ipotesi è corretta solo se vengono rispettate entrambe queste disuguaglianze; esistendo sicuramente almeno un tale valore di *h*, si può affermare che T(n) è in Ω(n). Ovviamente, avendo verificato che T(n) è sia in O(n) che in Ω(n), si arriva alla conclusione che **T(n) è in θ(n)**.
___
### Metodo dell'albero

[pag. 62 - 63 - 64 - 65]
___
### Metodo principale

L'idea alla base del **metodo principale** consiste nell'**avere una formula in grado di calcolare rapidamente il costo computazionale** di un algoritmo. Per natura del metodo, il suo svantaggio più grande è la sua limitatezza: esso, infatti, può essere applicato solo su equazioni di ricorrenza espresse nel formato:
$$T(n) = \alpha ⋅ T\left(\frac{n}{\beta} \right) + f(n)$$
con *T(1) = θ(1)* e con f(n) pari a un qualsiasi costo computazionale espresso nella [[Notazione asintotica|notazione asintotica]] θ. Di seguito l'enunciato di questo metodo.

Dati *α ≥ 1* e *β ≥ 1*, una funzione asintoticamente positiva f(n) e un'equazione di ricorrenza della forma:
$$T = \begin{cases} T(n) = \alpha ⋅ T\left(\frac{n}{\beta} \right) + f(n) \\ T(1) = \theta(1) \end{cases}$$
si distinguono tre casi.

Nel **primo caso**, se per qualche costante *ε > 0* si ha che:
$$f(n) = O(n^{log_\beta(\alpha) - \epsilon})$$
allora possiamo affermare che:
$$T(n) = \theta(n^{log_\beta(\alpha)})$$
Poi, nel **secondo caso**, se si ha che:
$$f(n) = \theta(n^{log_\beta(\alpha)})$$
allora possiamo affermare che:
$$T(n) = \theta(n^{log_\beta(\alpha)} ⋅ log(n))$$
Infine, nel **terzo caso**, se per qualche costante *ε > 0*, per qualche costante *0 < c < 1* e per *n* abbastanza grande, si ha che:
$$f(n) = \Omega(n^{log_\beta(\alpha) + \epsilon}) \mbox{ } \mbox{ e che } \mbox{ } \alpha ⋅ f \left(\frac{n}{\beta} \right) ≤ c ⋅ f(n)$$
allora possiamo affermare che:
$$T(n) = θ(f(n))$$
