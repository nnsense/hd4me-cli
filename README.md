# hd4me-cli

Questo breve programma in python (è stato creato con python 3.9 ma dovrebbe funzionare con qualsiasi versione di python superiore alla 3.6) permette di cercare, ottenere informazioni e mettere in coda per il download i file presenti su hd4me.

Senza alcun argomento, il programma si limita ad elencare tutti i film presenti sul sito. Data la quantità (quasi 8000 al momento), è meglio restringere la ricerca.

La ricerca può essere effettuata con lo switch `-s/--search`, ad esempio per cercare i film su "007":

```
hd4me-cli -s "007"
```

E' possibile usare lo switch `-y/--anno-release` per restringere la ricerca ai soli film prodotti in quell'anno:

```
hd4me-cli -s "007" -y 1965
```

I risultati della ricerca possono essere ordinati per anno o per IMdb rating:

```
hd4me-cli -s "007" --rating
hd4me-cli -s "007" --data
```

Di default, le informazioni presentate sono solo il titolo da hd4me, il titolo originale da IMdb, anno e rating, per esempioç

```
hd4me-cli -s "007" -y 1965
Agente 007 – Thunderball: operazione tuono - (Thunderball, 1965 - rating: 6.9)
```

Per ottenere maggiori dettagli, come genere e trama (in inglese), usare `--info`.

```
hd4me-cli -s "007" -y 1965 --info
Thunderball (Data: 1965-12-30, Rating: 6.9)
Download: https://mega.nz/#!8hdF3Apa!bkpOyim50t8ArG4GhsgWLFVdM2ZJFx_KFOCNA11WSgQ
Genere: Action, Adventure, Thriller
Trama:James Bond heads to the Bahamas to recover two nuclear warheads stolen by S.P.E.C.T.R.E. Agent Emilio Largo in an international extortion scheme.
```

Impostando lo switch `-d / --download` si aggiungerà il file alla coda di `mega-get`, ovviamente la CLI di mega deve essere stata preventivamente installata.

Di default il file viene scaricato nella diractory corrente, per impostare la destinazione usare `-p/--path`:

```
hd4me-cli -s "007" -y 1965 -dp /directory/di/destinazione`
```

Infine, per i maniaci delle informazioni, è possibile scaricare il file con tutte le informazioni sul video da hd4me con `-m / --mediainfo`:

```
hd4me-cli -s "007" -y 1965 --mediainfo
```

**Importante**:

Lo script funziona in modo molto semplice e, per il momento, in modo "seriale".

Questo significa che ad ogni ricerca lo script andrà a prelevare le informazioni IMdb *per ogni file*, uno alla volta, il che richiede un tempo che può essere anche piuttosto lungo.

Per fare un esempio, la ricerca di "007", che al momento restituisce 13 file, richiede circa 20 secondi per essere completata. 

Un file specifico invece, per esempio la ricerca di "beetlejuice" ne richiede circa 4.

Fra i prossimi aggiornamenti vorrei implementare python threads per eseguire le ricerche in modo parallelo, sveltendo notevolmente la ricerca (e rendendo il programma più pesante sulla CPU, purtroppo leggero e veloce non vanno d'accordo..).

