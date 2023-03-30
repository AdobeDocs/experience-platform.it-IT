---
title: Corrispondenza fuzzy nel servizio query
description: Scopri come eseguire una corrispondenza sui dati di Platform che combina i risultati di più set di dati facendo corrispondere approssimativamente una stringa di tua scelta.
source-git-commit: a3a4ca4179610348eba73cf1239861265d2bf887
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 0%

---

# Corrispondenza fuzzy

Utilizza una corrispondenza &quot;sfocata&quot; sui dati della piattaforma per restituire le corrispondenze più probabili e approssimative senza la necessità di cercare stringhe con caratteri identici. Ciò consente una ricerca dei dati molto più flessibile e rende i dati più accessibili risparmiando tempo e fatica.

Invece di cercare di riformattare le stringhe di ricerca per farle corrispondere, la corrispondenza sfocata analizza il rapporto di somiglianza tra due sequenze e restituisce la percentuale di somiglianza. [!DNL FuzzyWuzzy] è consigliato per questo processo in quanto le sue funzioni sono più adatte per aiutare a far corrispondere stringhe in situazioni più complesse rispetto a [!DNL regex] o [!DNL difflib].

L&#39;esempio fornito in questo caso d&#39;uso si concentra sulla corrispondenza di attributi simili da una ricerca in una camera d&#39;albergo tra due diversi set di dati dell&#39;agenzia di viaggio. Il documento illustra come associare le stringhe in base al loro grado di somiglianza rispetto a grandi origini dati separate. In questo esempio, la corrispondenza fuzzy confronta i risultati della ricerca per le caratteristiche di una stanza dalle agenzie di viaggio Luma e Acme.

## Introduzione {#getting-started}

Come parte di questo processo richiede la formazione di un modello di apprendimento automatico, in questo documento si presuppone una conoscenza operativa di uno o più ambienti di apprendimento automatico.

Questo esempio utilizza [!DNL Python] e [!DNL Jupyter Notebook] ambiente di sviluppo. Sebbene siano disponibili molte opzioni, [!DNL Jupyter Notebook] è consigliato perché si tratta di un&#39;applicazione web open-source con requisiti di elaborazione ridotti. Può essere [scaricato dal sito ufficiale di Jupyter](https://jupyter.org/).

Prima di iniziare, è necessario importare le librerie necessarie. [!DNL FuzzyWuzzy] è un [!DNL Python] libreria basata su [!DNL difflib] e utilizzato per far corrispondere le stringhe. Usa [!DNL Levenshtein Distance] per calcolare le differenze tra sequenze e pattern. [!DNL FuzzyWuzzy] presenta i seguenti requisiti:

- [!DNL Python] 2.4 (o superiore)
- [!DNL Python-Levenshtein]

Dalla riga di comando, utilizza il seguente comando per installare [!DNL FuzzyWuzzy]:

```console
pip install fuzzywuzzy
```

Oppure usa il seguente comando per installare [!DNL Python-Levenshtein] inoltre:

```console
pip install fuzzywuzzy[speedup]
```

