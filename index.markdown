---
layout: default
---

* Table of contents
{:toc}

# Domande d'esame

{% for domanda in site.data.domande %}

{{ domanda.domanda | markdownify }}

<details>
    <summary><strong>Soluzione</strong></summary>

    {{ domanda.soluzione | markdownify }}
</details>

{% endfor %}

# Lezione 6 - Documentazione
## Esercizio 1 (slide 21)

Il comando `cd` è interno. Come è possibile ottenere la relativa documentazione?
È possibile ottenere documentazione sul comando esterno `ls` in maniera analoga?

## Esercizio 2 (slide 31)

L'eseguibile `dd` è un comando esterno. Come è possibile ottenere documentazione su di esso?

## Esercizio 3 (slide 36)

**Traccia**

Si consideri la parola chiave di ricerca `stat`. Si stabilisca se essa è contenuta in più sezioni del manuale ed, in caso affermativo, si elenchino quali.

**Soluzione**

Eseguendo `man -a stat` si scopre che `stat` è disponibile sia come eseguibile (`/usr/bin/stat`) sia come funzione di libreria, quindi è sia nella sezione 1 che nella
sezione 2 del manuale.

## Esercizio 4 (slide 39)

**Traccia**

Trovare la documentazione relativa allo shell builtin che permette di attendere la terminazione di un'applicazione.

**Soluzione**

Eseguendo `man bash-builtins` e cercando il termine `wait` si giunge al builtin `wait`.

## Esercizio 5 (slide 44)

**Traccia**

Trovare un comando esterno che calcola il checksum di un file.

**Soluzione**

La traccia chiede di cercare un **comando esterno**, quindi la ricerca dev'essere fatta nella 1° sezione del manuale. Eseguendo la ricerca con il termine `checksum`
vengono restituiti diversi comandi:
```
$ apropos -s 1 checksum
cksum (1)            - checksum and count the bytes in a file
shasum (1)           - Print or Check SHA Checksums
sum (1)              - checksum and count the blocks in a file
```

# Lezione 7 - File
## Esercizio 1 (slide 32)

**Traccia**

A quale file speciale di dispositivo corrisponde il dispositivo “primo disco SATA”? 
Che cosa si può ottenere con l’accesso a tale dispositivo?

**Soluzione**

Il primo disco SATA è rappresentato dal file speciale di dispositivo `/dev/sda1`.
Accedendo ad esso è possibile vedere i byte presenti in tale disco.

## Esercizio 2 (slide 54)

**Traccia**

Si stampi l’insieme dei metadati per i file seguenti:
- `$HOME`
- `/tmp/.X11-unix/X0`
- `/dev/sda1`
- `/dev/tty0`
Notate delle differenze?

**Soluzione**
```
$ stat $HOME
  File: /home/studente
  Size: 4096      	Blocks: 8          IO Block: 4096   directory
Device: 801h/2049d	Inode: 273597      Links: 22
Access: (0755/drwxr-xr-x)  Uid: ( 1000/studente)   Gid: ( 1000/studente)
Access: 2022-02-14 08:34:47.330047501 +0100
Modify: 2022-02-14 08:35:26.426049007 +0100
Change: 2022-02-14 08:35:26.426049007 +0100
 Birth: 2021-12-01 12:25:10.740210166 +0100

$ stat /tmp/.X11-unix/X0
  File: /tmp/.X11-unix/X0
  Size: 0         	Blocks: 0          IO Block: 4096   socket
Device: 801h/2049d	Inode: 2884071     Links: 1
Access: (0755/srwxr-xr-x)  Uid: ( 1000/studente)   Gid: ( 1000/studente)
Access: 2022-01-04 12:13:29.268627270 +0100
Modify: 2022-01-04 12:13:29.268627270 +0100
Change: 2022-01-04 12:13:29.268627270 +0100
 Birth: 2022-01-04 12:13:29.268627270 +0100

$ stat /dev/sda1
  File: /dev/sda1
  Size: 0         	Blocks: 0          IO Block: 4096   block special file
Device: 5h/5d	Inode: 199         Links: 1     Device type: 8,1
Access: (0660/brw-rw----)  Uid: (    0/    root)   Gid: (    6/    disk)
Access: 2022-01-04 12:12:54.416000536 +0100
Modify: 2022-01-04 12:12:48.272000299 +0100
Change: 2022-01-04 12:12:48.272000299 +0100
 Birth: -

$ stat /dev/tty0
  File: /dev/tty0
  Size: 0         	Blocks: 0          IO Block: 4096   character special file
Device: 5h/5d	Inode: 13          Links: 1     Device type: 4,0
Access: (0620/crw--w----)  Uid: (    0/    root)   Gid: (    5/     tty)
Access: 2022-01-04 12:12:47.760000279 +0100
Modify: 2022-01-04 12:12:47.760000279 +0100
Change: 2022-01-04 12:12:47.760000279 +0100
 Birth: -
```

