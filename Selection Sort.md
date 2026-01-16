
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

