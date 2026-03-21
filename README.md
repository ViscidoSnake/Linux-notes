# Scopo del progetto
Vorrei aumentare le mie conoscenze riguardo il sistema Linux, per fare ciò non ho in mente un percorso di apprendimento ben strutturato e il presente documento serve per raccogliere e organizzare tutti i vari concetti progressivamente appresi seguendo varie fonti. Come punto di riferimento viene usato il materiale fornito da [LPI](https://learning.lpi.org/it/) (Linux Professional Institute), in particolare, per iniziare, la risorsa **Linux Essentials** il cui pdf si trova nella cartella `resources` con il nome di `LPI-Learning-Material-010-160-it.pdf`.

# Note pratiche sulla stesura del documento
Il presente template è stato realizzato da Daan Zwaneveld ed è sotto licenza [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/), la presente versione è stata modificata in alcune parti e quella originale è reperibile al seguente [link](https://github.com/dzwaneveld/TU-Delft-Unofficial-Report-Template). Aprendo la cartella `DocLatex` è possibile vedere l'organizzazione del template, rimandando alla documentazione ufficiale scritta dall'autore del template originale (sempre reperibile al link riportato sopra), qui riporto solo la modalità con cui è possibile espandere il contenuto del documento; Ogni capitolo del documento possiede un file `.tex` nella directory `mainmatter`, dentro tale file deve essere sempre presente un intestazione del tipo:
```
\chapter{<nome del capitolo>}
\label{chapter: <etichetta>}
```
e a seguire il contenuto va organizzato in sezioni (comando *\section*), sottosezioni (comando *\subsection*) e sotto-sottosezioni (comando *\subsubsection*) tutte da corredare con etichetta (come mostrato sopra per il capitolo ma ovviamente con prefisso differente, quindi per una sezione sarà una cosa del tipo *\label{sec: < etichetta >}*); Per richiamare le sezioni, sottosezioni e capitoli nel documento si usa il classico comando **\ref{< prefisso >:< etichetta >}**.

Per includere il nuovo file `.tex` nella compilazione è necessario scrivere nel file *main-Linux-notes.tex*, sotto la sezione *mainmatter*, una stringa del tipo `\input{mainmatter/<file>}` dove *file* sarebbe il nome del nuovo file da compilare privato del *.tex*, l'ordine con cui gli input vengono scritti determina l'ordine con cui i capitoli (e quindi i contenuti) si presentano nel documento `.pdf` finale.

In fine, se nel documento vengono trattati aspetti che non sono riportati nelle risorse di riferimento (contenute nella cartella `resouces`), è possibile lasciare un riferimento nel documento usando il comando **\cite{< nome risorsa >}** il quale riporta la fonte dichiarata nel file `.bib`.

## Tipologia di contenuti e modalità di inserimento nel documento
I contenuti organizzati in capitoli e sezioni possono essere di vario tipo: testo, immagine, tabella e listato, per ciascuna di queste categorie sono previsti comandi appositi da utilizzare.


### Testo semplice
sono previsti 4 stili diversi:
- **\tb{ < testo > }**: testo in grasseto, usato per evidenziare concetti importanti.
- **\ti{ < testo > }**: testo in corsivo, usato per termini specifici o tecnici non direttamente collegati al contenuto principale della frase.
- **\tc{ < testo > }**: testo typewriter, uato per evidenziare comandi ed eventuali opzioni e argomenti che lo seguono, anche per riportare nomi di file o percorsi.
- **\sh{ < testo > }**: crea un rettangolo con sfondo grigio e applica font family typewriter al testo, usato per evidenziare comandi completi scritti inline nel testo.


### Listato
Ambiente custom con sfondo grigio e testo typewriter, bold per i caratteri che seguono il simbolo "$", Usato per riportare nel documento esempi con stile cmd Linux; 2 stili diversi, uno permette indicizzazione del listato nell'indice mentre l'altro no.
- **\begin{cmdc} { < descrizione > } { < etichetta > } < testo > \end{cmdc}**: permette indicizzazione, tutti gli argomenti sono obbligatori:
	- < descrizione > e < etichetta > rispettivamente le classiche *caption* e *label* usate nell'ambiente *lst* per definire *caption* e *label* del listato.
	- < testo > contenuto effettivo, **molto importante**: Il testo scritto nel blocco va indentato con 1 tab oppure 4 spazzi, se lo stesso blocco subisce indentazione (caso tipico all'interno di ambienti come *itemize*) allora in testo non va indentato ulteriormente. Per disabilitare completamente l'indentazione, nel file `.cls`, in *\lstdefinestyle{cmds}*, decommentare *,gobble=4*.
	
	**Note**:
	- L'ambiente non è *floating*, appare nel PDF esattamente nel punto in cui viene scritto nel file `.tex`.
	- Il riferimento si effetua con il comando **\ref{lst:< etichetta >}**.

	Esempio di utilizzo:
	```
	\begin{cmdc}{Esempio 1 comandi}
		$ cat file
		hello world
		$ ls fileX*
		fileX100
	\end{cmdc}
	Facendo riferimento a \ref{lst:Esempio_1_comandi}
	```

- **\begin{cmd} { < testo > } \end{cmd}**: Identico all'ambiente *cmdc* desctitto sopra, l'unica differenza è che questo non supporta descrizione ed etichetta e per questo non compare nell'indice dei listati. Viene usato per riportare in stile cmd Linux passaggi intermedi di particolari procedure o comunque listati non particolarmente importanti nella spiegazione.

	**Note**:
	- L'ambiente non è *floating*, appare nel PDF esattamente nel punto in cui viene scritto nel file `.tex`.

	Esempio di utilizzo:
	```
	\begin{cmd}
		$ cd ./web/index.html
	\end{cmd}
	```


### Immagini
Sono previsti due comandi (in raltà è un comando e un ambiente), uno permette di inserire generiche immagini che si trovano nella cartella `figures` del template mentre l'altro è specifico per l'inserimento nel documento di struttuture realizzate attraverso il pacchetto *dirtree*.
- **\fig[ < size > ]{ < nome file > }{ < descrizione > }{ < etichetta > }**: per inserire immagini nel documento, gli argomenti tra parentesi quadre sono opzionali mentre gli altri sono obbligatori:
	- < size > permette di effettuare un ridimensionamento dell'immagine in relazione allo spazio (larghezza) occupato dal testo, il valore di dafault è 0.95.
	- < nome file > specifica il nome del file immagine da inserire, è necessario che il file si trovi nella directory `figures` del template.
	- < descrizione > e < etichetta >, rispettivamente le classiche *caption* e *label* usate nell'ambiente *figure* per aggiungere descrizione ed etichetta.

	**Note**:
	- L'ambiente è *floating*.
	- Per fare riferimento all'immagine si utilizza il comando **\ref{fig: < etichetta >}**. 
	
	Esempio di utilizzo:
	```
	\fig[0.8]{FHS.png}{FHS}{schema-FHS}
	Facendo riferimento a \ref{fig:schema-FHS}
	```
- **\begin{figtree}[ < altezza > ][ < larghezza > ]{ < descrizione > }{ < etichetta > }{ < ambiente \dirtree > }\end{figtree}**: ambiente usato per riportare nel documento le strutture di sistemi in termini di directory e file, viene usato il pacchetto *dirtree* per il disegno dell'albero e un ambiente *figure* per gestire la posizione e il richiamo. Gli argomenti tra parentesi quadre sono opzionali mentre gli altri sono obbligatori:
	- < altezza >, espresso in *pt*, regola lo spazio verticale tra i rami, il valore di default è *13pt*.
	- < larghezza >, espressa in *em*, regola la lunghezza orizzontale dei rami, il valore di default è *6em*.
	- < descrizione > e < etichetta >, rispettivamente le classiche *caption* e *label* usate nell'ambiente *figure* per aggiungere descrizione ed etichetta.
	- < ambiente \dirtree > classica sintatti prevista dal pacchetto *dirtree* per il disegno dell'albero.

	**Note**:
	- L'ambiente è *floating*.
	- Nel documento `.pdf` il risultato è una figura che segue la numerazione classica prevista (per le entità figure) pertanto il riferimento a questa aviene direttamente usando il seguente comando **\ref{fig: < etichetta >}**.
	
	Esempio di utilizzo:
	```
	\begin{figtree}{Struttura interna della directory \tc{user}}{Struttura-interna-della-directory-user}
		\dirtree{%
			.1 user.
			.2 documenti.
			.3 fileZ1.
			.2 musica.
			.3 fileA1.
			.3 fileA2.
			.3 fileA3.
			.3 nuovi.
			.4 fileB1.
			.4 fileB2.
			.3 preferiti.
			.4 fileC1.
			.4 fileC2.
			.2 scuola.
		}
	\end{figtree}
	Facendo riferimento a \ref{fig:Struttura-interna-della-directory-user}
	```


### Tabelle
Un solo ambiente custom che permette una certa flessibilità nella scrittura della tabella e permette di avere uno stile abbastanza uniforme.
- **\begin{tbl}{ < pattern > }{ < descrizione > }{ < etichetta > }{ < tabella > }\end{tbl}**: tutti gli argomenti sono necessari,
	- < pattern > dichiara la struttura della tabella realizzata nell'ambiente *tabular*, si utilizza la sintassi standard del pacchetto quindi ad esempio *ccc* sarebbero tre colonne dove in ciascuna il testo si dispone al centro.
	- < descrizione > e < etichetta >, rispettivamente le classiche *caption* e *label* usate nell'ambiente *table* per aggiungere descrizione ed etichetta.
	- < tabella > contiene il codice effettivo che definisce la tabella, si usano le regole classiche di costruzione, importante ricordare di inserire *\midrule* tra l'intestazione e il resto della tabella.

	**Note**:
	- L'ambiente è *floating*.
	- Il riferimeto alla tabella si effetua con il comando **\ref{tab: < etichetta >}**.
	
	Esempio di utilizzo:
	```
	\begin{tbl}{lccc}{esempio numero 1}{esempio-numero-1}
		\textbf{Type} & $\mathbf{N_C}$ & \textbf{$\mathbf{F_S}$  (Hz)} & \textbf{$\mathbf{N_B}$  (Bits)} \\
		\midrule
		EMG & 1 & 3200 & 24 \\
		EMG & 2 & 1600 & 24  \\
		EMG & 3 & 800 & 24 \\
		EMG & 3 & 200 & 24 \\
		ACC & 3 & 104 & 16 \\
		ACC + GYRO & 6 & 104 & 16 \\
		ACC + GYRO & 6 & 208 & 16 \\
		ACC + GYRO & 6 & 416 & 16 \\
	\end{tbl}
	Facendo riferimento a \ref{tab:esempio-numero-1}
	```
