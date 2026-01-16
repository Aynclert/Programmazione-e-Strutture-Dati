
- #Testing : esercitare il programma con dati di test per verificare che il suo comportamento sia conforme a quello atteso:
	- Oracolo: output atteso;
	- Malfunzionamento: output differente da quello atteso.

Obiettivo del #Testing è l'individuazione dei vari malfunzionamenti, causati da errori o bug nel codice.

#Debugging : individuazione e correzione del difetto che ha causato il malfunzionamento.

Più è alta la fase in cui si introduce il difetto, maggiore è la difficoltà nel rimuoverlo. La sua ricerca può essere fatta inserendo nel source code dei punti di ispezione dello stato delle variabili.

#### Classi di dati

Testare il programma con tutti i possibili dati di test è impraticabile...

#Obiettivo: individuare classi di dati di test, selezionare un caso di test da ogni classe ed evitare casi di test ridondanti.

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
