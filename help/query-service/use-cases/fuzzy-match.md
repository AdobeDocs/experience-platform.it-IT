---
title: Corrispondenza fuzzy in Query Service
description: Scopri come eseguire una corrispondenza sui dati di Platform che combina i risultati di più set di dati approssimativamente corrispondendo una stringa di tua scelta.
exl-id: ec1e2dda-9b80-44a4-9fd5-863c45bc74a7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 0%

---

# Corrispondenza fuzzy in Query Service

Utilizza una corrispondenza &quot;fuzzy&quot; nei dati Adobe Experience Platform per restituire le corrispondenze più probabili e approssimative senza dover cercare stringhe con caratteri identici. Questo consente una ricerca molto più flessibile dei dati e li rende più accessibili risparmiando tempo e fatica.

Invece di provare a riformattare le stringhe di ricerca per farle corrispondere, la corrispondenza sfocata analizza il rapporto di somiglianza tra due sequenze e restituisce la percentuale di somiglianza. [[!DNL FuzzyWuzzy]](https://pypi.org/project/fuzzywuzzy/) è consigliato per questo processo in quanto le sue funzioni sono più adatte per consentire la corrispondenza di stringhe in situazioni più complesse rispetto a [!DNL regex] o [!DNL difflib].

L’esempio fornito in questo caso d’uso si concentra sulla corrispondenza di attributi simili da una ricerca nella camera d’albergo in due diversi set di dati dell’agenzia di viaggio. Il documento illustra come far corrispondere le stringhe in base al loro grado di somiglianza da grandi origini dati separate. In questo esempio, fuzzy match confronta i risultati della ricerca per le caratteristiche di una stanza delle agenzie di viaggio Luma e Acme.

## Introduzione {#getting-started}

Poiché parte di questo processo richiede la formazione di un modello di apprendimento automatico, il presente documento presuppone una conoscenza operativa di uno o più ambienti di apprendimento automatico.

Questo esempio utilizza [!DNL Python] e l&#39;ambiente di sviluppo [!DNL Jupyter Notebook]. Sebbene siano disponibili molte opzioni, [!DNL Jupyter Notebook] è consigliato in quanto si tratta di un&#39;applicazione Web open-source con requisiti di calcolo ridotti. Può essere scaricato da [il sito ufficiale Jupyter](https://jupyter.org/).

Prima di iniziare, è necessario importare le librerie necessarie. [!DNL FuzzyWuzzy] è una libreria [!DNL Python] open source creata sulla libreria [!DNL difflib] e utilizzata per trovare stringhe corrispondenti. Utilizza [!DNL Levenshtein Distance] per calcolare le differenze tra sequenze e pattern. [!DNL FuzzyWuzzy] ha i seguenti requisiti:

- [!DNL Python] 2.4 (o versione successiva)
- [!DNL Python-Levenshtein]

Dalla riga di comando, utilizzare il comando seguente per installare [!DNL FuzzyWuzzy]:

```console
pip install fuzzywuzzy
```

Oppure usa il seguente comando per installare anche [!DNL Python-Levenshtein]:

```console
pip install fuzzywuzzy[speedup]
```

Ulteriori informazioni tecniche su [!DNL Fuzzywuzzy] sono disponibili nella [documentazione ufficiale](https://pypi.org/project/fuzzywuzzy/).

### Connetti a Query Service

È necessario collegare il modello di apprendimento automatico a Query Service fornendo le credenziali di connessione. È possibile fornire credenziali sia in scadenza che non in scadenza. Per ulteriori informazioni su come acquisire le credenziali necessarie, vedere la [guida alle credenziali](../ui/credentials.md). Se utilizzi [!DNL Jupyter Notebook], leggi la guida completa su [come connetterti a Query Service](../clients/jupyter-notebook.md).

Assicurarsi inoltre di importare il pacchetto [!DNL numpy] nell&#39;ambiente [!DNL Python] per abilitare l&#39;algebra lineare.

```python
import numpy as np
```

I comandi seguenti sono necessari per connettersi a Query Service da [!DNL Jupyter Notebook]:

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

L&#39;istanza [!DNL Jupyter Notebook] è ora connessa a Query Service. Se la connessione ha esito positivo, non viene visualizzato alcun messaggio. Se la connessione non è riuscita, viene visualizzato un errore.

### Dati Draw dal set di dati Luma {#luma-dataset}

I dati per l’analisi vengono estratti dal primo set di dati con i seguenti comandi. Per brevità, gli esempi sono stati limitati ai primi 10 risultati della colonna.

```python
cur.execute('''SELECT * FROM luma;
''')    
luma = np.array([r[0] for r in cur])

luma[:10]
```

Seleziona **Output** per visualizzare l&#39;array restituito.

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

### Dati Draw dal set di dati Acme {#acme-dataset}

I dati per l’analisi vengono ora estratti dal secondo set di dati con i seguenti comandi. Anche in questo caso, per brevità, gli esempi sono stati limitati ai primi 10 risultati della colonna.

```python
cur.execute('''SELECT * FROM acme;
''')    
acme = np.array([r[0] for r in cur])

acme[:10]
```

Seleziona **Output** per visualizzare l&#39;array restituito.

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

### Creare una funzione di punteggio fuzzy {#fuzzy-scoring}

È quindi necessario importare `fuzz` dalla libreria FuzzyWuzzy ed eseguire un confronto delle proporzioni parziali delle stringhe. La funzione di rapporto parziale consente di eseguire la corrispondenza della sottostringa. Questa opzione consente di prendere la stringa più breve e di farla corrispondere a tutte le sottostringhe della stessa lunghezza. La funzione restituisce un rapporto di somiglianza percentuale fino al 100%. Ad esempio, la funzione di rapporto parziale confronta le seguenti stringhe &quot;Camera Deluxe&quot;, &quot;1 Letto King&quot; e &quot;Camera Re Deluxe&quot; e restituisce un punteggio di somiglianza del 69%.

Nel caso di utilizzo di corrispondenza della camera di hotel, questa operazione viene eseguita utilizzando i seguenti comandi:

```python
from fuzzywuzzy import fuzz
def compute_match_score(x,y):
    return fuzz.partial_ratio(x,y)
```

Importare quindi `cdist` dalla libreria [!DNL SciPy] per calcolare la distanza tra ciascuna coppia nei due insiemi di input. In questo modo vengono calcolati i punteggi di tutte le coppie di camere di hotel fornite da ciascuna agenzia di viaggio.

```python
from scipy.spatial.distance import cdist
pairwise_distance =  cdist(luma.reshape((-1,1)),acme.reshape((-1,1)),compute_match_score)
```

### Creare mappature tra le due colonne utilizzando il punteggio di join fuzzy

Ora che le colonne sono state valutate in base alla distanza, puoi indicizzare le coppie e mantenere solo le corrispondenze con un punteggio superiore a una determinata percentuale. In questo esempio vengono mantenute solo le coppie corrispondenti a un punteggio pari o superiore al 70%.

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

Seleziona **Output** per visualizzare i risultati.

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

I risultati vengono quindi associati utilizzando SQL con il seguente comando:

<!-- Q) Why and is this accurate? -->

```python
matching_sql = ' OR '.join(["(e.luma = '{}' AND b.acme = '{}')".format(c1,c2) for c1,c2 in matched_pairs])
```

## Applicare le mappature per eseguire un join fuzzy in Query Service {#mappings-for-query-service}

Successivamente, le coppie corrispondenti con punteggio elevato vengono unite utilizzando SQL per creare un nuovo set di dati.

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

Seleziona **Output** per visualizzare i risultati di questo join.

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

### Salva risultati di corrispondenza approssimativi in Platform {#save-to-platform}

Infine, i risultati della corrispondenza fuzzy possono essere salvati come set di dati da utilizzare in Adobe Experience Platform utilizzando SQL.

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
