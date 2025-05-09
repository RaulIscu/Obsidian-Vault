### Introduzione

Per poter valutare l’efficienza di un algoritmo, così da confrontarlo con altri che risolvono lo stesso problema, bisogna essere in grado di valutarne il **costo computazionale**, ovvero il suo tempo di esecuzione e le sue necessità in termini di memoria (salvo ove diversamente specificato, la grandezza che verrà valutata maggiormente nel corso è il tempo di esecuzione dell’algoritmo). 

In generale, questa valutazione è complicata e contiene spesso dettagli trascurabili, per cui ci piacerebbe limitarci a dare una visione più astratta, e valutare solo quello che informalmente possiamo chiamare “**tasso di crescita**”, cioè la velocità con cui il tempo di esecuzione cresce all’aumentare della dimensione dell’*input*. Poiché per piccole dimensioni dell’*input* il tempo usato è comunque poco, tale valutazione è più interessante quando la dimensione dell’*input* è sufficientemente grande, per questo si parla di "**efficienza asintotica**" degli algoritmi.

Inoltre, siccome la velocità dello specifico calcolatore usato influisce solo per una costante moltiplicativa, vogliamo descrivere un modello che riesca a prescindere da essa. Infine, essendo il tempo di esecuzione una quantità necessariamente positiva, assumeremo in generale che tutte le funzioni coinvolte siano asintoticamente non negative.

Ci sono varie forme di notazione asintotica, principalmente tre:
- la **notazione *O***, o "limite asintotico superiore";
- la **notazione *Ω***, o "limite asintotico inferiore";
- la **notazione *θ***, o "limite asintotico stretto".
___
### La notazione *O*

Partiamo dalla **notazione *O***. Date due funzioni *f(n)* e *g(n)*, entrambe positive, si dice che "***f(n)* è un *O(g(n))***" se esistono due costanti *c* e *n₀* tali che, per ogni *n ≥ n₀*, vale che:
$$0 ≤ f(n) ≤ c ⋅ g(n)$$
Graficamente, deve valere ciò:

![[notazioneO.png]]
In *O(g(n))*, dunque, troviamo tutte le funzioni "**dominate**" dalla funzione *g(n)*. La notazione *O* definisce così quello che è il limite asintotico superiore della funzione *f(n)*: una volta superato un certo valore *n₀*, l'andamento della funzione sarà limitato dalla funzione *cg(n)*, rimanendo sempre al di sotto di quest'ultima.

Ad esempio, avendo *f(n) = 3n + 3*, si può affermare che *f(n) = O(n)*, in quanto esistono *c* (ad esempio *c* = 6) e *n₀* (ad esempio *n₀ = 1*) tali che venga rispettata la condizione stabilita in precedenza (infatti, *6n ≥ 3n + 3* per ogni *n ≥ 1*). Invece, avendo *f(n) = n² + 4n*, si può affermare che *f(n) = O(n²)*, in quanto esistono *c* (ad esempio *c = 5*) e *n₀* (ad esempio *n₀ = 1*) tali che venga rispettata la condizione stabilita in precedenza (infatti, *5n² ≥ n² + 4n*).

Possiamo notare un pattern: infatti, concludiamo che un polinomio di primo grado si trova sempre in *O(n)*; un polinomio di secondo grado, invece, si trova in *O(n²)*, e così via. In generale, infatti, **sia *f(n)* un polinomio di grado *i*, possiamo affermare che *f(n)* è in *O(nⁱ)***.

È facile convincersi che, data una funzione *f(n)*, esistono infinite funzioni *g(n)* per cui *f(n)* risulta un *O(g(n))*.
___
### La notazione *Ω*

Parliamo, ora, della **notazione *Ω***. Date due funzioni *f(n)* e *g(n)*, entrambe positive, si dice che "***f(n)* è un *Ω(g(n))***" se esistono due costanti *c* e *n₀* tali che, per ogni *n ≥ n₀*, vale che:
$$f(n) ≥ c ⋅ g(n)$$
Graficamente, deve valere ciò:

![[notazioneΩ.png]]
In *Ω(g(n))*, dunque, troviamo tutte le funzioni che "**dominano**" la funzione *g(n)*. La notazione *Ω* definisce così quello che è il limite asintotico inferiore della funzione *f(n)*: una volta superato un certo valore *n₀*, l'andamento della funzione sarà limitato dalla funzione *cg(n)*, rimanendo sempre al di sopra di quest'ultima.

Ad esempio, avendo *f(n) = 2n² + 3*, si può affermare che *f(n) = Ω(n²)*, in quanto esistono *c* (ad esempio *c = 2*) e *n₀* (in questo caso, qualunque valore) tali che venga rispettata la condizione stabilita in precedenza (infatti, *2n² + 3 ≥ n²* per ogni *n ∈ R*).