Ulteriori informazioni tecniche su [!DNL Fuzzywuzzy] si trova nella [documentazione ufficiale](https://pypi.org/project/fuzzywuzzy/).

### Connessione al servizio query

È necessario collegare il modello di apprendimento automatico a Query Service fornendo le credenziali di connessione. È possibile specificare sia le credenziali in scadenza che quelle non in scadenza. Vedi la [guida alle credenziali](../ui/credentials.md) per ulteriori informazioni su come acquisire le credenziali necessarie. Se utilizzi [!DNL Jupyter Notebook], consulta la guida completa su [come connettersi al servizio query](../clients/jupyter-notebook.md).

Inoltre, assicurati di importare il [!DNL numpy] inserisci nel pacchetto [!DNL Python] per abilitare l&#39;algebra lineare.

```python
import numpy as np
```

I comandi seguenti sono necessari per connettersi al servizio query da [!DNL Jupyter Notebook]:

```python
import psycopg2
conn = psycopg2.connect('''
sslmode=require
host=<YOUR_ORGANIZATION_ID>
port=80
dbname=prod:all
user=<YOUR_ADOBE_ID_TO_CONNECT_TO_QUERY_SERVICE>
password=<YOUR_QUERY_SERVICE_PASSWORD>
''')
cur = conn.cursor()
```

Le [!DNL Jupyter Notebook] L’istanza è ora connessa al servizio query. Se la connessione ha esito positivo, non verrà visualizzato alcun messaggio. Se la connessione non è riuscita, viene visualizzato un errore.

### Disegnare dati dal set di dati Luma {#luma-dataset}

I dati da analizzare sono ricavati dal primo set di dati con i seguenti comandi. Per brevità, gli esempi sono stati limitati ai primi 10 risultati della colonna.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Seleziona **Uscita** per visualizzare la matrice restituita.

+++Output

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Disegnare dati dal set di dati Acme {#acme-dataset}

I dati per l’analisi vengono ora estratti dal secondo set di dati con i seguenti comandi. Anche in questo caso, per brevità, gli esempi sono stati limitati ai primi 10 risultati della colonna.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Seleziona **Uscita** per visualizzare la matrice restituita.

+++Output

```console
array(['Deluxe King Or Queen Room', 'Kona Tower City / Mountain View',
       'Luxury Double Room', 'Alii Tower Ocean View With King Bed',
       'Club Two Queen', 'Corner Deluxe Studio',
       'Luxury Queen Room With Two Queen Beds', 'Grand Corner King Room',
       'Accessible Club Ocean View Suite With One King Bed',
       'Junior Suite'], dtype='<U66')
```

+++

### Creare una funzione di punteggio sfocato {#fuzzy-scoring}

Successivamente, devi importare `fuzz` dalla libreria FuzzyWuzzy ed esegui un confronto del rapporto parziale delle stringhe. La funzione del rapporto parziale consente di eseguire la corrispondenza della sottostringa. La stringa più breve viene presa in considerazione e corrisponde a tutte le sottostringhe della stessa lunghezza. La funzione restituisce un rapporto di somiglianza percentuale fino al 100%. Ad esempio, la funzione del rapporto parziale confronterebbe le seguenti stringhe &quot;Camera Deluxe&quot;, &quot;1 letto King&quot; e &quot;Camera King Deluxe&quot; e restituirebbe un punteggio di similarità del 69%.

Nel caso d&#39;uso di abbinamento della stanza dell&#39;hotel, questo viene fatto utilizzando i seguenti comandi:

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

Quindi, importa `cdist` dal [!DNL SciPy] per calcolare la distanza tra ciascuna coppia nelle due raccolte di input. Questo calcola i punteggi tra tutte le coppie di camere dell&#39;hotel fornite da ciascuna agenzia di viaggio.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Crea mappature tra le due colonne utilizzando il punteggio di join sfumato

Ora che le colonne sono state valutate in base alla distanza, è possibile indicizzare le coppie e mantenere solo le corrispondenze con un punteggio superiore a una determinata percentuale. In questo esempio vengono mantenute solo le coppie che corrispondono a un punteggio pari o superiore al 70%.

```python
matched_pairs = []
for i,c1 in enumerate(luma):
    idx = np.where(pairwise_distance[i,:] > 70)[0]
    for j in idx:
        matched_pairs.append((luma[i].replace("'","''"),acme[j].replace("'","''")))
```

I risultati possono essere visualizzati con il seguente comando. Per brevità, i risultati sono limitati a dieci righe.

```python
matched_pairs[:10]
```

Seleziona **Uscita** per vedere i risultati.

+++Output

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio')]
```

+++

I risultati vengono quindi confrontati utilizzando SQL con il seguente comando:

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## Applicare le mappature per eseguire un join fuzzy nel servizio query {#mappings-for-query-service}

Successivamente, le coppie di corrispondenza con punteggio elevato vengono unite utilizzando SQL per creare un nuovo set di dati.

```python
:
cur.execute('''
SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{}
'''.format(matching_sql)) 
[r for r in cur]
```

Seleziona **Uscita** per vedere i risultati di questo join.

+++Output

```console
[('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Standard Room, Lagoon View', 'Standard Room With Ocean View'),
 ('Standard Room, Lagoon View', 'Standard Room Dolphin Lagoon View'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room, 2 Queen Beds', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, Corner', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Suite', 'Corner Deluxe Studio'),
 ('Deluxe Suite', 'Deluxe Suite'),
 ('Deluxe Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Business King Room'),
 ('Business Double Room, 2 Double Beds', 'Double Room with Two Double Beds'),
 ('Business Double Room, 2 Double Beds',
  'Business Double Room With Two Double Beds'),
 ('Business Double Room, 2 Double Beds', 'Deluxe Double Room'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Traditional Double Room, 2 Double Beds',
  'Double Room with Two Double Beds'),
 ('Deluxe Suite, 1 Bedroom', 'Deluxe Suite'),
 ('City Room, City View', 'Room With City View'),
 ('City Room, City View', 'Queen Room With City View'),
 ('City Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Club Room, Premium 2 Queen Beds', 'Club Premium Two Queen'),
 ('Club Room, Premium 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, Lake View', 'Deluxe King Or Queen Room with Lake View'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('King Room, Suite, 1 King Bed with Sofa bed', 'King Room'),
 ('Deluxe Suite, 1 King Bed, Non Smoking, Kitchen', 'Deluxe Suite'),
 ('Junior Suite, 1 King Bed, Accessible (Roll-in Shower)', 'Junior Suite'),
 ('Regency Club, Mountain View', 'Regency Club Ocean View'),
 ('Regency Club, Mountain View', 'Regency Club Mountain View'),
 ('Club Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Room, Partial Ocean View', 'Room With Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View With Two Double Beds'),
 ('Room, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, Partial Ocean View', 'Waikiki Tower Partial Ocean View'),
 ('Premium Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Grand Corner King Room, 1 King Bed', 'Grand Corner King Room'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Deluxe Room, 1 King Bed, Non Smoking', 'Deluxe Room - One King Bed'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Accessible Partial Ocean View With Two Double Beds'),
 ('Room, 2 Double Beds, Accessible, Partial Ocean View',
  'Partial Ocean View Room'),
 ('Room, Ocean View ', 'Room With Ocean View'),
 ('Room, Ocean View ', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View ', 'Standard Room With Ocean View'),
 ('Signature Suite, 1 Bedroom', 'Signature King'),
 ('Room, 2 Queen Beds (Waikiki View)',
  'Queen Room With Two Queen Beds and Waikiki View'),
 ('Deluxe Room', 'Queen Room'),
 ('Deluxe Room', 'Deluxe Room (Non Refundable)'),
 ('Deluxe Room', 'Deluxe Room - Two Queen Beds'),
 ('Deluxe Room', 'Deluxe Room - One King Bed'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean View'),
 ('Standard Room, Oceanfront', 'Standard Room With Ocean Front View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (City View - Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('High-Floor Premium Room, 1 King Bed', 'High-Floor Premium King Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Junior Suite'),
 ('Junior Suite, 1 King Bed with Sofa Bed', 'Deluxe King Suite With Sofa Bed'),
 ('Deluxe Room, City View', 'Queen Room With City View'),
 ('Deluxe Room, City View', 'Club Level King Or Queen Room with City View'),
 ('Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Room, 1 King Bed', 'Ocean View Room With King Bed'),
 ('Room, 1 King Bed', 'Royal Club Premier Room - One King Bed'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Kona Tower Partial Ocean View'),
 ('Room, 2 Double Beds, Partial Ocean View', 'Partial Ocean View Room'),
 ('Room, 1 Queen Bed, City View',
  'Queen Room With Two Queen Beds and City View'),
 ('Room, Ocean View', 'Room With Ocean View'),
 ('Room, Ocean View', 'King Or Two Queen Room With Ocean View'),
 ('Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Partial Ocean View Room'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Kona Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Standard Room, Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean View'),
 ('Standard Room, Partial Ocean View (Waikiki Tower) - No Resort Fee',
  'Standard Room With Ocean Front View'),
 ('Regency Club, Ocean View',
  'Accessible Club Ocean View Suite With One King Bed'),
 ('Regency Club, Ocean View', 'Regency Club Ocean View'),
 ('Regency Club, Ocean View', 'Regency Club Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Mountain View'),
 ('Standard Room, Mountain View (Scenic)', 'Standard Room With Ocean View'),
 ('Room, 1 Queen Bed', 'Deluxe Room - Two Queen Beds'),
 ('Double Room', 'Luxury Double Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Queen Room'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Double Room with Two Double Beds'),
 ('Double Room', 'Business Double Room With Two Double Beds'),
 ('Double Room', 'Deluxe Double Room'),
 ('Club Room, 1 King Bed', 'Deluxe Room - One King Bed'),
 ('Premier Twin Room', 'High-Floor Premium King Room'),
 ('Premier Twin Room', 'Premier King Room'),
 ('Premier Twin Room', 'Premier Queen Room With Two Queen Beds'),
 ('Premier Twin Room', 'Premium King Room With Free Wi-Fi'),
 ('Premium Room, 1 Queen Bed', 'Premium Two Queen'),
 ('Premium Room, 2 Queen Beds', 'Premium Two Queen'),
 ('Deluxe Room, 1 Queen Bed (High Floor)', 'Deluxe Room - Two Queen Beds'),
 ('Room, 2 Queen Beds, Garden View',
  'Queen Room With Two Queen Beds and Garden View'),
 ('Signature Room, 2 Queen Beds', 'Deluxe Room - Two Queen Beds'),
 ('Signature Room, 2 Queen Beds', 'Signature Two Queen'),
 ('Standard Room, Ocean View', 'Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean View'),
 ('Standard Room, Ocean View', 'Standard Room With Ocean Front View')]
```

+++

### Salvare i risultati della corrispondenza approssimativa su Platform {#save-to-platform}

Infine, i risultati della corrispondenza approssimativa possono essere salvati come set di dati da utilizzare in Adobe Experience Platform utilizzando SQL.

```python
cur.execute(''' 
Create table luma_acme_join
AS
(SELECT *  FROM luma e
CROSS JOIN acme b
WHERE 
{})
'''.format(matching_sql))
```


