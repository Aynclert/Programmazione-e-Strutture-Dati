
## Tipi di astrazioni

Funzionale/Procedurale:
- Finalità: ampliare l'insieme dei modi di operare sui tipi di dati già disponibili, con la definizione di nuovi operatori
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

|                                    | Sintattica                                             | Semantica                                                         |
| ---------------------------------- | ------------------------------------------------------ | ----------------------------------------------------------------- |
| **Tipi di dati**                   | - Nome dell'ADT e Tipi di dati già usati               | - Insieme dei valori                                              |
| **Operatori** : per ogni operatore | - Nome dell'operatore e Tipi di dati di input e output | Funzione associata all'operatore: - Precondizioni -Postcondizioni |

Le precondizioni definiscono quando l'operatore è applicabile;
Le postcondizioni definiscono relazioni tra dati di input e output.


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

