
- Una ***queue (coda***) è una sequenza di elementi di un determinato tipo, in cui gli elementi si aggiungono da un lato (***tail***) e si tolgono dall'altro (***head***)
- la sequenza viene gestita con la modalità ***FIFO (First-In-First-Out)***: il primo elemento inserito nella sequenza sarà il primo ad essere eliminato
- la coda è una struttura dati *lineare* a *dimensione variabile*
	- si può accedere direttamente solo alla testa (**head**) della lista
	- non è possibile accedere ad un elemento diverso da **head**, se non dopo aver eliminato tutti gli elementi che lo precedono (cioè quelli inseriti prima).

| Sintattica                                       | Semantica                                                                                    |
| ------------------------------------------------ | -------------------------------------------------------------------------------------------- |
| Nome del tipo: Queue   Tipi usati: Item, boolean | Dominio: insieme di sequenze S=a1,…,an di tipo Item L’elemento nil rappresenta la coda vuota |
| newQueue() -> Queue                              | newQueue() → q    -Post: q = nil                                                             |
| isEmptyQueue(Queue)-> boolean                    | isEmptyQueue(s) -> b    -Post: se q=nil allora b=true altrimenti b=false                     |
| enqueue(Queue, Item) -> Queue                    | enqueue(q, e) → q’    -Post:  q = <a1, …, an> AND q’ = <a1, …, an, e>                        |
| dequeue(Queue) -> Queue                          | dequeue(q) -> q'    -Pre: q = <a1, a2, …, an> n>0   -Post: q’ = <a2, …, an>                  |

## Implementazione con Lista Concatenata
---
- E' possibile  utilizzare gli operatori di:
	- rimozione dalla testa
	- aggiunta in coda
- Per motivi di efficienza, conviene avere accesso sia al primo elemento sia all'ultimo. Occorre modificare il tipo lista come un puntatore ad una struct che contiene:
	- un intero **numelem** che indica il numero di elementi della coda
	- un puntatore **head** ad uno **struct nodo**
	- un puntatore **tail** ad uno **struct nodo**

### Modifica Implementazione ADT #lista 
---
- Dobbiamo aggiungere il puntatore tail
- Poi bisogna modificare gli operatori principali:
	- *RemoveHead*
		- deve eventualmente aggiornare entrambi i puntatori head e tail
	- *addListTail*, grazie alla presenza del puntatore tail,
		- non deve più scorrere gli elementi della lista fino all'ultimo
		- deve aggiornare entrambi i puntatori head e tail

### Modifica removeHead (ADT List)
---
- Bisogna prima salvare il puntatore al nodo da eliminare (quello puntato da head)
- Head dovrà puntare al successivo
- A questo punto si può deallocare la memoria del nodo da rimuovere
- **Se la coda aveva un solo elemento, ora è vuota, per cui bisogna porre anche il puntatore tail a NULL**

### Modifica addListTail(ADT List)
---
- Dobbiamo anzitutto creare un nuovo nodo a cui dovrà puntare il puntatore tail
- poi bisogna distinguere il caso in cui la coda di input sia vuota e il caso in cui non lo sia
	- coda vuota: il puntatore head dovrà puntare al nuovo nodo
	- coda non vuoto: il puntatore next dell'ultimo nodo dovrà puntare a nuovo

## Implementazione con array
---
- La coda è implementata come un puntatore ad una **struct queue** che contiene tre elementi:
	- un array di **MAXQUEUE** elementi
	- un intero che indica la posizione ***head*** della coda
	- un intero che indica la posizione ***tail*** della coda
- Quando la coda si riempie, non è possibile eseguire l'operazione enqueue ...

### Problemi
---
- Se l'array viene gestito normalmente, cioè mantenendo head<= tail, ci sono dei problemi...
- se rimuoviamo uno alla volta i primi tre elementi in coda, otteniamo un array in cui risultano disponibili solo le posizioni a destra di tail, ma sono libere anche quelle a sinistra di head

### Soluzioni
---
- **Prima soluzione**: ad ogni rimozione si compatta l'array nelle posizioni iniziali, con uno shift degli elementi
	- TROPPO COSTOSO!
- **Seconda soluzione**: si gestisce l'array in modo circolare
	- in ogni istante, gli elementi della coda si trovano nel segmento head, head+1,..., tail-1, ma non necessariamente head<=tail
	- infatti, dopo aver inserito in posizione N-1, se c'è ancora spazio in coda, si inseriscono ulteriori elementi a partire dalla posizione 0
	- in questo modo si riesce a garantire che ad ogni istante la coda abbia capacità massima di N-1 elementi.