## Esercizio 3 (slide 63)

**Traccia**

Elencate la directory `/etc` nella modalità seguente:
- ricorsivamente;
- con i metadati;
- con i file nascosti.

**Soluzione**

- Elenco ricorsivo: `ls -R /etc`;
- Elenco con i metadati: `ls -l /etc`
- Elenco con i file nascosti: `ls -a /etc`

## Esercizio 4 (slide 71)

**Traccia**

Individuate il tipo di file dei file seguenti:
- `$HOME`
- `/tmp/.X11-unix/X0`
- `/dev/sda1`
- `/dev/tty0`
- `/usr/bin/editor`

**Soluzione**

```
$ file $HOME /tmp/.X11-unix/X0 /dev/sda1 /dev/tty0 /usr/bin/editor
/home/studente:    directory
/tmp/.X11-unix/X0: socket
/dev/sda1:         block special (8/1)
/dev/tty0:         character special (4/0)
/usr/bin/editor:   symbolic link to /etc/alternatives/editor
```

## Esercizio 5 (slide 81)

**Traccia**

Si crei un file nuovo di contenuto nullo. Leggendo la pagina manuale del comando relativo, si individui un modo per impostare i timestamp al 1/1/1970, ore 00:00.

**Soluzione**

```
$ touch -t 197001010000 new
$ stat new
  File: new
  Size: 0         	Blocks: 0          IO Block: 4096   regular empty file
Device: 801h/2049d	Inode: 655894      Links: 1
Access: (0644/-rw-r--r--)  Uid: ( 1000/studente)   Gid: ( 1000/studente)
Access: 1970-01-01 00:00:00.000000000 +0100
Modify: 1970-01-01 00:00:00.000000000 +0100
Change: 2022-02-14 09:27:08.706168501 +0100
 Birth: 2022-02-14 09:27:08.706168501 +0100
```

## Esercizio 6 (slide 86)

**Traccia**

Si crei la seguente gerarchia di directory: `dir1/dir2/dir3`

**Soluzione**

```
$ mkdir -p dir1/dir2/dir3
```

## Esercizio 7

**Traccia**

Create dieci file vuoti con i nomi seguenti:
`file1` `file2` `file3` `file4` `file5` `file6` `file7` `file8` `file9` `file10`

Cancellate i file appena creati.

**Soluzione**

```
$ touch file{1..10}
studente@riccardo-vm-debian:~/sistemi-operativi/lezione-7-file$ ls -l
total 0
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file1
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file10
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file2
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file3
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file4
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file5
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file6
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file7
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file8
-rw-r--r-- 1 studente studente 0 Feb 14 09:33 file9
$ rm file{1..10}
$ ls
```

## Esercizio 8 (slide 101)

**Traccia**

Create un backup della propria home directory nella directory `/tmp`.

**Soluzione**

```
$ cp -r ~ /tmp/home_studente
```

## Esercizio 9 (slide 104)

**Traccia**

Studiate la pagina di manuale di `mv` e individuate un metodo per creare backup dei file sovrascritti.

**Soluzione**

Si possono usare le opzioni `--backup[=CONTROL]` o `-b`.

## Esercizio 10 (slide 139)

**Traccia**

Leggendo la pagina di manuale del comando opportuno, individuate un modo per stampare un file “al contrario” (dall’ultima alla prima riga).
Applicate tale metodo per stampare le righe del file `/etc/passwd` dall’ultima alla prima.

**Soluzione**

