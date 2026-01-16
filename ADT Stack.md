
- Una ***pila*** è una sequenza di elementi di un determinato tipo, in cui è possibile aggiungere o togliere elementi esclusivamente da un unico lato (***top*** dello stack).
	- la pila è una struttura dati *lineare* a *dimensione variabile* in cui si può accedere direttamente solo al ***primo*** elemento della lista
	- non è possibile accedere ad un elemento diverso dal primo **se non dopo** aver eliminato tutti gli elementi che lo precedono (inseriti dopo)
	- lista gestita con la modalità ***LIFO (Last-In-First-Out)*** cioè l'ultimo elemento inserito nella sequenza sarà il primo ad essere eliminato

| Sintattica                                          | Semantica                                                                                    |
| --------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| Nome del tipo: Stack      Tipi usati: Item, boolean | Dominio: insieme di sequenze S=a1,…,an di tipo Item L’elemento nil rappresenta la pila vuota |
| newStack() -> Stack                                 | newStack() -> s     -Post: s=nil                                                             |
| isEmptyStack(Stack) -> boolean                      | isEmptyStack(s) -> b     -Post: se s=nil allora b = true altrimenti b = false                |
| push(Stack, Item) -> Stack                          | push(s, e) -> s'     -Post: s = <a1, a2, … an> AND s’ = <e, a1, …, an>                       |
| pop(Stack, Item) -> Stack                           | pop(s) → s’     -Pre: s = <a1, a2, …, an> n>0     -Post: s’ = <a2, …, an>                    |
| top(Stack) -> Item                                  | top(s) → e     -Pre: s = <a1, a2, …, an> n>0   -Post: e = a1                                 |

## Implementazione
---
Tra le possibili implementazioni, le più usate sono realizzate tramite:
- array
- lista concatenata

### Implementazione con Array
---
- Lo stack è implementato come un puntatore ad una **struct stack** che contiene due elementi:
	- un array di **MAXSTACK** elementi
	- un intero che indica la posizione del top dello stack
	- quando lo stack si riempie, non è possibile eseguire l'operazione push...

### Implementazione con Lista
---
- Il tipo stack è definito come un puntatore ad una struct che contiene
	- un elemento **items** di tipo **list**
	- non serve più **MAXSTACK** 
	- anche se abbiamo un solo elemento nella struct, continuiamo a definire il tipo stack come puntatore a **struct stack** per non cambiare la definizione nell'header file.