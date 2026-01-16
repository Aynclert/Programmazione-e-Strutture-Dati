
## Il tipo astratto *Lista*
- Definizione: sequenza di elementi di un determinato tipo, in cui è possibile aggiungere o togliere elementi
	- è possibile specificare la *posizione* relativa nella quale l'elemento va aggiunto o tolto

## Funzioni delle Liste

| Sintattica                                 | Semantica                                                                                                                                                    |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Nome tipo: List  Tipi usati: Item, boolean | Dominio: insieme di sequenze L=a1,....,an di tipo Item. L'elemento nil rappresenta la lista vuota                                                            |
| newList() -> List                          | newList()-> nil   -Post: l= nil                                                                                                                              |
| isEmpty(List)-> boolean                    | isEmpty(I)-> b -Post: se l = nil allora b = true altrimenti b = false                                                                                        |
| addHead(List, Item) -> List                | addHead(l, e)-> I' -Post: l =<a1,a2,...an> AND l' = <e,a1,...,an>                                                                                            |
| removeHead(List) -> List                   | removeHead(l) ->l' -Pre: l = <a1,a2,..,an> n>0  -Post: l' = <a2,a3,..,an                                                                                     |
| getFirst(List) -> Item                     | getHead(I) -> e  -Pre: l=<a1,a2,..,an> n>0   -Post: e=a1                                                                                                     |
| insertItem(List, Item, int) -> List        | insertItem(l, e, pos) -> l'  -Pre: l = <a1,...,a<sub>n+1</sub>> & 1<= pos<= n+1  -Post: l = <a1,..,a<sub>pos</sub>,..,a<sub>n+1</sub>> & a<sub>pos</sub> = e |
| insertTail(List, Item) -> List             | insertTail(l, e) -> l'  -Post: l=<a1,...,an> & l' = <a1,....,an,e>                                                                                           |
| reverseList(List, Item) -> List            | reverseList(l) -> l'    -Post: l=<a1,a2,...,an> AND l'=<an,...,a2,a1>                                                                                        |
| cloneList(List) -> List                    | cloneList(l) -> l'   -Post: l=<a1,a2,...,an> AND l'=<a1,a2,...,an>                                                                                           |

## Progettazione: Liste Concatenate
---
- Ogni elemento di una lista concatenata è un record con un campo puntatore che serve da collegamento per il successivo.
- Si accede alla struttura attraverso il puntatore al primo record.
- Il campo puntatore dell'ultimo record contiene il valore NULL.

Per accedere ad un generico elemento di una lista occorre **scandire sequenzialmente**gli elementi della lista.

## Progettazione: Inserimento in testa
---
Per inserire un nuovo elemento nella lista concatenata L, basta inserire l'elemento in un nuovo nodo da aggiungere in testa alla lista
1. si alloca il nuovo nodo N
2. si aggiunge il collegamento con il record iniziale della lista
3. si aggiorna L facendolo puntare ad N

## Progettazione: Eliminazione in testa
---
Per eliminare un elemento in una lista concatenata L basta è eliminarlo in testa alla lista
1. si crea un puntatore temporaneo T, copia di L
2. si aggiorna l facendolo puntare al successivo di L
3. si elimina il nodo puntato da T, liberando la memoria

## Progettazione: Visita di una lista
---
- Alcuni operatori richiedono una **visita** parziale o totale della lista
- Esempi di visita totale:
	- calcolo della size
	- stampa degli elementi
- Esempi di visita parziale:
	- inserimento o rimozione in una posizione i;
	- ricerca di un elemento
- **Calcolo della size**: scorriamo i nodi incrementando un contatore
	- ottimizzazione: mantenere un contatore da incrementare ad ogni inserimento e decrementare ad ogni cancellazione.

## Implementazione
---
1. Dichiarare il tipo lista, e istanziarla riservando memoria e inizializzarla vuota.
2. Dichiarare una struttura auto-referenziale per i nodi, contenenti i dati necessari ed un puntatore al prossimo elemento della lista

```C
typedef struct List *list;
struct List {
	int size;
	struct node *head;
};
List list = malloc(sizeof(struct List));
list->size = 0;
list->head = NULL;

struct node{
	Item value;
	struct node *next;
};
```
- Per iterare sui nodi si può usare un ciclo for operante su di un puntatore temporaneo *p* di tipo **struct node** con indirizzo list->head:
```C
struct node *p;
int i;

for(p = list->head; p != NULL; p = p->next)
	outputItem(p->value);
```

## Istanziare un nodo
---
- Man mano che costruiamo la nostra lista, creiamo dei nuovi nodi da aggiungere alla lista
- I passi per creare un nodo sono:
	1. allocare la memoria necessaria
	2. memorizzare i dati nel nodo
	3. inserire il nodo nella lista

- Per creare un nodo ci sere un puntatore temporaneo che punti al nodo :
```C
struct node* new_node;
```
- Possiamo usare la malloc per allocare la memoria necessaria e salvare l'indirizzo in new_code:
```C
new_node = malloc(sizeof(struct node));
```
 - new_node adesso punta ad un blocco di memoria che contiene la struttura di tipo node.

## searchItem(l, i)
---
- Dati una lista l e un elemento val, restituisce:
	- la posizione della lista in cui appare la prima occorrenza dell'elemento
	- -1 se l'elemento non è presente
- Richiede una ***visita finalizzata*** della lista: usciamo dal ciclo quando troviamo l'elemento cercato oppure quando raggiungiamo la fine della lista
- Possiamo ottenere sia il riferimento all'Item ricercato, sia la sua posizione, implementando la funzione con il seguente prototipo: Item searchItem(List list, Item item, int * pos)

## Eliminazione
---
Per eliminare un elemento in una lista concatenata L:
1. si fanno avanzare due puntatori Prev e P fino a che P punta al nodo da eliminare;
2. si aggiorna il nodo puntato da Prev, facendolo puntare al successivo di P
3. si elimina il nodo puntato da P, liberando la memoria

## Inserimento
---
Per inserire un elemento in una lista concatenata L:
1. si fa avanzare un puntatore P, fino a che punta al nodo precedente alla posizione dell'inserimento;
2. si crea il nuovo nodo e lo si fa puntare al successivo di P;
3. si fa puntare P al nuovo nodo.

## Reverse
---
Per invertire una lista concatenata L:
1. **per ogni nodo** (con i nodi fino a Prev già invertiti) si utilizzano due puntatori Prev e P;
	1. si salva il successivo di P in un puntatore temporaneo Temp
	2. si aggiorna il nodo puntato da P, facendolo puntare a Prev
	3. si fanno avanzare P e Prev
2. si aggiorna la testa facendola puntare all'ultimo nodo

## CloneList
---
- Diverse scelte progettuali possibili
	- clonare solo al struct list:
		- i nodi sono gli stessi. una modifica su una lista viene riflessa nell'altra
	- clonare i nodi ma non gli item
		- modifiche alla struttura di una lista non vengono riflesse nell'altra, ma se si modifica un item, risulta modificata in entrambe le liste
	- clonare i nodi e gli item
		- le liste, una volta create, sono totalmente indipendenti.

