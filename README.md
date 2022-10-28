# hd4me-cli

```
usage: hd4me-cli [-h] [-l] [--min-year MIN_YEAR] [--max-year MAX_YEAR] [--min-rating MIN_RATING] [-r] [-y] [-d] [-p PATH] [-i] [--backup] movie_title

positional arguments:
  movie_title           Cerca una stringa specifica nel titolo, per elencare tutti i film usare "" (vuoto)

optional arguments:
  -h, --help            show this help message and exit
  -l, --list            Elenca semplicemente i film trovati dalla ricerca (senza ulteriori dati, per velocizzare la ricerca, non sarà possibile usare --min-year, --max-year e --min-rating)
  --min-year MIN_YEAR   Imposta l'anno minimo dei film da elencare
  --max-year MAX_YEAR   Imposta l'anno minimo dei film da elencare (oggi, se assente)
  --min-rating MIN_RATING
                        Imposta il rating minimo dei film da elencare
  -r, --rating          Ordina i film per IMdb rating
  -y, --year            Ordina i film per anno di rilascio
  -d, --download        Aggiungi il link mega alla coda download (richiede mega-cli installato)
  -p PATH, --path PATH  Imposta un percorso per il download, se assente scarica nella directory corrente
  -i, --info            Visualizza tutti i dettagli del film da IMdb
  --backup              Crea una cartella 'backup' ed esporta tutti i dati sui film di hd4me e relativi file data in quella cartella
```

Questo breve programma in python (è stato creato con python 3.9 ma dovrebbe funzionare con qualsiasi versione di python superiore alla 3.6) permette di cercare, ottenere informazioni e mettere in coda per il download i film presenti su hd4me.

Richiede, come minimo, parte del nome del film da cercare, ad esempio per cercare i film su "007":

```
> hd4me-cli "007"
```

E' possibile usare gli switch `--min-year / --max-year` e `--min-rating` per effettuare la ricerca dei soli film prodotti successivamente o precedentemente un dato anno o con un rating IMDB maggiore di un certo valore. I due argomenti posso essere usati contemporaneamente per restringere ulteriormente la ricerca:

```
> hd4me-cli "007" --min-year 1965
oppure
> hd4me-cli "007" --min-rating 7
oppure
> hd4me-cli "007" --min-year 1965 --min-rating 7
oppure
> hd4me-cli "007" --min-year 1965 --max-year 1980 --min-rating 7
```

I risultati della ricerca possono essere eventualmente ordinati per anno o per IMdb rating:

```
> hd4me-cli "007" --rating
oppure
> hd4me-cli "007" --year
```

Di default, le informazioni presentate sono solo il titolo da hd4me, il titolo originale da IMdb, data di rilascio e rating, per esempio:

```
> hd4me-cli "007" --min-year 1989
007 – Vendetta privata - (Licence to Kill, 1989-07-14 - rating: 6.6)
```

Per ottenere maggiori dettagli, come genere e trama (in inglese), usare `--info`.

```
> hd4me-cli "007" --min-year 1989 --info
Licence to Kill (Data rilascio: 1989-07-14, IMDB Rating: 6.6)
Download link: https://[redacted]
Genere: Action, Adventure, Thriller
Trama: A vengeful James Bond goes rogue to infiltrate and take down the organization of a drug lord who has murdered his friend&apos;s new wife and left him near death.
```

Impostando lo switch `-d / --download` si aggiungerà il file alla coda di `mega-get`, ovviamente la CLI di mega deve essere stata preventivamente installata.

Di default il file viene scaricato nella directory corrente, per impostare la destinazione usare `-p/--path`:

```
> hd4me-cli "007" --min-year 1989 -dp /directory/di/destinazione`
```

Infine, è possibile scaricare una sorta di backup in una cartella (creata automaticamente col nome "backup") che includerà tutte le informazioni dal hd4me e i file con le informazioni sul video con `--backup`. Questo argomento scrive direttamente sul disco e non permette quindi di ordinare l'elenco.

```
> hd4me-cli "007" --backup
```

**Importante**:

Lo script ricerca le informazioni mancanti da IMDB **per ogni film elencato**, quindi maggiore è il numero di film trovati, più tempo sarà necessario per contattare IMDB, scaricare ed elaborare i dati, e visualizzare il risultato.