Proviamo a cercare un qualche comando che contiene "reverse" nella propria descrizione:
```
$ apropos -s 1 "reverse"
col (1)              - filter reverse line feeds from input
rev (1)              - reverse lines characterwise
tac (1)              - concatenate and print files in reverse
xxd (1)              - make a hexdump or do the reverse.
```

Il comando per risolvere l'esercizio è `tac` (che, curiosamente, è l'inverso di `cat`).

```
$ tac `/etc/passwd`
```

## Esercizio 11 (slide 148)

**Traccia**

Visualizzate nella forma canonica di `hexdump` i primi 32 byte dei file seguenti:
- `/usr/bin/ls`
- `/usr/bin/bash`
- `/usr/bin/which`

Notate qualche differenza?

**Soluzione**

Di default `hexdump` mostra il contenuto dell'intero file. Per vedere soltanto i primi 32 byte bisogna usare l'opzione `-n`.

```
$ hexdump -C -n 32 /usr/bin/ls
00000000  7f 45 4c 46 02 01 01 00  00 00 00 00 00 00 00 00  |.ELF............|
00000010  03 00 3e 00 01 00 00 00  60 61 00 00 00 00 00 00  |..>.....`a......|
00000020

$ hexdump -C -n 32 /usr/bin/bash
00000000  7f 45 4c 46 02 01 01 00  00 00 00 00 00 00 00 00  |.ELF............|
00000010  03 00 3e 00 01 00 00 00  80 06 03 00 00 00 00 00  |..>.............|
00000020

$ hexdump -C -n 32 /usr/bin/which
00000000  23 21 20 2f 62 69 6e 2f  73 68 0a 73 65 74 20 2d  |#! /bin/sh.set -|
00000010  65 66 0a 0a 69 66 20 74  65 73 74 20 2d 6e 20 22  |ef..if test -n "|
00000020
```

Leggendo l'output si nota che `/usr/bin/ls` e `/usr/bin/bash` sono due eseguibili ELF, mentre `/usr/bin/which` è uno script.

## Esercizio 12 (slide 155)

**Traccia**

Individuate due modi distinti in head per stampare i primi 1024 byte del file `/bin/ls`.

**Soluzione**

Il numero di byte da leggere può essere passato in byte oppure in forma umana:

```
head -c 1024 /bin/ls
head -c 1K /bin/ls
```

## Esercizio 13 (slide 164)

Stampate il primo ed il settimo campo di ogni riga dell’archivio testuale `/etc/passwd`.

**Soluzione**

```
$ cut -f 1,7 -d : /etc/passwd
```

- l'opzione `-f 1,7` prende il 1° ed il 7° campo;
- l'opzione `-d :` dice a `cut` che il separatore è il carattere `:`

## Esercizio 14 (slide 166)

Stampate i primi tre caratteri di ogni riga dell’archivio testuale `/etc/passwd`.

**Soluzione**

```
$ cut -c 1-3 /etc/passwd
```

## Esercizio 15 (slide 172)

Producete un output multicolonnare nel modo seguente:
- Prima colonna. Una sequenza di numeri interi crescenti a partire da 1.
- Seconda colonna. Gli username esistenti nel sistema (primo campo).
- Terza colonna. Le shell assegnate agli username (ultimo campo).

{% capture soluzioneEs15Lezione7 %}
``` bash
# Crea il file id.txt con i numeri da 1 a 10 (uno per ogni riga)
for i in {1..10}; do
    echo $i >> id.txt;
done

# Estrae gli username dal file /etc/passwd
cut --fields=1 --delimiter=':' /etc/passwd > user.txt

# Estrae le shell dal file /etc/passwd
cut --fields=7 --delimiter=':' /etc/passwd > shell.txt

