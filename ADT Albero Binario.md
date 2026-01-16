
## I grafi
---
- Un grafo orientato G è una coppia <N,A>, dove:
	- N è un insieme finito non vuoto (insieme di nodi) e
	- A sottoinsieme di NxN è un insieme finito di coppie ordinate di noti, detti archi (o spigoli o linee)
- Se < u<sub>i</sub>, u<sub>j</sub> > appartiene ad A, nel grafo vi è un arco da u<sub>i</sub> ad u<sub>j</sub>

## Gli Alberi
---
- L'Albero è una struttura informativa per rappresentare:
	- organizzazione gerarchiche di dati
	- partizioni successive di un insieme in sottoinsiemi disgiunti
	- procedimenti decisionali enumerativi

### Proprietà
---
- Ogni nodo ha un unico arco entrante, tranne la radice, che non ha archi entranti;
- Ogni nodo può avere 0 o più archi uscenti
	- i nodi senza archi uscenti sono detti foglie
- Un arco nell'albero induce una relazione padre-figlio
- A ciascun nodo è solitamente associato un valore, detto *etichetta* del nodo

## Concetti
---
- **Grado di un nodo**: numero di figli del nodo
	- **ordine dell'albero**: grado max fra tutti i nodi
- **Cammino**: sequenza di nodi dove il nodo <sub>i</sub> è padre del nodo n<sub>i+1</sub>, per 0<=i e minore di k
	- la lunghezza del cammino è k 
- **Livello di un nodo**: lunghezza del cammino dalla radice del nodo
	- Definizione ricorsiva: il livello della radice è 0, il livello di un nodo non radice è 1+livello del padre
- **Altezza dell'albero**: la lunghezza del più lungo cammino nell'albero
	- parte dalla radice e termina in una foglia

## Alberi come Struttura Ricorsiva
---
- Un albero è un insieme di nodi ai quali sono associate delle informazioni
- Tra i nodi esiste un nodo particolare che è la radice (livello 0)
- Gli altri nodi sono partizionati in sottoinsiemi che sono a loro volta alberi (livelli successivi):
	- Vuoto o costituito da un solo nodo (detto radice)
	- Radice a cui sono connessi altri alberi

## Alberi Binari
---
- Particolari alberi n-ari: ogni nodo può avere al più 2 figli
	- sottoalbero sinistro e sottoalbero destro
- Definizione ricorsiva:
	- un albero binario è vuoto
	- un albero binario è una terna (s, r, d), dove r è un nodo (radice), s e d sono alberi binari
- Alberi binari semplificati
	- Costruzione bottom-up
	- Operatori di selezione
	- Operatori di visita


| Sintattica                                          | Semantica                                                                                                          |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| Nome del tipo: BTree      Tipi usati: Item, boolean | Dominio: T= nil \| T = <N, T1, T2><br>N ϵ NODO, T1 e T2 sono BTree                                                 |
| newBTree() -> BTree                                 | newBTree() → T    -Post: T=nil                                                                                     |
| isEmpty(BTree) -> boolean                           | isEmpty(T) -> b     -Post: se T=nil allora b = true altrimenti b = false                                           |
| buildBTree(Btree, Btree, Item) -> BTree             | buildBTree(T1, T2, e) -> T    -Pre: e != nil     -Post: T = <N, T1, T2>; N ha etichetta e                          |
| getBTreeRoot(BTree) -> Item                         | getBTreeRoot(T) -> e    -Pre: T = <N, T<sub>left</sub>, T<sub>right</sub>> non è vuoto    -Post: N ha etichetta e  |
| getLeft(BTree) -> Btree                             | getLeft(T) -> T'    -Pre: T = <N, T<sub>left</sub>, T<sub>right</sub>> non è vuoto   -Post: T’ = T<sub>left</sub>  |
| getRight(BTree) -> Btree                            | getRight(T) -> T'   -Pre: T = <N, T<sub>left</sub>, T<sub>right</sub>> non è vuoto   -Post: T’ = T<sub>right</sub> |

### Realizzazione
---
- La realizzazione più diffusa è quella di una struttura a puntatori con nodi doppiamente concatenati
- Ogni nodo è una struttura con tre componenti:
	- Puntatore alla radice del sottoalbero sinistro
	- Puntatore alla radice del sottoalbero destro
	- Etichetta (useremo il tipo generico Item per questo campo)
- Un albero binario è definito come puntatore ad un nodo:
	- se l'albero binario è vuoto, puntatore nullo
	- se l'albero binario non è vuoto, puntatore al nodo radice


### Dichiarazione del tipo nodo
---