Anche per questa notazione vale la stessa proprietà della notazione *O*: in generale, infatti, **sia *f(n)* un polinomio di grado *i*, possiamo affermare che *f(n)* è in *Ω(nⁱ)***.
___
### Ordini di grandezza per le notazioni *O* e *Ω*

Unendo i concetti di limite asintotico inferiore e superiore appena spiegati, possiamo definire una **gerarchia di ordini di grandezza** che rispecchia, in realtà, quella che vale per le successioni numeriche:
- un logaritmo domina qualunque costante;
- una radice domina qualunque logaritmo;
- un polinomio domina qualunque radice;
- un esponenziale domina qualunque polinomio;
- un fattoriale domina qualunque esponenziale;
- una tetrazione domina qualunque fattoriale.

Per "**domina**", si intende che la prima funzione *f(n)* si trova in *Ω(g(n))*, dove *g(n)* è la seconda funzione del confronto; possiamo ripercorrere la scala al contrario, affermando invece che una funzione "**viene dominata**" da un'altra, ovvero che la prima funzione *f(n)* si trova in *O(g(n))*, dove *g(n)* è la seconda funzione del confronto.

Per comodità, di seguito si ricorda la gerarchia degli ordini di grandezza in maniera compatta:
$$1 < log^a(n) < \sqrt[b]{n} < n < n ⋅ log^c(n) < n^d < e^n < n! < n^n$$
___
### La notazione *θ*

Date due funzioni *f(n)* e *g(n)*, entrambe positive, si dice che "***f(n)* è un *θ(g(n))***" se esistono tre costanti *c₁*, *c₂* e *n₀* tali che, per ogni *n ≥ n₀*, vale che:
$$c_1 ⋅ g(n) ≤ f(n) ≤ c_2 ⋅ g(n)$$
In altre parole, *f(n) = θ(g(n))* se è contemporaneamente in *O(g(n))* e in *Ω(g(n))*. Graficamente, deve valere ciò:

![[notazioneθ.png]]
In *θ(g(n))*, dunque, si trovano **le funzioni *f(n)* che si comportano come *g(n)***.

Ad esempio, avendo *f(n) = 3n + 3*, si può affermare che *f(n) = θ(n)*, in quanto esistono *c₁* (ad esempio, *c₁ = 3*), *c₂* (ad esempio, *c₂ = 4*) e *n₀* (ad esempio, *n₀ = 3*) tali che venga rispettata la condizione stabilita in precedenza (infatti, *3n ≤ 3n + 3 ≤ 4n* per ogni *n ≥ 3*).
___
### Calcolo della notazione asintotica mediante limiti

In generale, possiamo formulare alcune regole per facilitare il **calcolo delle notazioni asintotiche** utilizzando dei **limiti**.

Di seguito, le regole in questione formalizzate in maniera compatta:
$$\lim_{n \to +\infty}\frac{f(n)}{g(n)} = k > 0, \mbox{ allora } f(n) = θ(g(n))$$
$$\lim_{n \to +\infty}\frac{f(n)}{g(n)} = +\infty, \mbox{ allora } f(n) = Ω(g(n)) \mbox{ ma } f(n) \ne θ(g(n))$$
$$\lim_{n \to +\infty}\frac{f(n)}{g(n)} = 0, \mbox{ allora } f(n) = O(g(n)) \mbox{ ma } f(n) \ne θ(g(n))$$
La prima afferma che, se il limite per *n* che tende a +∞ del rapporto tra due funzioni *f(n)* e *g(n)* è pari a una costante positiva, allora si ottiene che *f(n)* è in *θ(g(n))*. La seconda afferma che, se lo stesso limite è pari a +∞, allora si ottiene che *f(n)* è in *Ω(g(n))*, ma non è in *θ(g(n))*. Infine, la terza afferma che, se lo stesso limite è pari a 0, allora si ottiene che *f(n)* è in *O(g(n))*, ma non è in *θ(g(n))*.

Invece, se il limite in questione **non esiste**, sarà necessario ricorrere ad altri metodi.
___
### Algebra della notazione asintotica

Per semplificare il calcolo del costo computazionale tramite la notazione asintotica, è possibile utilizzare anche tre **regole algebriche**: la regola delle **costanti moltiplicative**, la regola della **commutatività della somma**, e la regola della **commutatività del prodotto**.

La regola delle **costanti moltiplicative** si esplica in tre sotto-regole, quante sono le varie forme di notazione asintotica:

$$\mbox{per ogni } k > 0 \mbox{ e } f(n) \ge 0, \mbox{ se } f(n) \mbox{ è in } O(g(n)) \mbox{ allora lo è anche } k ⋅ f(n)$$
$$\mbox{per ogni } k > 0 \mbox{ e } f(n) \ge 0, \mbox{ se } f(n) \mbox{ è in } Ω(g(n)) \mbox{ allora lo è anche } k ⋅ f(n)$$
$$\mbox{per ogni } k > 0 \mbox{ e } f(n) \ge 0, \mbox{ se } f(n) \mbox{ è in } θ(g(n)) \mbox{ allora lo è anche } k ⋅ f(n)$$

Informalmente, questa regola afferma che **le costanti moltiplicative possono essere ignorate** durante il calcolo di un qualsiasi limite asintotico, a patto però che queste non si trovino all'esponente della funzione su cui si sta lavorando.

La regola della **commutatività della somma** si esplica anch'essa in tre sotto-regole. Sia *f(n)* la somma di due funzioni *p(n)* e *q(n)*, per ogni *p(n), q(n) > 0*:

$$\mbox{se } p(n) \mbox{ è in } O(g(n)) \mbox{ e } q(n) \mbox{ è in } O(h(n)), \mbox{ allora } f(n) \mbox{ sarà in } O(g(n) \mbox{ } + \mbox{ } h(n)) = O(\mbox{max}(g(n), h(n)))$$
$$\mbox{se } p(n) \mbox{ è in } Ω(g(n)) \mbox{ e } q(n) \mbox{ è in } Ω(h(n)), \mbox{ allora } f(n) \mbox{ sarà in } Ω(g(n) \mbox{ } + \mbox{ } h(n)) = Ω(\mbox{max}(g(n), h(n)))$$
$$\mbox{se } p(n) \mbox{ è in } θ(g(n)) \mbox{ e } q(n) \mbox{ è in } θ(h(n)), \mbox{ allora } f(n) \mbox{ sarà in } θ(g(n) \mbox{ } + \mbox{ } h(n)) = θ(\mbox{max}(g(n), h(n)))$$

Informalmente, questa regola afferma che, data una funzione *f(n) = p(n) + q(n)*, allora **un qualsiasi limite asintotico di *f(n)* sarà uguale al massimo tra i limiti asintotici di *p(n)* e di *q(n)***.

Infine, la regola della **commutatività del prodotto** si esplica anch'essa in tre sotto-regole. Sia *f(n)* il prodotto di due funzioni *p(n)* e *q(n)*, per ogni *p(n), q(n) > 0*:

$$\mbox{se } p(n) \mbox{ è in } O(g(n)) \mbox{ e } q(n) \mbox{ è in } O(h(n)), \mbox{ allora } f(n) \mbox{ sarà in } O(g(n) \mbox{ } ⋅ \mbox{ } h(n))$$
$$\mbox{se } p(n) \mbox{ è in } Ω(g(n)) \mbox{ e } q(n) \mbox{ è in } Ω(h(n)), \mbox{ allora } f(n) \mbox{ sarà in } Ω(g(n) \mbox{ } ⋅ \mbox{ } h(n))$$
$$\mbox{se } p(n) \mbox{ è in } θ(g(n)) \mbox{ e } q(n) \mbox{ è in } θ(h(n)), \mbox{ allora } f(n) \mbox{ sarà in } θ(g(n) \mbox{ } ⋅ \mbox{ } h(n))$$

Informalmente, questa regola afferma che, data una funzione *f(n) = p(n) ∙ q(n)*, allora **un qualsiasi limite asintotico di *f(n)* sarà uguale al prodotto tra i limiti asintotici di *p(n)* e di *q(n)***.
___
### Sommatorie notevoli

Di seguito, alcune **sommatorie notevoli** che potranno tornare utile nel calcolo e nella semplificazione di notazioni asintotiche:
$$\sum_{i = 0}^{n}i = \theta(n^2) \mbox{, }\mbox{ }\mbox{ } \sum_{i= 0}^{n}2^i = \theta(2^n) \mbox{, }\mbox{ }\mbox{ } \sum_{i = 0}^{n}i2^i = \theta(n2^n) \mbox{, }\mbox{ }\mbox{ } \sum_{i = 0}^{n}log(i) = \theta(nlog(n)) \mbox{, }\mbox{ }\mbox{ } \sum_{i = 0}^{n}\frac{1}{i} = \theta(log(n)) \mbox{, }\mbox{ }\mbox{ } \sum_{i = 0}^{n}k^i = \theta(1) \mbox{ }\mbox{ se } k < 1$$