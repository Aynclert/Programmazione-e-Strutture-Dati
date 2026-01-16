--- 
# Sviluppo di Programmi
---
- #Analisi 
	Specifica di _cosa fa_ il programma. Individuazione di:
		1. Dati di ingresso e loro vincoli ( #Precondizione);
		2. Dati in uscita e loro vincoli ( #Postcondizione).
- #Progettazione 
	Definisce _come_ il programma effettua la trasformazione specificata:
	1. Progettazione dell'algoritmo per raffinamenti successivi (stepwise refinement):
		1. Definizione degli step;
		2. Decomposizione funzionale.
- #Implementazione 
	1. Codifica dell'algoritmo nel linguaggio scelto;
	2. Verifica (testing) del programma (individuazione dei malfunzionamenti):
		1. Scelta dei casi di prova;
		2. Esecuzione del programma;
		3. Verifica dei risultati rispetto ai *risultati attesi*.
	3. Utilizzo del software di base e di un ambiente di sviluppo ...

## _**Dizionario dei Dati**_

E' buona norma utilizzare un _**dizionario dei dati**_ da arricchire durante le varie fasi dell'analisi.

|Identificatore|Tipo|Descrizione|
|:--:|:--:|:--:|
|Nome1|Tipo1|Descrizione1|
|Nome2|Tipo2|Descrizione2|
|...|...|...|


## Esempio

### Esempio di Analisi per "ordinamento di una sequenza di interi"
- Dati di ingresso : sequenza s di n interi
	- Pre-condizione: n > 0
- Dati di uscita: sequenza s1 di n interi
	- Post-condizione: s1 è una permutazione di s dove ∀ i ∈ [0, n-2], s1 <sub>i</sub>  ≤ s1<sub>i+1</sub>

|Identificatore|Tipo|Descrizione|
|:--:|:--:|:--:|
|s|sequenza|sequenza di interi in input|
|s1|sequenza|sequenza di interi in output|
|n|intero|numero di elementi nella sequenza|
|i|intero|indice per individuare gli elementi nella sequenza|

### Esempio di Progettazione per "ordinamento di una sequenza di interi"

1. Input sequenza s in un array a di dimensione n
2. Ordina array a di dimensione n
3. Output sequenza s1 contenuta in array a di dimensione n

#Raffinamento_del_programma_principale: definiamo delle funzioni corrispondenti agli step individuati

- input_array(a, n)
- ordina_array(a, n)
- output_array(a, n)


# #Selection_Sort

- Effettua una visita totale delle posizioni dell'array
	- visita totale: visitati in sequenza tutti gli elementi dell'array
- Per ogni posizione visitata individua l'elemento che dovrebbe occupare quella posizione
	- In questo modo, se *i* è la posizione corre *(0 <= i <n)*, tutti gli elementi nelle posizioni comprese tra 0 ed *i-1* rispettano l'ordinamento;
	- L'elemento che dovrebbe occupare la posizione *i* sarà il minimo tra quelli nelle posizioni comprese tra *i* ed *n-1*;

### Funzione ordina_array

1. #Analisi: Specifica simile a quella del programma principale, ma introduciamo l'array ...
2. #Progettazione : scegliamo come strategia di ordinamento _Selection Sort_
3. **Codifica e verifica**

#### #Analisi della funzione "ordina_array"

- Dati di ingresso: array a di interi di dimensione n;
	- Precondizione: n>0
- Dati di uscita: array a di interi di dimensione n
	- Postcondizione: l'array a in output contiene una permutazione degli elementi dell'array a in input tale che ∀ i ∈ [0, n-2], a[i] <= a[i+1]


| Identificatore |  Tipo  |                  Descrizione                   |
| :------------: | :----: | :--------------------------------------------: |
|       a        | array  |                array di interi                 |
|       n        | intero |             dimensione dell'array              |
|       i        | intero | indice per individuare gli elementi dell'array |

#### #Progettazione della funzione "ordina_array"

for(i=0; i< n-1; i++)
	1. Individua la posizione p dell'elemento minimo compreso tra le posizioni i e n-1 dell'array a
	2. Scambia gli elementi di a di posizioni i e p

#Raffinamento del programma principale: definiamo delle funzioni corrispondenti agli step individuati

- minimo(a, n)
- scambia(i, j)

#### #Analisi della funzione "minimo"

- Dati di ingresso: array a di interi di dimensione n
	- Precondizione: n>0
- Dati di uscita: min
	- Postcondizione: ∀ i ∈ [0, n-1], a[min] <= a[i] 

|Identificatore|Tipo|Descrizione|
|:--:|:--:|:--:|
|a|array|array di interi|
|n|intero|dimensione dell'array|
|min|intero|indice dell'elemento minimo|
|i|intero|indice per individuare gli elementi dell'array|

#### #Progettazione della funzione "minimo"

```C
min=0;
for(i = 1; i < n; i++)
	if(a[i] < a[min])
		min = i;
return(min);
```


### #Codifica

```C
void selection_sort(int *arr, int n){
	int i;
	for(i=0; i<n-1; i++){
		int min = minimo(&arr[i], n-1) + i;
		scambia(&arr[i], &arr[min]);
	}
}
```

```C
int minimo(int *arr, int n){
	int min = 0, i;
	for(i=1; i<n; i++)
		if (arr[min] > arr[i])
			min =i;
	return min;
}
```

```C
void scambia(int *x, int *y)
{
	int temp = *x;
	*x = *y;
	*y = temp;
}
```


# #Testing

- #Testing : esercitare il programma con dati ditest per verificare che il suo comportamento sia conforme a quello atteso:
	- Oracolo: output atteso;
	- Malfunzionamento: output differente da quello atteso.

Obiettivo del #Testing è l'individuazione dei vari malfunzionamenti, causati da errori o bug nel codice.

#Debugging : individuazione e correzione del difetto che ha causato il malfunzionamento.

Più è alta la fase in cui si introduce il difetto, maggiore è la difficoltaà nel rimuoverlo. La sua ricerca può essere fatta inserendo nel source code dei punti di ispezione dello stato delle variabili.

#### Classi di dati

Testare il programma con tutti i possibili dati di test è impraticabile...

#Obiettivo: individuareclassi di dati di test, selezionare un caso di test da ogni classe ed evitare casi di test ridondanti.

#Test_Suite : insieme di test effettuati sulle classi di dati.


##### Esempio ordinamento di un array

Aspetti da tener conto nella scelta dei casi di test:
- il numero n di elementi dell'array:
	- caso generale: array con n>1;
	- caso particolare: n=1.
- La disposizione degli elementi:
	- caso generale: array non ordinato:
	- array già ordinato in modo crescente;
	- array già ordinato in modo decrescente.


#Test_Suite 
- Test case 1 - TC1
	- array di input: 5
	- oracolo: 5
- Test case 2 - TC2
	- array di input: 1 2 3 4 5 6 7  8 9
	- oracolo: 1 2 3 4 5 6 7 8 9
- Test case 3 -TC3
	- array di input:
	- oracolo:
- Test case 4 - TC4
	- array di input:
	- oracolo:

### Automatizzare il #Testing : #Stream

In C, il termine *stream* indica una sorgente di input o una destinazione per l'output.
Molti programmi ottengono il loro input da uno stream e lo inviano ad un altro stream.
Programmi più grandi possono avere la necessità di usare più stream.
Gli stream:
- rappresentano file memorizzati da qualche parte (HD o altre memorie);
- sono associati a periferiche.

#### I/O da #Stream 

```C
char *fgets (char *s, int size, FILE *stream);
int fscanf(FILE *stream, const char *format, ...);
int fprintf(FILE *stream, const char *format, ...);
```

- *Fgets()* legge da *stream* fino al carattere newline (o finché size-1 caratteri sono stati letti) e memorizza in *s*.
	- Ritorna s in caso di successo, NULL in caso di errore o se si raggiunge la fine del file senza aver letto alcun carattere.
- *Fscanf()* legge da *stream* fino ad un carattere di spazio e non lo memorizza
	- restituisce il numero di dati letti e scritti con successo.
- *Fprintf()* scrive su stream
	- restituisce il numero di caratteri scritti; -1 in caso di errore.


#### I/O su Stringhe

```C
int sprintf(char *restrict buffere, const char *restrict format, ...);
int sscanf(const char *str, const char *format, ...)
```

Le funzioni di sopra possono leggere e scrivere dati usando una stringa come se fosse un flusso.
- *sprintf()* scrive caratteri in una stringa. Restituisce il numero di caratteri memorizzati.
- *sscanf()* legge i caratteri da una stringa (puntata dal primo argomento). Restituisce il numero di dati letti e scritti con successo.


#### Funzioni di Input

- Un esempio che usa `fgets` per ottenere una riga dell'input, poi passa la linea alla `sscanf` per ulteriori elaborazioni:

```
fgets(str, sizeof(str), stdin);
	/* legge una riga dell'input */
sscanf(str, "%d%d", &i, &j);
	/*estrae due interi */
```


#### Programmi on più funzioni

- *Strategia big-bang*: integra il programma con tutti i sottoprogrammi e lo verifica nel suo insieme
	- Pessima strategia per programmi grandi: difficile localizzare la funzione contenente il difetto in caso di malfunzionamento ...
- *Strategie incrementali*: testare e integrare un sottoprogramma alla volta, considerando la struttura delle chiamate tra sottoprogrammi (architettura del programma)
	-  Bottom-up
	- Top-down
	- Sandwich
	- ...

#### Strategia bottom-up e driver

Per ogni sottoprogramma da verificare è necessario costruire un programma main (detto **driver**) che:
- acquisire i dati di ingresso necessari al sottoprogramma;
- invoca il sottoprogramma passandogli i dati di ingresso e ottenendo i dati in uscita;
- visualizza i dati di uscita del sottoprogramma.

# #ADT: Abstract Data Types
---
## Tipi di astrazioni

Funzionale/Procedurale:
- FInalità: ampliare l'insieme dei modi di operare sui tipi di dati già disponibili, con la definizione di nuovi operatori
- Una funzionalità di un programma è delegata ad un sottoprogramma, definito ed usabile indipendentemente dall'algoritmo implementante

Dati:
- Finalità: ampliare i tipi di dati disponibili attraverso l'introduzione sia di nuovi tipi di dati che di nuovi operatori, definiti a prescindere dalla loro implementazione.

## Tipi di dati
---
- Un tipo di dati è definito da un dominio di valori e un insieme di operazioni previste su quei valori
- Nel linguaggio C
	- tipi di dato primitivi: forniti direttamente dal linguaggio;
	- dati aggregati;
	- puntatori.

## Tipi di Dati Astratti (ADT)
---
- Tipo di dati che estende dati esistenti, definito distinguendo #Specifica e #Implementazione 
- #Specifica:
	- definizione del tipo di dati;
	- definizione dell'insieme degli operatori
	- #Sintattica: regole (nomi e tipi)
	- #Semantica: significati (valori, vincoli)
- #Implementazione:
	- codifica di quanto definito nella specifica, usando primitive e costrutti di un linguaggio di programmazione
	- è spesso nascosta al programmatore, seguendo il principio dell' #Incapsulamento(information hiding).

### Specifica di un ADT
---

|                                     | Sintattica                                                 | Semantica                                                                                                                                                                             |
| ----------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tipi di dati                        | Nome dell’ADT & Tipi da dati già usati                     | Insieme dei valori                                                                                                                                                                    |
| Operatori:<br>Per ogni<br>operatore | Nome dell’operatore & Tipi di dati di input e di<br>output | Funzione associata<br>all’operatore<br>• Precondizioni: definiscono<br>quando l’oeratore è<br>applicabile<br>• Postcondizioni: definiscono<br>relazioni tra dati di input e<br>output |



## #Implementazione ADT in C: Strutture

---
- Definizione: tipo di dati composito che include un elenco di variabili fisicamente raggruppate in un unico blocco di memoria
- Vantaggio: migliore leggibilità dei programmi

```C
struct point {
float x;
float y;
};

int main (){
struct point p;
p.x = 2.0;
p.y = 3.0;
printf("coordinate del punto: (%.1f, %1.f)", p.x, p.y);
}
```

### Strutture - Inizializzazione
---
- E' possibile inizializzare una struttura direttamente nel momento della sua dichiarazione.
- Si può usare il typedef sulla struttura precedente definita
```C
typedef struct point Punto;
```
- oppure usare in combinazione il typedef e la definizione della struttura
```C
typedef struct point {
float x;
float y;
};

int main (){
point p = {2.0, 3.0};
printf("coordinate del punto: (%.1f, %1.f)", p.x, p.y);
```

## #Implementazione ADT in C: Puntatori
---
- E' possibile allocare memoria per una struttura attraverso le funzioni _malloc_ o _calloc_
```C
point *p = malloc(sizeof(point));
```
- E' possibile accedere ai campi della struttura da un puntatore usando l'operatore freccia ->
```C
int main(){
Point *p = malloc(sizeof(Point));
p->x = 2.0;
p->y = 3.0;
printf("coordinate del punto: (%.1f, %.1f)", p->x, p->y);
}
```


# Pseudo-generics in C
---
- **Definizione**: strumento che permette la definizione di un tipo parametrizzato, esplicitato in fase di compilazione/linkaggio, secondo la necessità.
- Permettono di 
	- eseguire algoritmi su tipi di dati diversi
	- applicare ADT su tipi di dati diversi
- Alcuni linguaggi supportano generics al compile time.

## Obiettivo
---
- Implementare algoritmi e ADT che siano in grado di funzionare, di volta in volta, con il tipo di dati desiderato
- Esempio:
	- Interi: ordinare una sequenza numerica
	- stringe: mettere un elenco di nomi in ordine alfabetico
	- dati strutturati: ordinare i record di studenti secondo la matricola

## Soluzione
---
- Generalizzare il problema dell'ordinamento in modo che possa funzionare con i 3 tipi specificati in precedenza: interi, stringhe e strutture
- Come procedere:
	- creare un tipo generico *Item* (interfaccia) che supporti input, output e confronto
	- modificare le librerie in modo che operino sul tipo Item
	- realizzare Item in 3 file .c che supportano le 3 variabili intero, stringa e struttura
	- linkare ed eseguire separatamente (con make) le 3 varianti

## Supporto del C
---
- Il C mette a disposizione un elemento semplice per poter creare il tipo generico *Item*: il puntatore void*
```C
	void * p_void; 
```
- E' possibile dichiararlo nella maniera sopra riportata, per poi assegnarlo al tipo desiderato:
```C
	int* p_int = p_void;
	char* p:char = p_void;
	struct studente{
		char nome[20];
		int matricola;
	};
	typedef struct studente *Studente;
	Studente p_studente = p_void;
```

# ADT #LISTA
---
## Il tipo astratto *Lista*
- Definizione: sequenza di elementi di un determinato tipo, in cui è possibile aggiungere o togliere elementi
	- è possibile specificare la *posizione* relativa nella quale l'elemento va aggiunto o tolto

## Funzioni delle Liste
---
|Sintattica|Semantica|
|:--:|:--:|
|Nome tipo: List  Tipi usati: Item, boolean|Dominio: insieme di sequenze L=a1,....,an di tipo Item. L'elemento nil rappresenta la lista vuota|
|newList() -> List|newList()-> nil   -Post: l= nil|
|isEmpty(List)-> boolean|isEmpty(I)-> b -Post: se l = nil allora b = true altrimenti b = false|
|addHead(List, Item) -> List|addHead(l, e)-> I' -Post: l =<a1,a2,...an> AND l' = <e,a1,...,an>|
|removeHead(List) -> List| removeHead(l)->l' -Pre: l = <a1,a2,..,an> n>0  -Post:l' = <a2,a3,..,an|
|getFirst(List) -> Item|getHead(I) -> e  -Pre: l=<a1,a2,..,an> n>0   -Post: e=a1|
|insertItem(List, Item, int) -> List|insertItem(l, e, pos) -> l'   -Pre: l = <a1,...,a<sub>n+1</sub>> & 1<= pos<= n+1    -Post: l = <a1,..,a<sub>pos</sub>,..,a<sub>n+1</sub>> & a<sub>pos</sub> = e|
|insertTail(List, Item) -> List|insertTail(l, e) -> l'  -Post: l=<a1,...,an> & l' = <a1,....,an,e>|
|reverseList(List, Item) -> List|reverseList(l) -> l'    -Post: l=<a1,a2,...,an> AND l'=<an,...,a2,a1>|
|cloneList(List) -> List|cloneList(l) -> l'   -Post: l=<a1,a2,...,an> AND l'=<a1,a2,...,an>|


## Progettazione: Liste Concatenate
---
- Ogni elemento di una lista concatenata è un record con un campo puntatore che serve da collegamento pr il successivo.
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
		- le liste, una volta create, sono totalmente indipendenti

# ADT #STACK 
---
- Una ***pila*** è una sequenza di elementi di un determinato tipo, in cui è possibile aggiungere o togliere elementi esclusivamente da un unico lato (***top*** dello stack).
	- la pila è una struttura dati *lineare* a *dimensione variabile* in cui si può accedere direttamente solo al ***primo*** elemento della lista
	- non è possibile accedere ad un elemento diverso dal primo **se non dopo** aver eliminato tutti gli elementi che lo precedono (inseriti dopo)
	- lista gestita con la modalità ***LIFO (Last-In-First-Out)*** cioè l'ultimo elemento inserito nella sequenza sarà il primo ad essere eliminato

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
	- quando lo stack si riempie, non è possibile eseguire l'operazione push ...

### Implementazione con Lista
---
- Il tipo stack è definito come un puntatore ad una struct che contiene
	- un elemento **items** di tipo **list**
	- non serve più **MAXSTACK** 
	- anche se abbiamo un solo elemento nella struct, continuiamo a definire il tipo stack come puntatore a **struct stack** per non cambiare la definizione nell'header file




# ADT #QUEUE
---
- Una ***queue***(***coda***) è una sequenza di elementi di un determinato tipo, in cui gli elementi si aggiungono da un lato (***tail***) e si tolgono dall'altro (***head***)
- la sequenza viene gestita con la modalità ***FIFO (First-In-First-Out)***: il primo elemento inserito nella sequenza sarà il primo ad essere eliminato
- la coda è una struttura dati *lineare* a *dimensione variabile*
	- si può accedere direttamente solo alla testa (**head**) della lista
	- non è possibile accedere ad un elemento diverso da **head**, se non dopo aver eliminato tutti gli elementi che lo precedono (cioè quelli inseriti prima).

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
- Se l'array viene gestito normalmente, cioè mantenendo head<=tail, ci sono dei problemi...
- se rimuoviamo uno alla volta i primi tre elementi in coda, otteniamo un array in cui risultano disponibili solo le posizioni a destra di tail, ma sono libere anche quelle a sinistra di head

### Soluzioni
---
- **Prima soluzione**: ad ogni rimozione si compatta l'array nelle posizioni iniziali, con uno shift degli elementi
	- TROPPO COSTOSO!
- **Seconda soluzione**: si gestisce l'array in modo circolare
	- in ogni istante, gli elementi della coda si trovano nel segmento head, head+1,..., tail-1, ma non neessariamente head<=tail
	- infatti, dopo aver inserito in posizione N-1, se c'è ancora spazio in coda, si inseriscono ulteriori elementi a partire dalla posizione 0
	- in questo modo si riesce a garantire che ad ogni istante la coda abbia capacità massima di N-1 elementi


# #Ricorsione
---

## #RDA: Record Di Attivazione
---
Ogni volta che viene invocata una funzione, viene creata dinamicamente una struttura dati detta RECORD DI ATTIVAZIONE
- si crea di una nuova istanza della funzione chiamata
- viene allocata la memoria per i parametri e per le variabili locali
- si effettua il passaggio dei parametri
- si trasferisce il controllo alla funzione chiamata
- si esegue il codice della funzione

L' #RDA contiene:
- i parametri formali
- le variabili locali
- l'indirizzo di ritorno (RA) che indica il punto a cui tornare al termine della funzione
- un collegamento al record di attivazione del chiamante (Link Dinamico DL)
- l'indirizzo del codice della funzione 

L' #RDA associato a una chiamata di una funzione f:
	1. è creato al momento della invocazione di f
	2. permane per tutta la durata d'esecuzione di f
	3. è distrutto (deallocato) al termine dell'esecuzione
La dimensione dell' #RDA 
	1. varia da una funzione all'altra
	2. per una data funzione, è fissa e calcolabile a priori

## #Stack
---
L'area di memoria in cui vengono allocati i record di attivazione viene gestita come una lista LIFO
- nella quale ogni elemento è un #RDA 
La gestione dello #Stack avviene mediante due operazioni:
1. #push: aggiunta di un elemento in cima alla pila
2. #pop: prelievo di un elemento dalla cima della pila

L'ordine di collocazione degli RDA nello Stack indica la cronologia delle chiamate

## Programmazione Ricorsiva
---
Un sottoprogramma ricorsivo è:
- un sottoprogramma che richiama *direttamente* o *indirettamente* se stesso

I linguaggi che gestiscono la ricorsione, lo fanno mediante gli #RDA 
Operativamente, risolvere un problema con un approccio ricorsivo comporta:
	1. identificare un "caso base". con soluzione nota
	2. esprimere la soluzione al caso generico *n* in termini dello *stesso problema in uno o più casi più semplici* (n-1, n-2, etc.)

## Funzioni Matematiche Ricorsive
---
Una funzione matematica è definita ***ricorsivamente*** quando nella sua definizione compare un riferimento a se stessa
E' basata sul *principio di induzione* matematica:
	- se una proprietà P vale per n=n<sub>0</sub> (**CASO BASE**)
	- e si può provare che, ***assumendola valida per n***, allora vale per n+1
	- allora P vale per ogni n>= n<sub>0</sub>

Esempio di funzione matematica ricorsiva è il fattoriale.
La funzione fattoriale(n), denotato come n!, è definito per tutti gli interi n<=0 come:
- n! = 1                  se n = 0
- n! = n * (n-1)!     se n < 0


```C
int fact(int n)
{
	if (n==0) return 1;
	else return n*fact(n-1);
}

main() {
	int fz, z = 5;
	fz = fact (z - 2);
}
```


# Complessità computazionale
---
- **Analisi della complessità**: stima del costo degli algoritmi in termini di risorse di calcolo (tempo, spazio di memoria)
- esempio: dato un vettore v di n interi ordinati in maniera decrescente, verificare se un intero k è presente o meno in v
```C
int ricerca (int v[], int size, int k){
	int i;
	for(i=0; i<size; i++)
		if (v[i] == k) return i;
	return -1;
}
```


## Valutazione del tempo di esecuzione
---
- Variabili che influenzano il tempo di esecuzione:
	- la macchina utilizzata
	- la dimensione dei dati
	- la configurazione dei dati
- Modello astratto per la valutazione del tempo
	- indipendente dalla macchina usata
	- stima in funzione della dimensione dell'input 
	- comportamento asintotico
	- stima del caso peggiore di configurazione dei dati

## Esempio di macchina astratta
---
- Istruzioni e condizioni atomiche hanno costo unitario
- Le strutture di controllo hanno un costo pari alla somma dei costi dell'esecuzione delle istruzioni interne, più la somma dei costi delle condizioni
- Le chiamate a funzione
	- hanno un costo pari al costo di tutte le sue istruzioni e condizioni;
	- il passaggio dei parametri ha costo nullo
- Istruzioni e condizioni con chiamate a funzioni hanno costo pari alla somma del costo delle funzioni invocate più uno

## Caso peggiore
---
- Caso che, a parità di dimensione, produce il costo massimo
	- se accettabile nel caso peggiore...
- Nel caso della ricerca, k non presente nel vettore

**Totale: 3n + 3**

## Caso medio
---
- Supponiamo che il numero cercato sia presente e che ci sia equiprobabilità dell'input
	- la probabilità che k sia in posizione i (1<=i<=n)v vale 1/n
	- costo del caso in posizione i: 3i +1
	- costo caso medio: **(3n + 5)/2**

## Costo come funzione della dimensione dell'input
---
- Cos'è la dimensione?
	- vettore ... numero di elementi
	- albero ? ... numero dei nodi
	- grafo ? ... numero archi più numero nodi
- esempio: calcolo del fattoriale, con tipo intero non limitato
```C
int fattoriale(int n)
{
	int i=1;
	int fatt=!;
	while (i <= n){
		fatt *= fatt;
		i++:
	}
	return fatt;
}
```
**Totale: 3n +4**

## Dimensione dell'input
---
- Parametro n
	- Costo = 3n +4 (lineare)
- Numero d di bit necessari per rappresentare n:
	- d = log<sub>2</sub> n
	- costo = 3 x 2<sup>d</sup> + 4 (esponenziale)

- Nell'analizzare la complessità di tempo di un algoritmo siamo interessati a come aumenta il tempo al crescere della taglia *n* dell'input
- Siccome per valori "piccoli" di *n* il tempo richiesto è comunque poco, ci interessa soprattutto il comportamento per valori "grandi" di n (il **comportamento asintotico**)

## Comportamento asintotico
---
- Comportamento al crescere della dimensione n dei dati all'infinito
	- trascurare tutte le costanti moltiplicative ad additive e tutti i termini di ordine inferiore
	- suddivisione di algoritmi in classi di complessità
		- a costante
		- an + n  lineare 
		- an<sup>2</sup> + bn + c   quadratica
		- alog<sub>g</sub> (n) + h   logaritmica
		- a<sup>n</sup>   esponenziale
		- n<sup>n</sup>   esponenziale

## Notazione O ed Omega
---
- f e g funzioni dai naturali ai reali positivi
- f(n) è O di g(n), f(n) appartiene a O(g(n)), se esistono due costanti positive c ed n<sub>0</sub>  tali che :
	- **se n >= n<sub>0</sub>, f(n) <= cg(n)**
		- applicata alla funzione di complessità f(n), la notazione O ne limita superiormente la crescita e fornisce quindi una indicazione della bontà dell'algoritmo
- f(n) è Omega di g(n), f(n) appartiene ad Omega(g(n)), se esistono due costanti positive c ed  n<sub>0</sub>  tali che:
	- **se n >= n<sub>0</sub>, f(n) >= cg(n)
		- la notazione Omega limita inferiormente la complessità, indicando così che il comportamento dell'algoritmo non è migliore di un comportamento assegnato

## Complessità dei Problemi
---
- Studiare la complessità di un problema (ossia quello che un algoritmo risolve) è molto diverso dallo studiare la complessità di un algoritmo
	- per poter dire che un problema ha complessità O(g(n))  (immaginiamo di parlare del caso peggiore) basta trovare un qualsiasi algoritmo che lo risolva con O(g(n))
	- per poter affermare che un problema è Omega(g(n)) occorre invece dimostrare matematicamente che tutti i possibili algoritmi (inventati o non) lo risolvano alla meglio come Omega(g(n))
- Per limitare superiormente un problema basta trovare almeno un algoritmo con complessità O(g(n))
- Per limitare inferiormente un problema bisogna studiare ogni possibile soluzione (il problema, in linea teorica, potrebbe essere risolto in tempo costante, ma si può sempre dimostrare il contrario)
	- quando la complessità di un algoritmo è pari al limite inferiore di complessità determinato per un problema, l'algoritmo si dice ottimo (in ordine di grandezza)

## Individuazione di limiti inferiori
---
- ***DImensione n dei dati***: se nel caso peggiore occorre analizzare tutti i dati, allora Omega(n) è un limite inferiore alla complessità del problema
	- esempio: ricerca di un elemento o del massimo in un array
	- è una tecnica banale, la maggior parte dei problemi hanno limiti inferiori più alti
- ***Eventi contabili***: la ripetizione di un evento un dato numero di volte è essenziale per la risoluzione di un problema
	- esempio: generare tutte le permutazioni di n oggetti
	- l'evento è la generazione di una nuova permutazione che si ripete per tutte le permutazioni, ossia n! volte.

## Regole di valutazione della complessità (1)
---
- Scomposizione
	- alg è la sequenza di alg1 ed alg2
	- alg1 è O(g1(n)); alg2 è O(g2(n))
	- alg è O(max(g1(n), g2(n)))
- Esempio
```C
i=0;
//g1(n)
while (i<n)
{
	Stampastelle(i);
	i+=1;
}

//g2(n)
for(i=0; i<2*n; i++)
	scanf("%d", &numero);
```

- Blocchi annidati
	- alg è composto da due blocchi annidati
	- Blocco esterno è O(g1(n)); blocco interno è O(g2(n))
	- alg è =(g1(n) per g2(n))
- Esempio
```C
for(i=0; i<n; i++)
{
	scanf("%d", &j);
	printf("%d", j*j);
	do
	{
		scanf("%d", &numero);
		j+=1;
	}while (j<=n);
}
```

## Regole per la valutazione della complessità (2)
---
- Sottoprogrammi ripetuti
	- alg applica ripetutamente un certo insieme di istruzioni la cui complessità all'i-esima esecuzione vale f<sub>i</sub>(n); il numero di ripetizioni è g(n)
	- alg è O(Sum (i=1 -> g(n) (f<sub>i</sub>(n))))
	- per f<sub>i</sub>(n) tutte uguali ... O(g(n) f(n))


- Operazione dominante
	- sia f(n) il costo di esecuzione di un algoritmo alg
	- un'istruzione i è dominante se viene eseguita g(n) volte, con f(n) <= a g(n)
	- se un algoritmo ha una operazione dominante allora è O(g(n))

## Ricerca Binaria
---
```C
int ricercaBin(int v[], int size, int k)
{
	int inf=0, sup = size -1;
	while (sup>=inf)
	{
		int med = (sup + inf)/2;
		if (k==v[med])
			return med;
		else if(k>v[med])
			inf = med+1;
		else 
			sup = med-1;
	}
	return -1;
}
```

- Osserviamo che la dimensione del problema dimezza ad ogni ciclo
	- inizialmente è n, quindi n/2, poi n/4, e così via
- Il ciclo si arresta quando la dimensione del prolema è 1, dopo circa log<sub>2</sub> n iterazioni
- Eseguiamo un numero costante di confronti per ogni iterazione. Il numero massimo di confronti sarà:
***f(n) = O(log n)***

# ADT #Albero_Binario
---
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



# ADT #Alberi_binari_di_ricerca
---
## Definizione:
---
- Se l'albero non è vuoto:
	- ogni elemento del sottoalbero di sinistra precede (<) la radice
	- ogni elemento del sottoalbero di destra succede (>) la radice
Per ogni sottoalbero scelto, le proprietà precedenti si propagano.

## Operazioni
---
### Search
---
- se l'albero è vuoto, allora restituisce null
- se l'elemento cercato coincide con la radice dell'albero restituisce l'item della radice
- se l'elemento cercato è minore della radice, restituisce il risultato della ricerca dell'elemento nel sottoalbero sinistro
- se l'elemento cercato è maggiore della radice, restituisce il risultato della ricerca dell'elemento nel sottoalbero destro

### Min (Max)
---
- Algoritmo ricorsivo:
	- se l'albero è vuoto, allora restituisci null
	- se non esiste un sottoalbero sinistro (destro), ritorna l'item associato alla radice
	- se esiste un sottoalbero sinistro (destro), effettua la ricerca del minimo (massimo) nel sottoalbero sinistro (destro)

### Insert
---
- Inserimento di un elemento
	- se l'albero è vuoto, crea un nuovo albero con un solo elemento
	- se l'albero non è vuoto
		- se l'elemento coincide con la radice, non si fa nulla
		- se l'elemento è minore della radice, lo inserisce nel sottoalbero sinistro
		- se l'elemento è maggiore della radice, lo inserisce nel sottoalbero destro