# Incolla tutti i file insieme
paste id.txt user.txt shell.txt > output.txt
```
{% endcapture %}

{% include soluzione.html content=soluzioneEs15Lezione7 %}

## Esercizio 16 (slide 183)

Ordinate nel modo seguente il file `/etc/passwd`:
- Ordinamento: numerico crescente.
- Campo: quarto.
- Separatore: due punti.

{% capture soluzione16Lezione7 %}
```
$ sort -n -k 4 -t : /etc/passwd
```

- l'opzione `-n` abilita l'ordinamento numerico crescente;
- l'opzione `-k 4` indica a `sort` di ordinare in base al 4° campo;
- l'opzione `-t :` dice a `sort` che il separatore tra i campi del file passato come argomento è il carattere `:`

Per convicersi che l'ordinamento funziona si può usare `cut` in questo modo:

```
$ sort -n -k 4 -t : /etc/passwd | cut -f 4 -d :
0
1
1
2
3
7
8
9
10
12
13
```
{% endcapture %}
{% include soluzione.html content=soluzione16Lezione7 %}

## Esercizio 17 (slide 190)

Nell’ipotesi che un file di configurazione verifichi il pattern di shell `*.log`, individuate tutti i file di log nel sistema.

{% capture soluzione17Lezione7 %}
``` bash
find / -name '*.log' 2>/dev/null
```
{% endcapture %}
{% include soluzione.html content=soluzione17Lezione7 %}

## Esercizio 18 (slide 207)

Individuate tutti i file HTML nel sistema. 
In prima approssimazione, considerate come file HTML un file terminante in:
- `.html`
- `.htm`
- `.HTML`
- `.HTM`

{% capture soluzione18Lezione7 %}
``` bash
find / -iregex '^.*\.html?$' 2>/dev/null
```
{% endcapture %}
{% include soluzione.html content=soluzione18Lezione7 %}

## Esercizio 19 (slide 209)

Individuate tutti i file più grandi di 1MB presenti nell’intero sistema.

{% capture soluzione19Lezione7 %}
``` bash
find / -size +1M 2>/dev/null
```
{% endcapture %}
{% include soluzione.html content=soluzione19Lezione7 %}

## Esercizio 20 (slide 212)

Producete un elenco di tutti i file nel sistema con relativa dimensione:
- `/file1 dimensione1`
- `/file2 dimensione2`
- `...`

{% capture soluzione20Lezione7 %}
``` bash
find / -printf "%p %s\n" 2>/dev/null
```
{% endcapture %}
{% include soluzione.html content=soluzione20Lezione7 %}

## Esercizio 21 (slide 215)

Individuate tutti i file che verificano una delle proprietà seguenti:
- terminano con `.bak`;
- terminano con `~`.

Cancellate forzatamente i file individuati.

{% capture soluzione21Lezione7 %}
``` bash
find / -regex '^.*\(\(\.bak\)\|\(~\)\)$' -exec rm -f {} + 2>/dev/null
find / -regextype egrep -regex '^.*((\.bak)|(~))$' -exec rm -f {} + 2>/dev/null # con -regextype egrep si evitano molti escape nella regex
```
{% endcapture %}
{% include soluzione.html content=soluzione21Lezione7 %}

## Esercizio 22 (slide 242)

Stampate i valori di tutte le etichette `UUID` nel file `/etc/fstab`.
Se possibile, evitate di stampare la stringa `UUID=`.

{% capture soluzione22Lezione7 %}
Le righe che ci interessano del file `/etc/fstab` sono queste:
```
UUID=e1391b9c-8e31-48dd-ab59-fd8b690bced3 /               ext4    errors=remount-ro 0       1
UUID=f228e4a0-ae98-4030-aa3b-67ad6c720fb4 none            swap    sw              0       0
```
La regex per matchare soltanto il valore dello UUID è `[a-f0-9]{7}-([a-f0-9]{4}-){3}[a-f0-9]{12}`.

Il comando per risolvere l'esercizio è:
``` bash
grep -Eo '[a-f0-9]{7}-([a-f0-9]{4}-){3}[a-f0-9]{12}' /etc/fstab 
```
```
1391b9c-8e31-48dd-ab59-fd8b690bced3
228e4a0-ae98-4030-aa3b-67ad6c720fb4
```
{% endcapture %}
{% include soluzione.html content=soluzione22Lezione7 %}

-------------------------------------

{% for lezione in site.data.lezioni %}
# Lezione {{ lezione.numero }} - {{ lezione.titolo }}

{% for esercizio in lezione.esercizi %}
## Esercizio {{ esercizio.numero }} (slide {{ esercizio.slide }})

{{ esercizio.traccia | markdownify }}

<details>
    <summary><strong>Soluzione</strong></summary>

    {{ esercizio.soluzione | markdownify }}
</details>

{% endfor %} {% comment %} esercizio {% endcomment %}
{% endfor %} {% comment %} lezione {% endcomment %}
