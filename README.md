# hd4me-cli

Questo breve programma in python 3 (è stato creato con python 3.9 ma dovrebbe funzionare con qualsiasi versione di python superiore a 3.6) permette di cercare, ottenere informazioni e mettere in coda per il download i file presenti su hd4me.

Senza alcun argomento, il programma si limita ad elencare tutti i film presenti sul sito.

La ricerca può essere effettuata con lo switch `-s/--search`, ad esempio per cercare i film su "007":

```
hd4me-cli -s "007"
```

E' possibile usare lo switch `-y/--anno-release` per restringere la ricerca ai film prodotti in quell'anno:

```
hd4me-cli -s "007" -y 1965
```

I risultati della ricerca possono essere ordinati per anno o per IMdb rating:

```
hd4me-cli -s "007" --rating
hd4me-cli -s "007" --data
```

Di default, le informazioni presentate sono solo il titolo da hd4me, il titolo originale da IMdb, anno e rating.
Per ottenere maggiori dettagli, come genere e data completa di rilascio, usare `--info`.

```
hd4me-cli -s "007" -y 1965 --info
```

Impostando lo switch `-d / --download` si aggiungerà il file alla coda di `mega-get`, ovviamente la cli di mega deve essere installata per funzionare.
Di default il file viene scaricato nella diractory corrente, per impostare la destinazione usare `-p/--path`:

```
hd4me-cli -s "007" -y 1965 -dp /directory/di/destinazione`
```

**Importante**:

Lo script funziona in modo molto semplice e, per il momento, in serie. Questo significa che ad ogni ricerca lo script andrà a prelevare le informazioni IMdb per ogni file, uno alla volta, il che richiede un tempo anche piuttosto lungo.

Per fare un esempio, la ricerca di "007", che al momento restituisce 13 file, richiede circa 20 secondo per poter essere completata. 

Un file specifico invece, per esempio la ricerca di "beetlejuice" ne richiede circa 4.

Fra i prossimi aggiornamenti vorrei implementare python threads per eseguire le ricerche in modo parallelo, rendendo le ricerche notevolmente più rapide (e il programma più pesante sulla CPU, leggero e veloce non vanno d'accordo..).

