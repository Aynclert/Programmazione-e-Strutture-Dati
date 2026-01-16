
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
