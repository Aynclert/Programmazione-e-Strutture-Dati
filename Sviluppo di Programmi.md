
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

